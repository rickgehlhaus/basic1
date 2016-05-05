library(dplyr)
library(tidyr)
df <- read.csv("refine.csv")  #import csv file
df <- tbl_df(df) #easier to see headers
df$company <- tolower(df$company) #lowercase company field
df$company1 <- gsub("phillips|philips|phllips|fillips|phlips|phillps", "philips", df$company) #cleaning spelling
df$company1 <- gsub("akzo|akz0|ak zo", "akzo", df$company1)
df$company1 <- gsub("van Houten", "van houten", df$company1)
df$company1 <- gsub("unilver|unilever", "unilever", df$company1)
df <- separate(df, Product.code...number,c("product_code", "product_number"), sep = "-") #split into new col.
df$product_category[df$product_code == "p"] <- "smartphone" #product key
df$product_category[df$product_code == "v"] <- "tv"
df$product_category[df$product_code == "x"] <- "laptop"
df$product_category[df$product_code == "q"] <- "tablet"
df <- unite(df, full_address, address, city, country,sep = ",") #make full address
df <- mutate(df, company_philips = ifelse(company1 == "philips", 1, 0), company_akzo = ifelse #create dummies
             (company1 == "akzo", 1, 0), company_van_houten = ifelse(company1 == "van houten", 1, 0),
             company_unilever = ifelse(company1 == "unilever", 1, 0))
df <- mutate(df, product_smartphone = ifelse(product_category == "smartphone", 1, 0),
             product_tv = ifelse(product_category == "tv", 1, 0),
             product_laptop = ifelse(product_category == "laptop", 1, 0),
             product_tablet = ifelse(product_category == "tablet", 1, 0))
