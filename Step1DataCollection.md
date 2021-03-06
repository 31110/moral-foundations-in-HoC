
### Step 1: Data Collection

The first step of this study was to create a dataset with the
probability that each contribution made by a party leader belongs to a
particular moral foundation.

Therefore, I needed to download every debate that took place in the
House of Commons since 1979; I did that using the text scraped debates
that ‘They Work For You’ scraped from Hansard. You can find that page
here: <https://www.theyworkforyou.com/pwdata/scrapedxml/debates/>.

Each file is a .xml file, which needed to be downloaded. I used a Google
Chrome Extension (DownThemAll, find it here:
<https://www.downthemall.org/howto/>
help/english-menu/batch-downloadsbatch-descriptors/) to do this.

I end up with a folder on my computer of each debate ever undertaken in
the House of Commons, since the required date.

I first tell R where each debate is, and read in the first debate. Using
a loop command, I read in each debate and utilise the rbind command to
create one dataset of every debate ever undertaken:

``` r
debates<-list.files(path=folder, pattern='.xml', full.names = TRUE)

main    <- readDebateXML("debates1975-01-13a.xml")

for (file in debates){
  df <- readDebateXML(file)
  main <- do.call("rbind.fill", list(df,main))
```

Once I have this dataset, I want to extract the specific contributions
from each party leader, so I use the filter function to extract, for
example, Boris Johnson’s contributions to the House, and then extract
only the contributions he made whilst he was Prime Minister. I do this
for each party leader. Finally, I extract this as a .csv file in order
to run it through the eMFD.

``` r
BoJo <-
  main %>%
  filter(speaker == 'Boris Johnson')
BoJo <- BoJo[BoJo$date <= "2022-01-12" & BJ$date >= "2019-07-24",]
BoJo
write.csv(BoJo, file="BJohnson.csv")
```

The next step will explore running these contributions through Python to
calculate the probabilities of belonging to a particular moral
foundation.
