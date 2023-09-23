# Design

## Stack sides

- one axis for stacking machines (2 sides)
- one side for energy
- one side me (optional)
- 2 sides Enderio

## Needed Buffers

- Item Input Buffer 
    - for all enderio item inputs
    - a drawerwall (no controller needed)
    - exportbus into the drawer
    - enderio out of the drawer

- Primary Item Storage
    - drawerWall with controller
    - itemconduit into the controller (code blue)
    - storagebus the controller (put and get; high prio)

- Secondary Item Storage
    - drawerWall with controller
    - itemconduit into the controller (code red)
    - storagebus the controller (only get; low prio)
    - all drawers have void upgrade

- Primary Fluid Storage
    - Drums
    - fluidconduit on each (code blue)
    - fluid storage bus on each (put and get; high prio)

- Secondary Fluid Storage
    - Drums
    - fluidconduit on each (code red)
    - fluid storage bus on each (get only; low prio)
    - some trashcans 
        - with fluid conduit (code red; low prio; filtered)

# Fluid Input

- We need to use storage bus + interface or export bus, so that we can prioritize Secondary over Primary Storage.
- We use Fluid Input with interfaces with pumps.


# Item Input

- We need to use storage bus + interface or export bus, so that we can prioritize Secondary over Primary Storage.
- When there are multiple inputs, need to use export to input buffer + enderio itemconduits.
- When there is a single item, we could theoretically use Export bus or Interface, but if the item is already in the input buffer (or will be there in the future), we can reuse it and use an EnderIO Conduit.

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



## Rules:

- don't use import busses
- pipe out secondaries with enderio to secondary buffers
- item inputs via input buffer and enderio cables
- fluid input with ME FluidInterfaces (or FluidExportBus, if you dont have an fluid output) (so we don't need input buffers)
- reuse the FluidInterface for primary fluid output.

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

