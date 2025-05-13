SimpleLang TAC Compiler
======================

Project Overview
---------------
This project develops a compiler frontend for SimpleLang, a lightweight C-like language with Italian-inspired keywords like `stampa` (print), `se` (if), and `altrimenti` (else). Built with Flex for lexical analysis and Bison for parsing, it translates SimpleLang code into Three Address Code (TAC), stored in `output.txt`. The compiler showcases key concepts of compiler design, including tokenization, syntax analysis, and intermediate code generation.

Members
-------
- Shubham Pathak (En No: 22001011)
- Bhuvan Rathod (En No: 22000994)

Project Files
-------------
- `lexer.l`: Defines token patterns for Italian keywords and supports accented characters.
- `parser.y`: Specifies the grammar and TAC generation logic.
- `input.it`: Sample input file containing SimpleLang code.
- `Makefile`: Automates the build process.
- `compiler.exe`: Executable generated after compilation.

Setup and Execution
-------------------
### Requirements
- **Tools**: Flex, Bison, GCC.
- **Environment**: Windows 11 with MSYS2 (preferred) or Command Prompt with MinGW.
  - Install MSYS2: https://www.msys2.org/
  - Install dependencies:
    ```
    pacman -S mingw-w64-x86_64-gcc make flex bison
    ```
  - Add `C:\msys64\mingw64\bin` to your system PATH.

### Build Instructions
1. Navigate to the project directory in a terminal (MSYS2 or Command Prompt):
   ```
   cd D:\6th sem\cd\project
   ```
2. Build using the Makefile:
   ```
   make
   ```
   Or manually:
   ```
   flex lexer.l
   bison -d parser.y
   gcc -o compiler lex.yy.c parser.tab.c
   ```
   If linker errors occur, try:
   ```
   gcc -o compiler lex.yy.c parser.tab.c -lfl
   ```

### Running the Compiler
1. Create an input file (`input.it`) with SimpleLang code. Example:
   ```
   se (x < 0) {
       stampa "negative";
   }altrimenti se (x == 0){
       stampa "zero";
   }
   altrimenti {
       stampa "positive";
   }
   ```
2. Run the compiler:
   ```
   ./compiler.exe input.it output.txt
   ```
   Or in Command Prompt:
   ```
   compiler.exe input.it output.txt
   ```
3. View the generated TAC:
   ```
   cat output.txt
   ```
   Or in Command Prompt:
   ```
   type output.txt
   ```

Important Notes
---------------
- **Syntax**: Use Italian keywords (`stampa`, `se`, `altrimenti`) as defined in `lexer.l`. Ensure proper braces and semicolons in `input.sl`.
- **Encoding**: Set your terminal and text editor to UTF-8 to handle accented characters (e.g., é, à).
- **Debugging**: If `output.txt` is not generated, verify `input.it` syntax and check for parse errors in the terminal (e.g., "Error: syntax error"). Ensure the correct command is used:
  ```
  ./compiler.exe input.sl output.tac
  ```
- **Build Issues**: If `make` fails, use the manual build commands. Confirm MSYS2 tools are accessible in PATH.

Sample Execution
----------------
**Input (`input.it`)**
```
se (x < 0) {
    stampa "negative";
}altrimenti se (x == 0){
    stampa "zero";
}
altrimenti {
    stampa "positive";
}
```

**Output (`output.txt`)**
```
ifFalse x < 0 goto L0
print "negative"
goto L1
L0:
ifFalse x == 0 goto L2
print "zero"
goto L1
L2:
print "positive"
L1:
```

The TAC is generated in `output.txt`, adhering to a three-address code format with up to three operands per instruction.
