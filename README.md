**Markov cahain Text generation code**
#Packages
'''
install.packages("markovchain")
install.packages("tm")
library(markovchain) 
library(tm)
'''
#Import Text
text <- readLines(file.choose())
filePath <-"C:\\Users\\JosephN2\\Desktop\\That.txt"
text <- readLines(filePath)

#Text cleaning
docs <- Corpus(VectorSource(text))
inspect(docs)
toSpace <- content_transformer(function (x , pattern ) gsub(pattern, " ", x))
docs <- tm_map(docs, toSpace, "/")
docs <- tm_map(docs, toSpace, "@")
docs <- tm_map(docs, toSpace, "\\|")
docs <- tm_map(docs, toSpace, ")")
docs <- tm_map(docs, toSpace, "?")

# Remove punctuations
docs <- tm_map(docs, removePunctuation)

# Eliminate extra white spaces
docs <- tm_map(docs, stripWhitespace)
docs <- tm_map(docs, removeNumbers)
length(docs)

#Split text
terms <- unlist(strsplit(text, ' '))
fit <- markovchainFit(data = terms) 
plot(fit$estimate) 
paste(markovchainSequence(n=15, markovchain=fit$estimate), collapse=' ')



