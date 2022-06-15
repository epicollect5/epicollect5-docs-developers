# Using R

An example of getting Epicollect5 data in R. [Get the source code here.](https://gist.github.com/mirko77/3f4a101cd4a77e2ae3e760d44d18d901)

```
library(httr)
library(jsonlite) # if needing json format

cID<-"999"      # client ID
secret<- "F00HaHa00G" # client secret
proj.slug<- "YourProjectSlug" # project slug
form.ref<- "YourFormRef" # form reference
branch.ref<- "YourFromRef+BranchExtension" # branch reference

res <- POST("https://five.epicollect.net/api/oauth/token",
            body = list(grant_type = "client_credentials",
                        client_id = cID,
                        client_secret = secret))
http_status(res)
token <- content(res)$access_token

# url.form<- paste("https://five.epicollect.net/api/export/entries/", proj.slug, "?map_index=0&form_ref=", form.ref, "&format=json", sep= "") ## if using json
url.form<- paste("https://five.epicollect.net/api/export/entries/", proj.slug, "?map_index=0&form_ref=", form.ref, "&format=csv&headers=true", sep= "")

res1<- GET(url.form, add_headers("Authorization" = paste("Bearer", token)))
http_status(res1)
# ct1<- fromJSON(rawToChar(content(res1))) ## if using json
ct1<- read.csv(res1$url)
str(ct1)

# url.branch<- paste("https://five.epicollect.net/api/export/entries/", proj.slug, "?map_index=0&branch_ref=", branch.ref, "&format=json&per_page=1000000", sep= "") ## if using json; pushing max number of records from default 50 to 10^6
url.branch<- paste("https://five.epicollect.net/api/export/entries/", proj.slug, "?map_index=0&branch_ref=", branch.ref, "&format=csv&headers=true", sep= "")

res2<- GET(url.branch, add_headers("Authorization" = paste("Bearer", token)))
http_status(res2)
ct2<- read.csv(res2$url)
# ct2<- fromJSON(rawToChar(content(res2))) ## if using json
str(ct2)
```
