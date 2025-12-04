FROM prairielearn/grader-r:17dae10c6ffd1e8bce5ef7fe24b43228a4fee6b6

ADD install.R /

RUN Rscript --no-save install.R arrow caret corrr \
                    crayon forecast hexbin \
                    dplyr e1071 htmltools \
                    jsonlite kknn nycflights13 \
                    palmerpenguins randomForest RCurl \
                    rmarkdown robotstxt RODBC \
                    RSQlite rvest stringr \
                    themis tidyverse tidymodels \
                    htmlwidgets httr infer waffle \
                    naniar simputation mice MLmetrics \
                    visdat DMwR2 tibble cellWise \
                    matrixStats VIM Hmisc 

