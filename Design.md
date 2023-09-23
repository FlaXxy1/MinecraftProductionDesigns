# Design

An extra ME Network is needed for production. Not connected to the main one.

Some Storages of the Production Network are also attached to the Main Network. (putget or getonly)

## Stack sides

- one axis for stacking machines (2 sides)
- one side for energy
- one side me (optional)
- 2 sides Enderio

## Needed Buffers

- Item Input Buffer 
    - for all enderio item inputs to machines
    - a drawerwall (no controller needed)
    - exportbus From the production network into each drawer
    - enderio out of the drawer
    - optionally attach it as readonly storage to the main network.

- External Input Item Buffer
    - a drawerwall with controller
    - storagebus the controller from Production network (get; high prio)
    - manual insertion of items in here

- Primary Item Storage
    - drawerWall with controller
    - itemconduit into the controller (code blue)
    - storagebus the controller from Production network (put and get; high prio)
    - attach it as putget storage to the main network.

- Secondary Item Storage
    - drawerWall with controller
    - itemconduit into the controller (code red)
    - storagebus the controller from Production network (only get; low prio)
    - all drawers have void upgrade
    - optionally attach it as readonly storage to the main network.

- Primary Fluid Storage
    - Drums
    - fluidconduit on each (code blue)
    - fluid storage bus from Production network on each (put and get; high prio)
    - attach it as putget storage to the main network.

- Secondary Fluid Storage
    - Drums
    - fluidconduit on each (code red)
    - fluid storage bus on each (get only; low prio)
    - some trashcans 
        - with fluid conduit (code red; low prio; filtered)
    - attach it as readonly storage to the main network.

## Rules:

- don't use import busses
- pipe out secondaries with enderio to secondary buffers
- use enderio itemconduit via input buffer, when having multiple inputs or when the item comes from the main network 
- fluid input with ME FluidInterfaces + pump (or FluidExportBus, if you dont have an fluid output) (so we don't need input buffers)
- reuse the FluidInterface for primary fluid output.

# Reasoning

## Fluid Input

- We need to use storage bus + interface or export bus, so that we can prioritize Secondary over Primary Storage.
- If we use Enderio conduits for input, we need an input buffer. (as the source still needs to be the ME Network)
- We use Fluid Input with interfaces with pumps.


# Item Input

- We need to use storage bus + interface or export bus, so that we can prioritize Secondary over Primary Storage.
- When there are multiple inputs, need to use export to input buffer + enderio itemconduits.
- When there is a single item, we could theoretically use Export bus or Interface
    - but if the item is already in the input buffer (or will be there in the future), we can reuse it and use an EnderIO Conduit.

# Fluid Output

- primary fluid output can be done with enderio or ME Interface
- but if you also need fluid input, you can resue a fluid interface.
- fluid input can't be done with a single storage interface (like the drawercontroller), because there is no method to input fluids into the ME system without possibility of clogging, when the storage blocks.
- theoretically Secodary Fluid Storage could be done with a single FluidInterface, as long as the contents are voided (would need a low prio trash can storage)

# If then

What is needed for the machine

Item Input: None, Single, Multiple
Fluid Input: None, Some
Item Output: None, P(rimary), S(econdary), PS
Fluid Output: None, P(rimary), S(econdary), PS


| Item Input | Fluid Input | Item Output | Fluid Output | Solution     |
|------------|-------------|-------------|--------------|--------------|
| None       | Some        |             |              |              |
| Single     |             |             |              |              |
| Multiple   |             |             |              |              |
|            |             |             |              |              |
|            |             |             |              |              |
|            |             |             |              |              |
|            |             |             |              |              |
| Multiple   | Some        | PS          | PS           | (Worst case) |



## Worst case

- multiple item inputs
- some fluid inputs
- PS item outputs
- PS Fluid outputs

Solution:
- first side Enderio
    - item input with limited item filter + input buffer
    - primary item output
- second side ME Fluid Interface
    - fluid Input
    - primary fluid output
- third side enderio
    - secondary item output
    - secondary fluid output

