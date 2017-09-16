# ParallelDebugging
![Travis](https://img.shields.io/travis/rust-lang/rust.svg)

This project provides some representative algorithms in parallel debugging，including Block Diagonal Matrix (BDM), Jones II, Weil-Kettler (hor. W-K, vert. W-K), and Maximum Set Packing(MSP). The first 5 algorithms are implemented by [Hogerle et al.](http://www.feu.de/ps/prjs/PD/). Cite their paper as follows, 

<blockquote>Hogerle, Wolfgang, F. Steimann, and M. Frenkel. "More Debugging in Parallel." IEEE, International Symposium on Software Reliability Engineering IEEE Computer Society, 2014:133-143.</blockquote>

In addition, we fix some bugs in their Java code and also develop our own partitionning algorithms in parallel debugging, namely XXX. To compare the performances among those algorithms we design the contrast experiments which are also contained in our projects. 

### BDM
BDM is the basic partitioning algorithms among the above 5 algorithms, whose idea is quite simple. It divide the FCM into multiple <strong><em>block diagnoal matrixs</em></strong> whose rows and coloums can not be overlapped. Using BDM in our project is quite simple, you just need to call the static method <code>getBlocks()</code> in class <code>BDM</code>,

```java
Result input = MatrixDataReader.getTestsAndUUTsFromFile("path/to/your/file");
Set<Set<Test>> setTests = BDM.getBlocks(input);
```

### Jones II

Jones II is the second algorithom proposed by Jones et al. Jones II is a cluster-based partitioning algorithm, it has two main steps in test cases clustering:
- Constructing multiple test suites consisting of each single failed test cases and all passed test cases, 
- clustering these test suites according to the similarity of susipicious ranking list obtainted by fault localization technique (i.e., Tanrantula) in each suites. 

Using Jones II is also quite easy you only need to call the function <code>getBlocks()</code> in class <code>Jones</code>, 

```java
Result input = MatrixDataReader.getTestsAndUUTsFromFile("path/to/your/file");
Jones jones = new Jones();
Set<Set<Test>> setTests1 = jones.getBlocks(input); // use default parameters
Set<Set<Test>> setTests2 = jones.getBlocks(input, 0.2, 0.5); // specify your own parameters if you want
```

### W-K

### MSP
