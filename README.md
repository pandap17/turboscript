# TurboScript Documentation

TurboScript, also known as TS, is a scripting language designed to be executed within Scratch projects during runtime. This documentation provides an overview of TurboScript syntax and functionality.

## Simple Hello World

```
return str "Hello world!" to var helloWorld;
```

## Important Notes

- At the end of EVERY line in TurboScript, you MUST add a semicolon (`;`). It acts as a way to tell the compiler, "hey, this line of code is finished, let's go to the next one!"
- TurboScript has extension dependencies. This unfortunately makes it only compatible with modified Scratch versions, and as such, TurboScript is not compatible with vanilla Scratch.

## Technical Details

When TurboScript code is executed during runtime, it first converts all lines of code to a JSON array with the delimiter `;` (hence the need for the semicolon at the end of each line). Then, for each individual line of code in the array, the compiler creates an array based on the line of code using whitespace as the delimiter. This breaks down the line of code into its individual words in a JSON array, allowing the compiler to read specific items at specific positions in the line of code.

Once the compiler has processed the code line by line, it calls the "operation" script. The operation script contains and executes the Scratch code equivalents for every TurboScript function. The operation script works linearly, meaning it goes through the entire script, checking if the compiler can find a function at item 1 of the line of code that matches any of the functions within the "Operation" script. If a match is found, it executes the corresponding Scratch code and stops the operation script. If no match is found, an error is returned to the list `tsErrors` like this:

```
"Item" in line x was not found to be a valid function by the TurboScript compiler.
```

This process is repeated for each line of code in the array created with the semicolon delimiter, which contains all the lines of code.
