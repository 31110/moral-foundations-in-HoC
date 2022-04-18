
### Step 2: Calculating Probabilities

Once I have a dataset for each party leader, I merge the data using the
`rbind` function for each party, creating four datasets with all the
contributions and their respective probabilities for each party.

For this section of the research, I direct you to [Hopp et al.’s (2020)
tutorial](https://github.com/medianeuroscience/emfdscore/blob/master/eMFDscore_Tutorial.ipynb).

However, for replication, it is important to note that I used the
following setting shwnere running the code:

``` r
DICT_TYPE = 'emfd'
PROB_MAP = 'all'
SCORE_METHOD = 'bow'
OUT_METRICS = 'sentiment'
OUT_CSV_PATH = 'all-sent.csv'
```

I run this for each party’s dataset.

------------------------------------------------------------------------

##### Reference:

Hopp, F. R., Fisher, J. T., Cornell, D., Huskey, R., & Weber, R. (2020).
The extended Moral Foundations Dictionary (eMFD): Development and
applications of a crowd-sourced approach to extracting moral intuitions
from text. Behavior Research Methods,
<https://doi.org/10.3758/s13428-020-01433-0>
