# Inventory Routing Problem
## Known
### Set
| Set | Description | Size | Element | Remark |
| - | - | - | - | - |
| $M$ | Customers | $[1,N]$ | $i,j$ |  |
| $\cal F$ | Time | $[1,H]$ | $t$ |  |
| ${\cal F}'$ | ${\cal F} \cup \{H+1\} $ | $[1,H+1]$ | $t$ |  |
| $M'$ | $M \cup \{0\} $ | $[0,N]$ | $i,j$ | Supplier:$M_{0}$ |

### Constant
| Constant | Description | Type | Range | Remark |
| - | - | - | - | - |
| $N$ | The number of customers | int | $[1,\infty]$ |  |
| $H$ | Total time | int | $[1,\infty]$ |  |
| $C$ | The capacity of the car | int | $[1,\infty]$ |  |
| $c_{ij}$ | The cost of traveling from customer $i$ to customer $j$ | int | $[1,\infty]$ | $i,j\in M'$ $c_{ij}=c_{ji}$ |
| $r_{0t}$ | The unit produce at time $t$ at the supplier | int | $[1,\infty]$ | $t\in\cal F$ |
| $B_{0}$ | The initial inventory level at the supplier  | int | $(0, \infty]$ |        |
| $h_{0}$ | The unit inventory cost at the supplier  | int | $(0, \infty]$ |        |
| $r_{it}$ | The unit consumption at time $t$ at customer$i$ | int | $[1,\infty]$ | $i\in M$ $t\in\cal F$ |
| $U_{i}$ | The maximum capacity of the inventory at customer $i$ | int | $(0,\infty]$ | $i\in M$ |
| $I_{i0}$ | The initial inventory level of the inventory at customer $i$ | int | $(0,\infty]$ | $i\in M$ |
| $h_{i}$ | The unit inventory cost at customer $i$ | int | $(0,\infty]$ | $i\in M$ |

## Decision
| Variable | Description | Type | Domain | Remark |
| - | - | - | - | - |
| $F_{it}$ | Whether customer $i$ is visited at time $t$ | bool | $\{0,1\}$ | $0$ for not visited $1$ for visited |
| $x_{it}$ | The number of goods delivered to customer $i$ when customer $i$ is visited at time $t$ | int | $(0,\infty)$ |  |
| $y_{ij}^t$ | Whether the car passed by the road between customer $i$ and customer $j$ | bool | $\{0,1\}$ | $0$ for not passedby $1$ for passed by |

### Convention and Function
- Indicate the inventory level at time $t$ at the supplier
$B_{t}=B_{0}+\sum_{t=0}^{t}r_{0t}-\sum_{i\in M}\sum_{t=0}^{t}x_{it}F_{it}$

- Indicate the inventory level at time $t$ at the customer $i$
$I_{it}=I_{i0}-\sum_{t=0}^{t}r_{it}+\sum_{t=0}^{t}x_{it}F_{it}$

## Objective
$min(\sum_{t{\in {\cal F'}}}h_{0}B_{t}+\sum_{i\in M}\sum_{t\in {\cal F}'}h_{i}I_{it}+\sum_{i\in M'}\sum_{j\in M',i\neq j}\sum_{t\in {\cal F}}c_{ij}y_{ij}^t)$

## Constraint
$B_{t}\geq 0, I_{it}\geq 0,I_{it}\leq U_{i}, t\in{\cal F'}, i\in M$
$\sum_{i\in M}\sum_{t\in {\cal F}}x_{it}F_{it}\leq C$