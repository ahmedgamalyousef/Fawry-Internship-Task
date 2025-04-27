# Fawry-Internship-Task
## Reflective Section
### 1. How does your script handle arguments and options ?

- I used getopts to parse command-line options (-n, -v) .
- The script sets flags (show_line_numbers and invert_match) based on the options .
- After parsing options, it shifts positional arguments and checks that both a search string and filename are provided .
- It validates if the given file exists .
- Based on the flags, it either shows matching lines normally, shows line numbers, or inverts the match .


### 2. How would the structure change if regex or -i/-c/-l options were added ?

- For regex, I would replace the simple grep check with an extended regex match (grep -E) or shell pattern matching ([[ $line =~ $pattern ]]) .
- For -i (ignore case), the structure would not change because case-insensitive search is already done using grep -i .
- For -c (count matches), I would add a counter variable that increments on each match and print the count at the end .
- For -l (list filenames), I would only print the filename once if there is at least one match instead of printing lines .
- I would modularize the script into small functions to make it easier to maintain when adding more options .

### 3. What part of the script was hardest to implement and why?

- The hardest part was correctly parsing options (-v, -n, combinations like -vn) .
- Ensuring the logic for inverted matches with line numbers was tricky, especially when combining both options .
- Using getopts and shifting positional parameters cleanly also required careful handling to avoid wrong arguments .