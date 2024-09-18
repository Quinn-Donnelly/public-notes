---
parent:
  - "[[Software Architecture]]"
aliases: 
---
# Summary 
Architecture pattern that aims to isolate failures to units called cells. Where in a cell can independently service functionality such that the failure of one cell won't affect others.
# Body
![[ship bulkhead.png]]
The idea comes from a Bulkhead on a ship where in a hole in one part of the ship doesn't mean the ship is sunk as it only needs N subsections to still be empty to float. 


Here is an example of AWS cell based implementation 
![[aws-cell-based-arc.png]]
- **Cell router** — We also refer to this layer as the _thinnest possible layer_, with the responsibility of routing requests to the right cell, and only that.
    
- **Cell** — A complete workload, with everything needed to operate independently.
    
- **Control plane** — Responsible for administration tasks, such as provisioning cells, de-provisioning cells, and migrating cell customers.