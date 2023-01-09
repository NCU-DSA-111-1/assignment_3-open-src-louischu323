# Assignment 3 : Arithmetic Coding VS Huffman Coding

## Compile & Run 

```sh
# Compile
cd assignment_3

## for arithmetic coding:
gcc -o arcd arcd_stream.c arcd.c arcd.h adaptive_model.h adaptive_model.c

## for huffman coding:
gcc -o huffman huffcode.c huffman.c huffman.h 


# Run

##for arithmetic coding:
./arcd -e <testfilename | tee encodingtext
./arcd -d <encodingtext | tee decodingtext

##for huffman coding:
./huffman -i testfilename -o encodingtext -c
./huffman -i encodingtext -o decodingtext -d

```


## Usage

### For test_2, take huffman coding for instance, when insert:
```sh
./huffman -i test_2 -o encodingtext -c
```

### It will show the runtime it takes:
```sh
The runtime is 0.000086 sec.
```

### Insert the following command to decode it:
```sh
./huffman -i encodingtext -o decodingtext -d
```

### Then you can check the decodingtext to see if it's correct.