FROM prairielearn/grader-r:17dae10c6ffd1e8bce5ef7fe24b43228a4fee6b6

RUN R -e "install.packages(c('arrow', 'caret', 'corrr', 
                             'crayon', 'forecast', 'hexbin', 
                             'dplyr', 'e1071', 'htmltools', 
                             'jsonlite', 'kknn', 'nycflights13',
                             'palmerpenguins', 'randomforest', 'rcurl',
                             'rmarkdown', 'robotstxt', 'rodbc',
                             'rsqlite', 'rvest', 'stringr',
                             'themis', 'tidyverse', 'tidymodels',
                             'htmlwidgets', 'httr', 'infer', 'waffle'), 
                             repos='https://cloud.r-project.org/')"

