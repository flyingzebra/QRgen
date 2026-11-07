# QR generator

## Complete documentation

[QR Code Model construction guide](docs/QR_CODE_CONSTRUCTION.md) — comprehensive implementation reference, all 40 alignment layouts, 160 ECC configurations, and all BCH format/version words.


<a href="https://flyingzebra.github.io/QRgen/tools/padding_calculator.html">QR padding calculator</a>



![Eight-stage QR encoder pipeline](docs/assets/qr-encoding-pipeline.svg)



https://www.thonky.com/qr-code-tutorial/format-version-information



# reed-solomon

k = unencoded message length  
n = encoded message length  
m = symbol size in bits  
d = hamming distance  
t = number of correctable symbols

d = ![](https://latex.codecogs.com/svg.image?2t+1)

t = ![](https://latex.codecogs.com/gif.image?\dpi{110}&space;\left&space;\lfloor&space;\frac{d-1}{2}&space;\right&space;\rfloor)
= ![](https://latex.codecogs.com/svg.image?\frac{n-k}{2})

cylclic codes = any circular bit-shif of a codeword is another valid codeword  
liner codes = any sum of two valid codewords is is another valid codeword  

cyclic codes are represented as polynomials, and for the calculations we need to do, we start with writing the message as a polynomial.

example message:  
1011 = ![](https://latex.codecogs.com/gif.image?\dpi{110}&space;1x^0&space;&plus;&space;0x^1&space;&plus;&space;1x^2&space;&plus;&space;1x^3)  
= ![](https://latex.codecogs.com/gif.image?\dpi{110}&space;1&space;&plus;&space;x^2&space;&plus;&space;x^3)

convertion from message space to codeword space is achieved by:  
**multiplying** the message polynomial by a special **generator polynomial**

# BCH

online BCH code generator
http://www.ece.unb.ca/cgi-bin/tervo/bch.pl

# QR code calculation

https://www.thonky.com/qr-code-tutorial/format-version-information

---

https://latex.codecogs.com


