Optimized tool selection**Title**
- **Project**: Simple Caesar cipher cracking lab

**Description**
- **Summary**: Interactive UART program that reads a user string (terminated by `.`) and prints all 25 candidate decodings of the Caesar cipher.

**Learning Objectives**
- **Concepts**: Understand Caesar cipher encoding/decoding and brute-force key search.
- **Embedded skills**: UART I/O with HAL, safe string handling, basic C on STM32.

**Files**
- **Main logic**: main.c
- **Peripherals**: HAL setup in `MX_USART2_UART_Init()` and `_write()` for `printf`.

**Build & Flash**
- **Build**: Use the existing CMake project and your normal toolchain (e.g., `make` from the build folder or your IDE).
- **Flash**: Use your usual STM32 programmer (ST-Link, etc.).

**Usage**
- **Run**: Open a serial console at `115200 8N1` to the board's UART2.
- **Input**: Type the message and finish with a period `.` (the period is not included in decoding).
- **Output**: Program prints `Shift N: <candidate>` lines for shifts 1..25.

**Implementation Notes (Part 2: Decode)**
- **Outer loop**: iterates `shift` from `1` to `25`, producing each candidate plaintext.
- **Per-character**: non-letters are copied unchanged; letters are mapped to 0..25 positions (separately for uppercase/lowercase).
- **Decoding math**: reversed by subtracting the `shift` from position, then using modulo `26` to wrap-around; result mapped back to ASCII.
- **Termination**: output buffer is null-terminated before printing.

**Example**
- **Input**: `Khoor Zruog.`  
- **Output**: among printed candidates, `Shift 3: Hello World` will appear.

**Possible Improvements**
- **Robustness**: use `isalpha()` from `<ctype.h>` for clarity.
- **Clarity**: compute `(int)position - (int)shift + 26) % 26` to avoid unsigned-underflow reliance.
- **UX**: print an index or allow `shift = 0` option to show original text.

**Author**
- **Lab**: Philipp Schilk (2023) — adapted for embedded UART exercise.
