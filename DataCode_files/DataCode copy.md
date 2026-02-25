# DataCode


Running Code

All packages required for data processing

``` r
rm(list=ls())
library(tidyverse)
```

    ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ✔ dplyr     1.2.0     ✔ readr     2.1.6
    ✔ forcats   1.0.1     ✔ stringr   1.6.0
    ✔ ggplot2   4.0.2     ✔ tibble    3.3.1
    ✔ lubridate 1.9.5     ✔ tidyr     1.3.2
    ✔ purrr     1.2.1     
    ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ✖ dplyr::filter() masks stats::filter()
    ✖ dplyr::lag()    masks stats::lag()
    ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(readxl)
library(vegan)
```

    Loading required package: permute

``` r
data <- read_excel("Data/zooplankton_data.xlsx")#enter the data
```

    New names:
    • `` -> `...16`

Analysis (PCA)

Calculate the main components Use Principle Component Analysis This is
done to summarize variation in multivariate data

``` r
workdata <- data %>%
  slice(1:14) %>%
  select(2:15)
pca.fit <- workdata %>%
  select(-1) %>% #remove first column
  prcomp(scale. = TRUE)
pca.fit <- prcomp(x = workdata[, -c(1)], scale. = T) #scale=T ensures all variables are scaled to have a mean 
```

Use these results and the summary command to assign the output to a
variable (pca.summary)

``` r
pca.summary <- summary(pca.fit)

names(pca.summary) #view summary
```

    [1] "sdev"       "rotation"   "center"     "scale"      "x"         
    [6] "importance"

``` r
pca.summary$importance #view variance explained
```

                                PC1     PC2      PC3     PC4       PC5       PC6
    Standard deviation     2.127166 1.58437 1.438161 1.11728 0.9947211 0.8119034
    Proportion of Variance 0.348060 0.19309 0.159100 0.09602 0.0761100 0.0507100
    Cumulative Proportion  0.348060 0.54116 0.700260 0.79628 0.8724000 0.9231000
                                 PC7       PC8       PC9      PC10       PC11
    Standard deviation     0.6769965 0.5994863 0.3788346 0.1729906 0.08744047
    Proportion of Variance 0.0352600 0.0276400 0.0110400 0.0023000 0.00059000
    Cumulative Proportion  0.9583600 0.9860000 0.9970400 0.9993500 0.99993000
                                 PC12        PC13
    Standard deviation     0.02918766 0.003288521
    Proportion of Variance 0.00007000 0.000000000
    Cumulative Proportion  1.00000000 1.000000000

``` r
#This will give you the most importance principals (PC1, PC2)
pca.fit$rotation #view important variables
```

                                PC1         PC2         PC3         PC4
    Amphipoda         -0.0019443192 -0.45662557 -0.20232862  0.01750905
    Nematoda           0.1493704662 -0.12062304  0.50019839 -0.10972961
    Salp              -0.4163060936  0.03744006  0.16636489  0.23075690
    Copepoda          -0.4544665221  0.01362451  0.10516267  0.10397327
    Eggs               0.1332941712 -0.24045695  0.51810188 -0.21950795
    Chaetognaths       0.1563631672  0.28465709 -0.11862234  0.60522036
    Polychaetea       -0.0243625882 -0.52922487  0.07822764  0.37512331
    Crustacean larvae  0.2824246257  0.27961819  0.15032723  0.37094642
    Egg_mass           0.1497772448 -0.10236028  0.47853041  0.30314853
    Euphausid         -0.3940256794  0.07816830  0.07382493 -0.05339218
    Mysid             -0.4023682688  0.03645004  0.17083465  0.26565093
    Medusa            -0.3683342729  0.01177591  0.06189691 -0.10604817
    Mite               0.0005474683 -0.51008441 -0.30241097  0.23288000
                               PC5         PC6         PC7          PC8         PC9
    Amphipoda         -0.503883491  0.34397096  0.01526351  0.267855727 -0.49952141
    Nematoda           0.338863243 -0.14935097 -0.31861304  0.643550185 -0.20812009
    Salp               0.169532941  0.28165593 -0.01892120 -0.068456780 -0.08868354
    Copepoda          -0.001040533  0.11487515  0.06925426  0.148531579  0.02797003
    Eggs              -0.041434602  0.03086865  0.44027177 -0.388247477 -0.30302874
    Chaetognaths      -0.011871312 -0.29995513  0.47316255  0.275098443 -0.26102011
    Polychaetea        0.238237829 -0.21216932  0.15308675 -0.102936208  0.06796522
    Crustacean larvae -0.140407461  0.12901658 -0.54287937 -0.319718076 -0.35960353
    Egg_mass          -0.493336811 -0.03194470 -0.05428657  0.001394003  0.51902488
    Euphausid         -0.461009872 -0.21441806 -0.05928597  0.237588505  0.07902273
    Mysid              0.202181890  0.32254784 -0.03650553 -0.080904196 -0.04946643
    Medusa            -0.121839824 -0.66186756 -0.17882854 -0.273747370 -0.33600321
    Mite               0.112105244 -0.15863010 -0.34270811 -0.100917725  0.11682851
                             PC10        PC11         PC12         PC13
    Amphipoda          0.11515451 -0.16191254 -0.126516399 -0.032362730
    Nematoda           0.05556222  0.01750327  0.037089131 -0.003362240
    Salp               0.29825078  0.52044646 -0.373990963 -0.351700972
    Copepoda          -0.54818869 -0.27702032  0.317050700 -0.502787420
    Eggs              -0.05138957  0.23740581  0.331189688  0.006273347
    Chaetognaths       0.13064918  0.07515305  0.178752366 -0.040998695
    Polychaetea       -0.39417112 -0.08483823 -0.465302747  0.230199110
    Crustacean larvae -0.33860304  0.05827150 -0.006647072  0.033864786
    Egg_mass           0.26541138 -0.17579097 -0.021979179 -0.166230365
    Euphausid         -0.26712771  0.48376269  0.059782033  0.443466201
    Mysid              0.27926109 -0.34160373  0.278550205  0.556333080
    Medusa             0.25335015 -0.28574259 -0.107743876 -0.137625747
    Mite               0.14311344  0.29999976  0.539241900 -0.117693400

Create a a mainframe for plot use

``` r
pca_scores <- as_tibble(pca.fit$x) %>%
  mutate(Site = data$Site[1:14])
```

Make a user friendly plot

``` r
ggplot(pca_scores, aes(x = PC1, y = PC2, colour = Site)) +
  geom_point(size = 3) +
  labs(x = "PC1",
       y = "PC2",
       title = "PCA by Site") +
  theme_minimal()
```

![](DataCode_files/figure-commonmark/unnamed-chunk-5-1.png)
