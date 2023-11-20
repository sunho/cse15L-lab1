# Part 1


Fail 
```java
@Test
public void testReverseInPlace() {
  int[] input1 = { 1, 3 };
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[] { 3, 1 }, input1);
}
```

No fail
```java
@Test
public void testReverseInPlace() {
  int[] input1 = { 1 };
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[] { 1 }, input1);
}
```
Symptom: Array \[1, 3\] is not properly reversed as \[3, 1\]
![fa](./images/test_fail.png)

Bug: The code is overwriting the array before when the element is needed.
Fix: Swap elements instead of overwriting

Before 
```java
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

After
```java
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int tmp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = tmp;
    }
  }
```

This fixes the bug since now it doesn't overwrite the first element before it is needed; it's swapped to the correct place now.

## Part 2

All descriptions of command line option were from man grep.

**grep -r:** performs recursive search on the directory specified.

It can be useful when you want to find files with specific content.

```bash
❯ grep -r "microsatellites"
./technical/biomed/ar319.txt:        microsatellites. This should facilitate the identification
./technical/biomed/ar319.txt:          genotype data from the 11 microsatellites used in the
./technical/biomed/gb-2001-2-11-research0046.txt:            differ from those of many microsatellites reported in
./technical/biomed/gb-2001-2-11-research0046.txt:            primers used to amplify these microsatellites (except 
./technical/biomed/gb-2001-2-11-research0046.txt:          microsatellites. We can estimate the density of the
./technical/biomed/gb-2001-2-11-research0046.txt:          is appropriate for mapping SNPs, microsatellites and
./technical/biomed/1471-2229-3-3.txt:        DNA was highly enriched for microsatellites, with
./technical/biomed/1471-2229-3-3.txt:        microsatellites present in peanut [ 20 21 ] ,
./technical/biomed/1471-2229-3-3.txt:        microsatellites have not been fully identified, developed
./technical/biomed/1471-2229-3-3.txt:        microsatellites still remains blank.
./technical/biomed/1471-2229-3-3.txt:        microsatellites from the cultivated peanut genome; and (2)
./technical/biomed/1471-2229-3-3.txt:        microsatellites in a collection of peanut accessions with
./technical/biomed/1471-2229-3-3.txt:        microsatellites in peanut.
./technical/biomed/1471-2229-3-3.txt:        development of microsatellites through this study. When the
./technical/biomed/1471-2229-3-3.txt:        microsatellites after cloning and sequencing. In order to
./technical/biomed/1471-2229-3-3.txt:        are the most abundant microsatellites in peanut genome.
./technical/biomed/1471-2229-3-3.txt:        peanut microsatellites [ 21 ] , in which five polymorphic
./technical/biomed/1471-2229-3-3.txt:        development of microsatellites in peanut. Therefore, a
./technical/biomed/1471-2105-3-30.txt:          microsatellites can score high, but tend not to be
./technical/biomed/1471-2105-3-30.txt:          Tandem Repeat Remover [ 17 ] to mask microsatellites,
./technical/biomed/1471-2105-3-30.txt:          did not detect appreciable microsatellites in random
./technical/biomed/1471-2164-4-6.txt:        repeat polymorphisms (STRPs) (also called microsatellites
./technical/biomed/1471-2164-2-1.txt:          (VNTRs/ microsatellites) found in the gene. The G/C
./technical/biomed/gb-2002-3-10-research0052.txt:        for the creation of microsatellites through
./technical/biomed/gb-2002-3-10-research0052.txt:        poly(A) tail to microsatellites.
```

```bash
~/dev/docsearch main*
❯ grep -r "transbronchial"  
./technical/plos/pmed.0020073.txt:            lung lesion, and pleural fluid. However, re-review of the original transbronchial
./technical/plos/pmed.0020073.txt:          transbronchial biopsy, and a nearly 5:1 ratio in the pleural fluid (Figure 2A). Notably,
./technical/plos/pmed.0020073.txt:          we did not detect the 2573 T→G mutation in the original transbronchial biopsy specimen
./technical/biomed/rr166.txt:          transbronchial lung biopsies at the time of diagnosis. Of

**grep -v:** find all lines that does not include specified word.

Can be useful if you don\'t like certain words and find phrases that does not include it.

```bash
❯ grep -v "a" ./technical/plos/pmed.0010008.txt

  
    
      
        Introduction
        within the lung [14].
        IP-10.
      
      
        Methods
        
        
        
        
        
        
        
          Antibodies
        
        
          were resuspended to 1 × 10
```
```bash
❯ grep -v "The" ./technical/plos/pmed.0010008.txt

  
    
      
        Introduction
        Chronic inhalation of tobacco smoke causes progressive lung destruction in susceptible
        individuals, resulting in chronic obstructive pulmonary disease (COPD) and emphysema, two
        well-described clinical syndromes with poorly understood pathogenesis [1,2,3]. A role for T
        helper cells in the pathogenesis of obstructive lung disease has been established with
        asthma, where T helper 2 (Th2) cells are strongly linked to both human and experimental
        disease [4,5,6,7]. A potential role for T cells in COPD has also been suggested in several
        recent studies that show CD8
        + T cells are increased in the lungs of people who smoke [8,9,10,11]. T
        cells cause tissue injury through their secreted products such as cytokines; in mice,
```

**grep -i:** perform case-insensitive search.

Can be useful when you want to match more texts by case-insensitiveness.
```bash
❯ grep -i "the" ./technical/plos/pmed.0010008.txt          
        helper cells in the pathogenesis of obstructive lung disease has been established with
        + t cells are increased in the lungs of people who smoke [8,9,10,11]. t
        cells cause tissue injury through their secreted products such as cytokines; in mice,
        overexpression of interleukin (il)-13, a t cell cytokine that is strongly implicated in the
        enlargement of airspaces reminiscent of emphysema [12]. further, airway limitation, another
        function in smoker individuals [13]. it has been suggested, therefore, that asthma and copd
        may involve the same type of recruited inflammatory cells, differing only in their location
        within the lung [14].
        chemokines, their receptors, and cell adhesion molecules regulate migration of immune
        expression [26]. in addition to t cells, a wide variety of other inflammatory cells have
        been shown to express distinct chemokine receptors that are critical for their homing,
        injured epithelial cells and t cells that are required for homing of th1 cells [27,28,29].
        in addition to regulation of chemotaxis and homing, other functions have been ascribed to
        in this study we determined the dominant t helper phenotype in lung samples from
        both cd4 and cd8 t helper cells are strongly polarized to the th1 phenotype compared to t
        non-smoking-related obstructive lung disease. the same cells spontaneously secreted more
        ifn-γ and cxcr3 receptor ligands mig and ip-10 in the copd and emphysema group than in the
        group without emphysema. further, ip-10 and mig, but not ifn-γ, upregulated macrophage
        together, our findings reveal the strong association between copd/emphysema- and th1-driven
          necessary lung resection were serially entered into the study: ten individuals with no
          in copd/emphysema and control groups, respectively. copd was diagnosed according to the
          criteria recommended by the national institutes of health/world health organization
          workshop summary [31]. participants in the control and copd/emphysema groups had similar
```

```bash
❯ grep -i "loc" ./technical/plos/pmed.0010008.txt
        may involve the same type of recruited inflammatory cells, differing only in their location
          presence or absence of blocking anti-CXCR3 antibodies (5 μg/ml, R&D Systems).
          the immunohistochemical localization of this chemokine receptor that CD14
          interaction because in the presence of a CXCR3 function-blocking antibody, IP-10 failed

**grep -c:** count number of matching lines.

Can be useful if you want to count lines of code.

```bash
❯ grep -c "the" ./technical/plos/pmed.0010008.txt
124
```

```bash
❯ grep -c "either" ./technical/plos/pmed.0010008.txt
3
```

