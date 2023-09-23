# Machine IOs

## Optimize Space

A Machine has only limited sides to interface with it. 

- For Gregtech machines, one side will always be exclusively Energy.
- Another Axis (2 sides) should be used to stack more machines. (Stacking Axis)
- The front face of gregtech machines are sometimes limited, but you can turn it, so that the front side points towads one of the Stacking Axis sides.

So you are left with 3 sides of interfacing.
Ideally you only use EnderIO conduits, when optimizing space.

## Fluids

2 options for fluids insertion

### ME

- using a fluid export bus or a fluid interface with a pump
- both take the side exclusively and require the whole side of the stack to be ME
- both options can provide multiple fluids at once (fluids don't overflow to other slots)
- when using a fluid interface, you can also export primary fluids on this side. (need to enable input at output side on the machine)

### Enderio

- using the EnderIO fluid conduits
- can use fluid and item in one place
- can't be used with ME
- need an external input buffer
- can also extract primary and secondary fluids (only one at a time)



## Items


## Capability Matrix

This matrix lists the possibilities. You can't simultaneaously output to primary and secondary.

Option   | Primary Fluid Output | Secondary Fluid Output | Primary Item Output | Secondary Item Output | Single Fluid Input | Multiple Fluid Input | Single Item Input | Multiple Item Input
---------|----------------------|------------------------|---------------------|-----------------------|--------------------|----------------------|-------------------|--------------------
Enderio  | ✅                    | ✅                      | ✅                   | ✅                     | ✅                  | ✅                    | ✅                 | ✅
ME Fluid | ✅                    | ❌                      | ❌                   | ❌                     | ✅                  | ✅                    | ❌                 | ❌
ME Item  | ❌                    | ❌                      | ✅                   | ✅                     | ❌                  | ❌                    | ✅                 | ❌
