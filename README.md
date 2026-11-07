# QR generator

## Complete documentation

[QR Code Model construction guide](docs/QR_CODE_CONSTRUCTION.md) — comprehensive implementation reference, all 40 alignment layouts, 160 ECC configurations, and all BCH format/version words.


<a href="https://flyingzebra.github.io/QR_generator/tools/padding_calculator.html">QR padding calculator</a>



```mermaid


flowchart TB
    subgraph L1["LAYER 1 — Input and segmentation"]
        direction LR
        A["Input text / binary data"]
        B["Mode selection: Numeric, Alphanumeric, Byte, Kanji"]
        C["Mode indicator + character count + payload bits"]
        A --> B --> C
    end

    subgraph L2["LAYER 2 — Data encoding"]
        direction LR
        D["Terminator bits"]
        E["Byte alignment"]
        F["Padding bytes: EC / 11"]
        G["Data codewords"]
        D --> E --> F --> G
    end

    subgraph L3["LAYER 3 — Error correction"]
        direction LR
        H["RS block partitioning"]
        I["Reed–Solomon parity over GF(256)"]
        J["Interleave data and ECC codewords"]
        K["Remainder bits"]
        H --> I --> J --> K
    end

    subgraph L4["LAYER 4 — Structural patterns"]
        direction LR
        P1["Finder\npatterns"]
        P2["Light\nseparators"]
        P3["Timing\npatterns"]
        P4["Alignment\npatterns: 5×5"]
        P5["Reserve metadata positions"]
        P6["Fixed dark module"]
        P1 --> P2 --> P3 --> P4 --> P5 --> P6
    end

    subgraph L5["LAYER 5 — Matrix construction"]
        direction LR
        M1["Reserve all function modules"]
        M2["Place data and ECC bits in zigzag"]
        M3["Place remainder bits"]
        M1 --> M2 --> M3
    end

    subgraph L6["LAYER 6 — Data masking"]
        direction LR
        N1["Apply each of 8 candidate masks"]
        N2["Evaluate penalty rules N1–N4"]
        N3["Select best mask"]
        N1 --> N2 --> N3
    end

    subgraph L7["LAYER 7 — Protected metadata"]
        direction LR
        Q1["Format: ECC level + mask ID"]
        Q2["BCH(15,5) + XOR 0x5412"]
        Q3["Version: BCH(18,6) for versions 7–40"]
        Q4["Write both copies of metadata"]
        Q1 --> Q2 --> Q3 --> Q4
    end

    subgraph L8["LAYER 8 — Final symbol"]
        direction LR
        R1["Completed QR module matrix"]
        R2["Quiet zone: 4 modules on each side"]
        R3["Render SVG / PNG / canvas"]
        R1 --> R2 --> R3
    end

    L1 --> L2
    L2 --> L3
    L3 --> L4
    L4 --> L5
    L5 --> L6
    L6 --> L7
    L7 --> L8

    style L1 fill:#e8f1ff,stroke:#3975c6
    style L2 fill:#e8f1ff,stroke:#3975c6
    style L3 fill:#e7f5ea,stroke:#34834a
    style L4 fill:#fff3e3,stroke:#c88a37
    style L5 fill:#fff3e3,stroke:#c88a37
    style L6 fill:#f1eaff,stroke:#8354b0
    style L7 fill:#f1eaff,stroke:#8354b0
    style L8 fill:#e7f5ea,stroke:#34834a

```





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


