# Week 13 Assignment

2026-11-23

# Assignment

### Purpose

The goal of this assignment is to practice writing and using for loops
for iteration.

### Task

Write R code to successfully answer each question below.

### Criteria for Success

- Code is within the provided code chunks or new code chunks are created
  where necessary
- Code chunks run without errors
- Code chunks have brief comments indicating which code is answering
  which part of the question
- Code will be assessed as follows:
  - Produces the correct answer using the requested approach: 100%
  - Generally uses the right approach, but a minor mistake results in an
    incorrect answer: 90%
  - Attempts to solve the problem and makes some progress using the core
    concept, but returns the wrong answer and does not demonstrate
    comfort with the core concept: 50%
  - Answer demonstrates a lack of understanding of the core concept: 0%
- Any questions requiring written answers are answered with sufficient
  detail

### Due Date

Nov 24 before class

# Assignment Exercises

### Set Up

Be sure to load the `tidyverse` to use later in the assignment.

``` r
library(tidyverse)
```

    Warning: package 'tidyverse' was built under R version 4.4.3

    Warning: package 'readr' was built under R version 4.4.3

    Warning: package 'stringr' was built under R version 4.4.3

    Warning: package 'forcats' was built under R version 4.4.3

    Warning: package 'lubridate' was built under R version 4.4.3

    ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ✔ dplyr     1.1.4     ✔ readr     2.2.0
    ✔ forcats   1.0.1     ✔ stringr   1.6.0
    ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
    ✔ lubridate 1.9.5     ✔ tidyr     1.3.1
    ✔ purrr     1.0.2     
    ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ✖ dplyr::filter() masks stats::filter()
    ✖ dplyr::lag()    masks stats::lag()
    ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(dplyr)
```

### 1. For Loop Basics (30 pts)

Complete the following tasks.

**HINT!** I recommend copying the commented code and making changes to
the copy. That way, if you have made edits that you haven’t kept track
of, you have the original code to start over as needed.

1.  The code below prints the numbers 1 through 5 one line at a time.
    Modify it to print each of these numbers multiplied by 3.

    ``` r
    #1a
    numbers <- c(1, 2, 3, 4, 5)

    for (numb in numbers){
      numbers <- 3*numb
      print(numbers)
      }
    ```

        [1] 3
        [1] 6
        [1] 9
        [1] 12
        [1] 15

``` r
numbers <- c(1, 2, 3, 4, 5)
# for (number in numbers){
#   print(number)
# }
```

2.  Write a for loop that loops over the following vector and prints out
    the mass in kilograms (`mass_kg = mass_lb / 2.2`)

    ``` r
    #1b
    mass_lbs <- c(2.2, 3.5, 9.6, 1.2)

    for (mass in mass_lbs){
    mass_kg = mass / 2.2
    print(mass_kg)
    }
    ```

        [1] 1
        [1] 1.590909
        [1] 4.363636
        [1] 0.5454545

``` r
mass_lbs <- c(2.2, 3.5, 9.6, 1.2)
```

3.  Complete the code below so that it prints out the name of each bird
    one line at a time.

    ``` r
    #1c
    birds <- c("robin", "woodpecker", "blue jay", "sparrow")
    for (i in 1:length(birds)){
      print(birds[i])
      }
    ```

        [1] "robin"
        [1] "woodpecker"
        [1] "blue jay"
        [1] "sparrow"

``` r
# birds <- c("robin", "woodpecker", "blue jay", "sparrow")
# for (i in 1:length(_________)){
#   print(birds[__])
# }
```

4.  Complete the code below so that it stores one area for each radius.

    ``` r
    #1d
    radius <- c(1.3, 2.1, 3.5)
    areas <- vector(mode = "numeric",
                    length = length (radius))
    for (i in 1:length(radius)){
      areas[i] <- pi * radius[i] ^ 2
    }
    areas
    ```

        [1]  5.309292 13.854424 38.484510

``` r
radius <- c(1.3, 2.1, 3.5)
# areas <- vector(_____ = "numeric", length = ______)
# for (__ in 1:length(________)){
#   areas[__] <- pi * radius[i] ^ 2
# }
# areas
```

5.  Complete the code below to calculate an area for each pair of
    `lengths` and `widths`, store the areas in a vector, and after they
    are all calculated print them out:

    ``` r
    #1e
    lengths <- c(1.1, 2.2, 1.6)
    widths <- c(3.5, 2.4, 2.8)
    areas <- vector( mode = "numeric",
                     length = length (lengths))
    for (i in 1:length(lengths)) {
      areas[i] <- lengths[i] * widths[i]
      }
    areas
    ```

        [1] 3.85 5.28 4.48

``` r
lengths <- c(1.1, 2.2, 1.6)
widths <- c(3.5, 2.4, 2.8)
# areas <- vector(length = __________)
# for (i in _____) {
#   areas[__] <- lengths[__] * widths[__]
# }
# areas
```

### 2. Size Estimates by Name (30 pts)

This is a followup to “Size Estimates by Name” from last week.

Download the `dinosaur_lengths.csv` file from D2L and place it in the
correct directory. Read the file into R.

``` r
dinosaur_lengths <- read.csv("../raw_data/dinosaur_lengths.csv")
head(dinosaur_lengths)
```

           species  lengths
    1  Stegosauria 18.52588
    2 Ankylosauria 16.43598
    3 Ankylosauria 23.73421
    4    Sauropoda 23.93411
    5 Ankylosauria 21.68718
    6 Ankylosauria 21.38363

Write a function `mass_from_length()` that uses the equation
`mass <- a * length^b` to estimate the size of a dinosaur from its
length. This function should take two arguments, `length` and `species`.
For each of the following inputs for `species`, so use the associated
`a` and `b` values to estimate the species mass using these equations:

- *Stegosauria*: `mass = 10.95 * length ^ 2.64` ([Seebacher
  2001](http://www.jstor.org/stable/4524171)).
- *Theropoda*: `mass = 0.73 * length ^ 3.63` ([Seebacher
  2001](http://www.jstor.org/stable/4524171)).
- *Sauropoda*: `mass = 214.44 * length ^ 1.46` ([Seebacher
  2001](http://www.jstor.org/stable/4524171)).
- For any other value of `species`: `mass = 25.37 * length ^ 2.49`

1.  Use this function and a `for` loop to calculate the estimated mass
    for each dinosaur, store the masses in a vector, and after all of
    the calculations are complete show the first few items in the vector
    using `head()`.

2.  Add the results in the vector back to the original data frame. Show
    the first few rows of the data frame using `head()`.

    ``` r
    #2a/2b
    masss <-  function(lengths, species){
      if (species == "Stegosauria") {
        mass <-  10.95 * lengths ^ 2.64
      } else if (species == "Theropoda"){
        mass <-  0.73 * lengths ^ 3.63
      } else if (species == "Sauropoda"){
        mass = 214.44 * lengths ^ 1.46
      } else {
        mass = 25.37 * lengths ^ 2.49
      }
      return (mass)
    }
    masses <- vector(mode= "numeric",
                     length= nrow(dinosaur_lengths))
    for(i in 1:nrow(dinosaur_lengths)) {
      masses[i] <- masss(lengths= dinosaur_lengths$lengths[i],
                         species = dinosaur_lengths$species[i])
    }

    dinosaur_lengths <- dinosaur_lengths |> 
      mutate(mass = masses)

    head(dinosaur_lengths)
    ```

               species  lengths     mass
        1  Stegosauria 18.52588 24341.68
        2 Ankylosauria 16.43598 27017.90
        3 Ankylosauria 23.73421 67453.38
        4    Sauropoda 23.93411 22114.19
        5 Ankylosauria 21.68718 53884.76
        6 Ankylosauria 21.38363 52026.34

3.  Calculate the mean mass for each `species` using `dplyr` (no `for`
    loops).

    ``` r
    dinosaur_lengths |> 
      group_by(species) |> 
      summarize(
        mean_mass=mean(mass)
      )
    ```

        # A tibble: 4 × 2
          species      mean_mass
          <chr>            <dbl>
        1 Ankylosauria    46819.
        2 Sauropoda       16104.
        3 Stegosauria     31924.
        4 Theropoda       45572.

### 3. Multi-file Analysis (20 pts)

You have satellite collars on a number of different individuals and want
to be able to quickly look at all of their recent movements at once. The
data is posted daily to a URL that contains one csv file for each
individual: [zip
file](http://www.datacarpentry.org/semester-biology/data/individual_collar_data.zip)

Start your solution by:

- Download the zip file from the link above. Place the zip file in the
  appropriate sub-directory, if you have them.

- Unzip it using the `unzip()` function

- Obtain a list of all of the files with file names matching the pattern
  `"collar-data-.*.txt"` (using `list.files()`)

1.  Use a loop to load each of these files into R and make a line plot
    (using `geom_path()`) for each file with `long` on the `x` axis and
    `lat` on the `y` axis.

    Graphs, like other types of output, won’t display inside a loop
    unless you explicitly display them, so you need put your `ggplot()`
    command inside a `print()` statement. Do this by saving the output
    of the ggplot function as an object and then printing that object.

    Include the name of the file in the graph as the graph title using
    the `labs` function (`labs(title = ...)`).

2.  Add code to the loop to calculate the minimum and maximum latitude
    in the file, and store these values, along with the name of the
    file, in a data frame.

    Show the data frame as output.

``` r
#Setup
unzip(zipfile = "../raw_data/individual_collar_data.zip", exdir = "../raw_data/")

collar_data <-  list.files(path="../raw_data",
                         pattern = "collar-data-.*.txt",
full.names = TRUE)

#create empty data frame
latitude_summ <- data.frame(
  file_name = character(),
  min_lat = numeric(),
  max_lat = numeric()
)

num_files <-  length(collar_data)
for (i in 1: num_files){
  filename <- collar_data[i]
  locations <- read.csv(filename)
collar_plot <- ggplot(locations, aes(x= long, y= lat)) +
  geom_path() +
  labs(title = basename(filename))
print(collar_plot)

#3d
latitude_summ[i, ] <- NA
latitude_summ$file_name[i] <-  filename
latitude_summ$min_lat[i] <-  min(locations$lat, na.rm = TRUE)
latitude_summ$max_lat[i] <-  max(locations$lat, na.rm = TRUE)
}
```

![](Week13_Assignment_files/figure-commonmark/unnamed-chunk-15-1.png)

![](Week13_Assignment_files/figure-commonmark/unnamed-chunk-15-2.png)

![](Week13_Assignment_files/figure-commonmark/unnamed-chunk-15-3.png)

![](Week13_Assignment_files/figure-commonmark/unnamed-chunk-15-4.png)

![](Week13_Assignment_files/figure-commonmark/unnamed-chunk-15-5.png)

![](Week13_Assignment_files/figure-commonmark/unnamed-chunk-15-6.png)

![](Week13_Assignment_files/figure-commonmark/unnamed-chunk-15-7.png)

![](Week13_Assignment_files/figure-commonmark/unnamed-chunk-15-8.png)

![](Week13_Assignment_files/figure-commonmark/unnamed-chunk-15-9.png)

![](Week13_Assignment_files/figure-commonmark/unnamed-chunk-15-10.png)

``` r
latitude_summ
```

                                        file_name  min_lat  max_lat
    1   ../raw_data/collar-data-A1-2016-02-26.txt 25.21080 31.76912
    2   ../raw_data/collar-data-B2-2016-02-26.txt 26.70509 30.89907
    3   ../raw_data/collar-data-C3-2016-02-26.txt 28.86998 33.44421
    4   ../raw_data/collar-data-D4-2016-02-26.txt 21.34315 24.66598
    5   ../raw_data/collar-data-E5-2016-02-26.txt 21.85565 27.54663
    6   ../raw_data/collar-data-F6-2016-02-26.txt 17.90788 25.23623
    7   ../raw_data/collar-data-G7-2016-02-26.txt 27.67120 31.63272
    8   ../raw_data/collar-data-H8-2016-02-26.txt 19.70875 23.25601
    9   ../raw_data/collar-data-I9-2016-02-26.txt 25.70252 28.49172
    10 ../raw_data/collar-data-J10-2016-02-26.txt 24.71200 27.80325

### 4. DNA or RNA (20 points)

This question has you write a function and then use the function in
several different forms of iteration.

1.  Write a function that determines if a sequence of base pairs is DNA,
    RNA, or if it is not possible to tell given the sequence provided.
    RNA has the base Uracil (“u”) instead of the base Thymine (“t”), so
    sequences that contain a “u” are RNA, sequences with a “t” are DNA,
    and sequences with neither are unknown.

    Name the function `dna_or_rna()` and have it take `sequence` as an
    argument. Have the function return one of three outputs: “DNA”,
    “RNA”, or “UNKNOWN”.

    *HINT: Remember our work with character strings and the `stringr`
    package from the `tidyverse` (Week 7)?*

``` r
#4a
dna_or_rna <-  function(sequence) {
  if (str_detect(sequence, "u")) {
    return("RNA")
  } else if (str_detect(sequence, "t")) {
    return("DNA")
  } else{
    return("unknown")
  }
}
```

2.  Use the function to determine the sequence type for the following
    sequences.

``` r
seq1 <- "ttgaatgccttacaactgatcattacacaggcggcatgaagcaaaaatatactgtgaaccaatgcaggcg"
seq2 <- "gauuauuccccacaaagggagugggauuaggagcugcaucauuuacaagagcagaauguuucaaaugcau"
seq3 <- "gaaagcaagaaaaggcaggcgaggaagggaagaagggggggaaacc"
```

``` r
#4b
seq1result <- dna_or_rna(seq1)
seq1result
```

    [1] "DNA"

``` r
seq2result <- dna_or_rna(seq2)
seq2result
```

    [1] "RNA"

``` r
seq3result <- dna_or_rna(seq3)
seq3result
```

    [1] "unknown"

Before tackling the next questions (c-g), run the following code chunk
to create a vector called sequences.

``` r
sequences <- c("ttgaatgccttacaactgatcattacacaggcggcatgaagcaaaaatatactgtgaaccaatgcaggcg",
              "gauuauuccccacaaagggagugggauuaggagcugcaucauuuacaagagcagaauguuucaaaugcau",
              "gaaagcaagaaaaggcaggcgaggaagggaagaagggggggaaacc",
              "guuuccuacaguauuugaugagaaugagagcaccugaucagguggauaaggaagaugaagacu",
              "gauaaggaagaugaagacuuucaggaaucuaauaaaaugcacuccaugaauggauucauguaugggaaucagccggguc")
```

3.  Use the function you wrote and a `for` loop to create a vector of
    sequence types for the values in sequences

    ``` r
    #4c
    sequence_types <- character()
    for (i in 1:length(sequences)) {
      sequence_types[i] <- dna_or_rna(sequences[i])
    }
    sequence_types
    ```

        [1] "DNA"     "RNA"     "unknown" "RNA"     "RNA"    

4.  Use the function and a `for` loop to create a data frame that
    includes a column of sequences and a column of their types.

    ``` r
    #4d
    sequence_summary <- data.frame(
      sequence = character(),
      type = character()
    )

    for (i in 1:length(sequences)) {
      sequence_summary[i, "sequence"] <- sequences[i]
      sequence_summary[i, "type"] <- dna_or_rna(sequences[i])
    }
    sequence_summary
    ```

                                                                                 sequence
        1          ttgaatgccttacaactgatcattacacaggcggcatgaagcaaaaatatactgtgaaccaatgcaggcg
        2          gauuauuccccacaaagggagugggauuaggagcugcaucauuuacaagagcagaauguuucaaaugcau
        3                                  gaaagcaagaaaaggcaggcgaggaagggaagaagggggggaaacc
        4                 guuuccuacaguauuugaugagaaugagagcaccugaucagguggauaaggaagaugaagacu
        5 gauaaggaagaugaagacuuucaggaaucuaauaaaaugcacuccaugaauggauucauguaugggaaucagccggguc
             type
        1     DNA
        2     RNA
        3 unknown
        4     RNA
        5     RNA

5.  This time, instead of using the function, place the `if`-`else`
    portion of your function directly into the `for` loop. Modify the
    code so that it successfully creates the same output as (d) above.
    Remember to “reset” the data frame that will hold the output so it
    is empty before you start your loop.

    ``` r
    #4ewhy
    for (i in 1:length(sequences)) {
      sequence_summary[i, "sequence"] <- sequences[i]
      if(str_detect(sequences[i], "u")){
        sequence_summary[i, "type"] <- "RNA"
      } else if (str_detect(sequences[i], "t")){
        sequence_summary[i, "type"] <-  "DNA"
      } else {
        sequence_summary[i, "type"] <- "unknown"
        }
      }
    sequence_summary
    ```

                                                                                 sequence
        1          ttgaatgccttacaactgatcattacacaggcggcatgaagcaaaaatatactgtgaaccaatgcaggcg
        2          gauuauuccccacaaagggagugggauuaggagcugcaucauuuacaagagcagaauguuucaaaugcau
        3                                  gaaagcaagaaaaggcaggcgaggaagggaagaagggggggaaacc
        4                 guuuccuacaguauuugaugagaaugagagcaccugaucagguggauaaggaagaugaagacu
        5 gauaaggaagaugaagacuuucaggaaucuaauaaaaugcacuccaugaauggauucauguaugggaaucagccggguc
             type
        1     DNA
        2     RNA
        3 unknown
        4     RNA
        5     RNA

6.  OPTIONAL: Use the function and `sapply` to create a vector of
    sequence types for the values in sequences

7.  OPTIONAL: Use the function, and `mutate()` to create a data frame
    that includes a column of sequences and a column of their types.
    First, run the following line of code to turn the sequence vector
    into a dataframe.

``` r
seq_df <- as.data.frame(sequences)
```

## Turning in Your Assignment

As with the last few weeks, you will be submitting your assignment by
submitting the link to your GitHub repository.

**Remember!** You should “Render” your assignments to markdown (.md)
files and push all files, including the `.md` file, to GitHub.
