# Assignment 1 – Advanced Operating Systems

## Q1: File Reversal with Multiple Modes

### Execution Instructions
``` bash 
# Compile
g++ Q1.cpp

# Run for block-wise reversal (Flag 0)
./a.out <input_file> 0 <block_size>

# Run for full file reversal (Flag 1)
./a.out <input_file> 1

# Run for partial range reversal (Flag 2)
./a.out <input_file> 2 <start_index> <end_index>
```

### Code Overflow

1.  Argument Parsing
    Reads command-line arguments and validates them based on the selected flag.

2.  Directory Creation
    Creates a directory Assignment1/ with permission 700 using mkdir().

3.  File Opening
    Opens input file in read-only mode and output file in read-write mode with permission 600.

4.  Reversal Logic

    Flag 0: Read the file in block_size chunks, reverse each chunk, and write them in the same block order.

    Flag 1: Read from the end of the file in chunks, reverse each chunk, and write sequentially.

    Flag 2: Reverse bytes before start_index and after end_index, keep the middle section unchanged.

5.  Progress Display
    Shows percentage progress in the terminal using \r to overwrite the same line.

6.  Close Files
    Closes all file descriptors with close().


## Q2: File and Permission Verification

``` bash 
# Compile
g++ Q2.cpp

# Run for block-wise reversal (Flag 0)
./a.out <newfile> <oldfile> <directory> 0 <blocksize>

# Run for full file reversal (Flag 1)
./a.out <newfile> <oldfile> <directory> 1

# Run for partial range reversal (Flag 2)
./a.out <newfile> <oldfile> <directory> 2 <start> <end>
```

### Code Overflow

1.  Argument Parsing
    Reads inputs and determines verification type based on the flag.

2.  Permission Checks

    - Uses stat() to get permission bits.

    - Verifies:

        - Directory: 700

        - New file: 600

        - Original file: 644

    - Prints Yes/No for each permission bit:

        - User Read/Write/Execute

        - Group Read/Write/Execute

        - Others Read/Write/Execute

3.  File Size Check
    Compares sizes of the new file and original file.

4.  Content Verification

    - Flag 0: Reads both files block-by-block, checks if blocks are reversed correctly.

    - Flag 1: Reads original from start and new file from end, compares reversed data.

    - Flag 2:

        - Verifies first section is reversed.

        - Verifies middle section is identical.

        - Verifies last section is reversed.

5.  Result Output
    Prints results for:

        - Directory creation

        - Content correctness

        - File size match

        - All permission checks for directory, old file, and new file.