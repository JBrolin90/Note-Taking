- [Wikipedia](https://en.wikipedia.org/wiki/Roman_numerals)
- I = 1, V = 5, X = 10, L = 50, C = 100, D = 500, M = 1000
- In roman numeral, each symbol carry a value, regardless of position
- The symbols I, X, C & M can be repeated up to three times corresponds to addition. (III = 3 and XX = 20).
- To get 4, 40 and 90, for example, you prepend the next lower symbol (IV = 4, XL = 40 and XC = 90)
- You do not repeat the symbols V, L or D.
- Roman numeral [[Context Free Grammar]]
  Numeral := Thousands ? Hundrefds ? Tens ? Units ?
  Units := I | II | III | IV | V | VI | VII | VIII | IX
  Tens := X | XX | XXX | XL | L | LX | LXX | LXXX | XC
  Hundreds := C | CC | CCC | CD | D | DC | DCC | DCCC| CM
  Thousands := M | MM | MMM
-
- Numeral DIV 1000  [0-3]  -> 
  0 | 
  1 {print("M") } |
  2  {print("MM")
  3  {print("MMM")
- Numeral DIV 1100  [0-9]  -> 
  0 |
  1 {print (C)} |
  2 {print (CC)} |
  3 {print (CCC)} |
  4 {print (CD)} |
  5 {print (D)} |
  6 {print (DC)} |
  7 {print (DCC)} |
  8 {print (DCCC)} |
  9 {print (CD)}
  Numeral DIV 1110  [0-9]  ->