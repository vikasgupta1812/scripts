

#### How to remove Columns by name from data.frame
```r
churnTrain = churnTrain[,!names(churnTrain) %in% c("state", "area_code", "account_length") ]
churnTest = churnTest[,! names(churnTrain) %in% c("state", "area_code", "account_length") ]
```

#### How to split data into  training and testing sets randomly in reproducible way

```r
set.seed(2)
ind = sample(2, nrow(churnTrain), replace = TRUE, prob=c(0.7, 0.3))
trainset = churnTrain[ind == 1,]
testset = churnTrain[ind == 2,]
```

#### How to set Jyputer display parameters for IRKernel

```
options(repr.plot.width = 4, repr.plot.height = 3)
```

```
# Change mimetype 
options(jupyter.plot_mimetypes = "image/png") 
options(jupyter.plot_mimetypes = "image/svg+xml")
```


#### Use custom fonts in R, e.g. with ggplot2
The package [showtext](https://github.com/yixuan/showtext) can import .otf font files, that can be used with ggplot2 theme options.
```
library(showtext)
font.add("NameOfFont", "NameOfFont.otf")
showtext.auto() 
```
Alternativly, there is [extrafont](https://www.r-project.org/nosvn/pandoc/extrafont.html). The downside: It can only use .ttf files.
```
library(ggplot2)
ggplot(d, aes(x = x, y = y)) +
geom_point() +
theme(text = element_text(family="NameOfFont"))
```

#### Import online csv via R
```
library(RCurl)
url <- getURL("http://www.adress.com/data.csv")
d <- read.csv(text = url)
```


----
System 

```r
library(showtext)
png("System-Fonts.png", width=550, height=350);
par(mfrow=c(2,2))
plot(1 ~ 1, main="Lucida Bright", family = "Lucida Bright")
plot(1 ~ 1, main="Courier", family = "Courier")
plot(1 ~ 1, main="Helvetica Neue Light", family = "Helvetica Neue Light") 
plot(1 ~ 1, main="Lucida Handwriting Italic", family = "Lucida Handwriting Italic")
dev.off()
```


![](http://4.bp.blogspot.com/-68tbzYAcFPw/VXHuuP34LpI/AAAAAAAACFQ/qUF7_tl6FWo/s1600/Fonts_in_R.png)

```r
font.add.google("Alegreya Sans", "aleg");
font.add.google("Permanent Marker", "marker")
font.add.google("Gruppo", "gruppo")
font.add.google("Lobster", "lobster")
png("Google-Fonts.png", width=550, height=350)
showtext.begin()
par(mfrow=c(2,2))
plot(1 ~ 1, main="Alegreya Sans", family = "aleg")
plot(1 ~ 1, main="Permanent Marker", family = "marker")
plot(1 ~ 1, main="Gruppo", family = "gruppo") 
plot(1 ~ 1, main="Lobster", family = "lobster") 
showtext.end()
dev.off()
```

more examples here - https://github.com/yixuan/showtext/blob/59a1ba58d9c46f0e4ecc8fcc9f3d16def1cacf6d/README.md


```r
## Automatically use showtext to render text for future devices
showtext.auto()
```



#### Access SQL-Database via R

RMySQL is a handy package to import data from a sql database in R.

One caveat: if the location is on localhost, the host needs to be host = "127.0.0.1", instead of host = "localhost"

```
library(RMySQL)
# if database on localhost
db = dbConnect(MySQL(), user='root', password='root', host = "127.0.0.1", port=8888, dbname="table_name")

# look at tables in database
dbListTables(db)

# variables in a table
dbListFields(db, 'table_name')

# sql query to get all data in a table
query = dbSendQuery(db, "SELECT * FROM table_name")

# save as dataframe
df = fetch(query, n=-1)

look at dataframe in R
head(df)
```

#### How to load data from Google Spreadsheets into R

The googlesheets package from statistics professor Jennifer Bryan at the University of British Columbia is by far the most convenient way.
```
library(dplyr)
library(googlesheets)

# load all sheets in google drive by authentication (new browser tabs with 
all_my_sheets_in_drive <- gs_ls()

# show all sheets in R
my_sheets

# get a specific sheet
d <- gs_title("Name of Googlesheet")

# get worksheet 
d <-  d %>% gs_read(ws="worksheet 1")
```

#### How to set theme in ggplot figures. 

```
theme_set(theme_minimal(24))
ggplot(aes(x = gender, y = age),
      data = subset(pf, !is.na(gender))) + geom_boxplot()
```


- Supress warning messages from Packages 

```
suppressMessages(library(dplyr))
```
