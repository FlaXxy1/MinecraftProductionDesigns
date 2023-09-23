# Storage Types

Use different storages as outputs for different purposes.

Primary outputs of a machine are connected to Primary Storage, secondary outputs are connected to secondary storage.

Machines can have any combination of Primary and secondary outputs.

When a machine only has secondary outputs, it will always run and potentially void all outputs.

When you have 2 secondary outputs, it's sometimes better to have 2 same machines with each machine having one output as primary.


# Primary Storage

- don't take any more items/fluid, when limit reached
- are connected to ME as high prio storage (insert and extract)
- drawers for items
- drums for fluids
- enderio inputs from code blue

# Secondary Storage

- always will take items/fluids; void excess
- are connected to ME as low prio storage (extract only)
- drawers with voiding upgrades for items
- drum + trashcan for fluids
- when inserting, use secondary channel
- enderio inputs from code red

# Input Buffer

When using EnderIo Itemconduits to insert into machines, the Items need to be pulled out of the system into an InputBuffer.
This can be either an ME Interface or a Drawer with ME Export Busses attached.