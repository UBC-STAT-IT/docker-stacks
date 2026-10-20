FROM prairielearn/grader-r:a64f8e8b8cd2fa0273f61a7aa5bbdef3cf682503

ADD install.R /

RUN Rscript --no-save install.R arrow caret corrr \
                    crayon forecast hexbin \
                    dplyr e1071 htmltools \
                    jsonlite kknn nycflights13 RobStatTM robustbase \
                    palmerpenguins randomForest RCurl \
                    rmarkdown robotstxt RODBC \
                    RSQlite rvest stringr \
                    themis tidyverse tidymodels \
                    htmlwidgets httr infer waffle \
                    naniar simputation mice MLmetrics \
                    visdat DMwR2 tibble cellWise \
                    matrixStats VIM Hmisc NHANES

