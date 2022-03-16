When overriding gamepad settings inside a core it is possible to define button combinations (e.g. A+B) if you have enough physical buttons.

To allow for this, MiSTer will ask if you want to setup "alternate mappings" after defining a gamepad.

Alternate mappings are active in parallel and allow two kinds of abilities: map two physical button to the same core button (e.g. alternate button for Start), or map one physical button to two-button combo in the core (e.g. map physical X to thr core's A+B).

## Bind core button to two physical buttons

The simplest is to map an extra physical button. Only this additional button needs to be defined in the alternate map, as follows:

| **map** | **d-pad** | **A** | **B** |
|:--------|:---------|:------|:------|
|**main**|_define_|Btn 1|Btn 2|
|**alt**|_skip_|_skip_|Btn 3|

The result of using this setup ia that you will have physical buttons 2 and 3 mapped to the core button B.

This also works with gamepad directions. For example, for games that use Up as a jump button, it is possible to map a physical third button to jump.

## Bind physical button to core button combo

A more advanced setup is to use both mappings in parallel to make one physical button push two core buttons at the same time.

See the table below:

| **map** | **d-pad** | **A** | **B** 
|:--------|:---------|:------|:------|
|**main**|_define_|Btn 1|Btn 3|
|**alt**|_skip_|Btn 3|Btn 2|

The result of this is that Button 1 will be A, Button 2 will be B, and Button 3 will be A+B.

This is particularly useful for the Neogeo core where some fighting games use A+B and C+D as "strong hit".

(note: unfortunately NeoGeo games are not consistent with each other - so it is not possible to set one mapping for all games)

## Example: NeoGeo Breakers / Breakers' Revenge

Assume a six button arcade controller (for Street Fighter 2) with 3 punch buttons on top and 3 kick buttons below.

We will map the buttons so that Breakers / Breakers' revenge has the same kind of layout.

This particular game uses the following attack buttons:
* A: Weak Punch
* B: Weak Kick
* C: Strong Punch
* D: Strong Kick

In addition, most characters have an extra "command" move mapped to:
* Weak Punch + Strong Punch 
* Weak Kick + Strong Kick 

To match the Street Fighter 2 layout, we can assign this across six buttons:

| **-**   | **Weak** | **Strong** | **Weak+Strong** |
|:--------|:---------|:-----------|:----------------|
|**Punch**|    A     |  C         |   A + C         |
|**Kick** |    B     |  D         |   B + D         |

Which translates to the following buttons:

| **-**   | **Weak** | **Strong** | **Weak+Strong** |
|:--------|:---------|:-----------|:----------------|
|**Punch**|Btn 1     |  Btn 2     |   Btn 3         |
|**Kick** |Btn 4     |  Btn 5     |   Btn 6         |

To obtain this, input the following assignment during main and alternate mapping:

| **map** | **d-pad** | **A** | **B** | **C** | **D** |
|:--------|:----------|:------|:------|:------|:------|
|**main** |_define_   | Btn 1 | Btn 4 | Btn 3 | Btn 6 |
|**alt**  |_skip_     | Btn 3 | Btn 6 | Btn 2 | Btn 5 |

(in alternate mapping, d-pad and all other buttons can be skipped)

## Example: NeoGeo King of Fighters / Fatal Fury Special

Both of these game use the same attack layout as Breakers but their button combination differs:

| **-**   | **Weak** | **Strong** | **Combo**       |
|:--------|:---------|:-----------|:----------------|
|**Punch**|    A     |  C         |   A + B         |
|**Kick** |    B     |  D         |   C + D         |

To map this, we need to switch things around a little bit:

| **map** | **d-pad** | **A** | **B**   | **C**   | **D** |
|:--------|:----------|:------|:--------|:--------|:------|
|**main** |_define_   | Btn 1 | _Btn 3_ | _Btn 2_ | Btn 6 |
|**alt**  |_skip_     | Btn 3 | _Btn 4_ | _Btn 6_ | Btn 5 |

## Example: NeoGeo Samurai Shodown

This game has yet another layout, changing the order of base attacks:

| **-**   | **Weak** | **Medium** | **Strong**      |
|:--------|:---------|:-----------|:----------------|
|**Slash**|    A     |  B         |   A + B         |
|**Kick** |    C     |  D         |   C + D         |

We can map this as follows:

| **map** | **d-pad** | **A** | **B**   | **C**   | **D** |
|:--------|:----------|:------|:--------|:--------|:------|
|**main** |_define_   | Btn 1 |  Btn 3  | _Btn 4_ | Btn 6 |
|**alt**  |_skip_     | Btn 3 | _Btn 2_ |  Btn 6  | Btn 5 |

## Counter Example: The Last Blade 1 and 2

Very similar to the above but a different button combo:

| **-**   | **Weak** | **Medium** | **Special**     |
|:--------|:---------|:-----------|:----------------|
|**Slash**|    A     |  B         |   _B + C_       |
|**Kick** |    C     |  D         |   C + D         |

In this case, it is not possible to map C three times _so we must choose whether to map B+C or C+D_.

#### Option 1: Mapping B+C to button 3:

| **map** | **d-pad** | **A** | **B**   | **C**   | **D** |
|:--------|:----------|:------|:--------|:--------|:------|
|**main** |_define_   | Btn 1 |  Btn 2  |  Btn 3  | Btn 5 |
|**alt**  |_skip_     | _skip_| Btn 3   |  Btn 4  | _skip_|

(Btn 6 remains unassigned)

#### Option 2: Mapping C+D to button 6:

| **map** | **d-pad** | **A** | **B**   | **C**   | **D** |
|:--------|:----------|:------|:--------|:--------|:------|
|**main** |_define_   | Btn 1 |  Btn 2  |  Btn 6  | Btn 5 |
|**alt**  |_skip_     | _skip_| _skip_  |  Btn 4  | Btn 6|

(Btn 3 remains unassigned)
