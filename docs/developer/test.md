
## code syntax highlighting for .ini incorrect { data-search-exclude }

Ini Example 1:

```ini
video_mode=8 ; Number 8 - 1920x1080 - 60hz - 16:9 - FHD 1080p
```

Ini Example 2:

```ini
video_mode=8 # Number 8 - 1920x1080 - 60hz - 16:9 - FHD 1080p
```

Ini Example 3:

```ini
; Number 8 - 1920x1080 - 60hz - 16:9 - FHD 1080p
# Number 8 - 1920x1080 - 60hz - 16:9 - FHD 1080p
video_mode=8
```

Verilog Example 1:

```sv
module playfield
(
    input         clk,     // Master clock
    input         reset,   // System reset
    input logic   clkp,    // Pixel Clock
    input clock_t hclk,    // Horizontal clock phase 2
    input         reflect, // Control playfield, 1 makes right half mirror image
    input         cnt,     // center signal, high means right half
    input         rhb,     // Reset HBlank signal
    input [19:0]  pfc,     // Combined playfield registers
    output logic  pf       // Playfield graphics
);
```

When the comment is inside the same line as the code and it is an ini language file, the comment signifier (either `;` or `#` for ini files) is ignored.
