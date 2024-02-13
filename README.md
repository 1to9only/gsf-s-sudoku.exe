# gsf's sudoku.exe
The source files are obtained from gsf's (Glenn Fowler) [ast-sudoku.2012-08-01](https://github.com/1to9only/ast-sudoku.2012-08-01) package.
## To build using TCC (Tiny C Compiler)
```
tcc.exe -DBBSS=1 -D_TCC=1 sudoku.c subcanon.c sudata.c sudzlib.c
```
## To build using GCC (GNU C Compiler)
```
gcc.exe -flto -s -static -static-libgcc -O3 -march=native -DBBSS=1 -o sudoku.exe sudoku.c subcanon.c sudata.c sudzlib.c
```
## For usage
```
sudoku[64].exe --help
```
## Examples
To generate sudoku grids with same pattern as a given sudoku grid:
```
sudoku.exe -n10 -gto{-3+3}p -euniq()*(1==minimal) -f%v <pattern.txt
output:
6...2...9.5.4...7...7...8...1.5...8.2...9.5.......3.....6.1.2...4.7...3.5.......1
7...6...3.4.8...2...6...7...2.3...4.3...9.5.......1.....5.1.9...8.5...1.9.......2
8...2...3.5.4...6...4...8...4.6...5.3...7.9.......1.....9.4.5...7.3...2.2.......1
3...6...8.7.2...9...1...2...3.7...6.4...2.1.......4.....9.7.8...5.8...3.6.......4
7...6...8.2.3...1...5...6...4.1...2.3...7.4.......9.....7.4.3...1.8...4.6.......9
9...2...8.1.6...7...8...9...6.7...1.2...4.3.......1.....5.7.4...2.5...3.1.......6
6...5...9.3.7...8...2...1...6.4...7.3...6.8.......9.....5.8.9...7.1...5.1.......7
2...7...9.5.4...3...3...1...2.7...1.9...1.6.......9.....7.6.5...9.3...4.1.......2
3...8...7.6.9...1...1...2...5.2...8.2...3.7.......4.....6.2.5...4.5...2.7.......9
7...2...8.4.3...1...6...9...1.4...5.5...3.7.......8.....2.7.4...5.9...8.8.......3
```
For minlex:
```
sudoku.exe -f%#mc puzzles.txt > output.txt

sudoku.exe -f%#mc 45.....6......17..8...............92....7.1..5...36..........58..1..7............
output:
................12..3..4..........56....4.3...1..78........34...2.......19.....8.
```
For solution-minlex:
```
sudoku.exe -f%#.c puzzles.txt > output.txt

sudoku.exe -f%#.c 45.....6......17..8...............92....7.1..5...36..........58..1..7............
output:
.2..5..8....1....6.9..3......1...........297........2....6.4.....6..8..1.........
```
For solution-maxlex [Use the -f%#**N**c option]:
```
sudoku.exe -f%#Nc puzzles.txt > output.txt

sudoku.exe -f%#Nc 45.....6......17..8...............92....7.1..5...36..........58..1..7............
output:
.8..5..2....9....4.1..7......9...........813........8....4.6.....4..2..9.........
```
Solution-maxlex is just renumbering the sudoku-minlex grid using mapping from minlex row 1 (123456789) to maxlex row 1 (987654321).
## sudoku64.exe [only]
For true-minlex [For this I've replaced the subcanon() function with my own minlex() function (source not included)]:
```
sudoku64.exe -f%#mc puzzles.txt > output.txt

sudoku64.exe -f%#mc 45.....6......17..8...............92....7.1..5...36..........58..1..7............
output:
................12..1..3..4.....1.3..5....6...7..4.8......7.......59...7..3......
```
For maxlex [Use the -f%#**M**c option, and I've added my own maxlex() function (source not included)]:
```
sudoku64.exe -f%#Mc puzzles.txt > output.txt

sudoku64.exe -f%#Mc 45.....6......17..8...............92....7.1..5...36..........58..1..7............
output:
98.7.....7..............6..5...4..7...3..6.......2..8...65..3.....1.3............
```
Note: In sudoku.exe, -f%#Mc is same as -f%#mc, i.e. outputs minlex form.
### Comparison
Comparison of time taken to minlex the 49158 17-clues sudokus:
```
gsf.exe         gsf's            3,236 ms

sudoku.exe      tcc compiler     3,868 ms

sudoku.exe      gcc compiler     1,952 ms

sudoku64.exe    true minlex      8,813 ms

```
Time taken to maxlex the 49158 17-clues sudokus:
```
sudoku64.exe    maxlex            25.3 s

```
&nbsp;
