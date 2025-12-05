# Class 6: R Functions
Alexandra Garcia (PID: A16278166)

- [Our first (silly) function](#our-first-silly-function)
- [A second function](#a-second-function)
- [A protein generating function](#a-protein-generating-function)

All functions in R have at least 3 things:

- A **name**, we pick this and use it to call our function
- Input **arguments**, (there can be multiple)
- The **body**, lines of R code that tod the work

## Our first (silly) function

Write a function to add some numbers

``` r
add <- function(x, y=1) {
  x + y
}
```

Now we can call this function:

``` r
add(10, 100)
```

    [1] 110

``` r
add(c(10,10), 100)
```

    [1] 110 110

\< You can have arguments with a default value by setting the value with
=

## A second function

Write a function to generate random nucleotide sequences of a user
defined length:

The `sample()` function can be useful here.

``` r
v <- sample(c("A", "C", "G", "T"), size=50, replace=TRUE)
paste(v, collapse="")
```

    [1] "AGGAAGGGGAGCTAGGTCCTTTCGGCGTCGGATACGGATTCATGACAACT"

Turned this into my first function:

``` r
generate_dna <- function(size=50) {
  v <- sample(c("A", "C", "G", "T"), size=size, replace=TRUE)
  paste(v, collapse="")
}
```

Test it:

``` r
generate_dna(6)
```

    [1] "GCAAAA"

Add the ability to return a multi-element vector or a single element
fasta like vector.

``` r
fasta = TRUE
if(fasta) {
  cat("Hello")
} else{
  cat("Bye")
}
```

    Hello

``` r
generate_fasta <- function(size=50, fasta=TRUE) {
  v <- sample(c("A", "C", "G", "T"), size=size, replace=TRUE)
  s <- paste(v, collapse ="")
  
  if(fasta) {
    return(s)
  } else{
    return(v)
  }
}
```

``` r
generate_fasta(10, fasta=TRUE)
```

    [1] "ATACAGGGGG"

## A protein generating function

So you have to make amino acids

``` r
generate_protein <- function(size=50, fasta=TRUE) {
  aa <- c("A", "R", "N", "D", "C", "Q", "E", "G", "H", "I", "L", "K", "M", "F", "P", "S", "T", "W", "Y", "V")
  v <- sample(aa, size=size, replace=TRUE)
  s <- paste(v, collapse ="")
  
  if(fasta) {
    return(s)
  } else{
    return(v)
  }
}
```

``` r
generate_protein(6)
```

    [1] "RQIQCN"

Use our new `generate_protein()` function to make random protein
sequences of length 6 to 12 (i.e. one length 6, length 7, up to length)

One way to do it is brute force

``` r
generate_protein(6)
```

    [1] "RCDHSD"

``` r
generate_protein(7)
```

    [1] "RKGCQFS"

A second way to do it is to use a `for()` loop:

``` r
lengths <- 6:12
lengths
```

    [1]  6  7  8  9 10 11 12

``` r
for(i in lengths) {
  cat(">", i, "\n", sep="")
  sq <- generate_protein(i)
  cat(sq)
  cat(sq, "\n")
}
```

    >6
    LNCEGKLNCEGK 
    >7
    ALAHFTKALAHFTK 
    >8
    NVAFWWMLNVAFWWML 
    >9
    KLSEYCGYSKLSEYCGYS 
    >10
    KVLMIASYAEKVLMIASYAE 
    >11
    YHVQCYYYEESYHVQCYYYEES 
    >12
    LMLYFGYCGVSDLMLYFGYCGVSD 

A third, and better, way to solve this is to use the `apply()` family of
functions, specifically the `sapply()` function in this case.

``` r
sapply(6:12, generate_protein)
```

    [1] "WRNAPI"       "PRINVIT"      "SVMRPPYT"     "IIGGCDHTS"    "MMFKAPYIWE"  
    [6] "EKNSTIEDHYR"  "PAYHPQFYSVMK"
