R Markdown
----------

This is an R Markdown document. Markdown is a simple formatting syntax
for authoring HTML, PDF, and MS Word documents. For more details on
using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that
includes both content as well as the output of any embedded R code
chunks within the document. You can embed an R code chunk like this:

    summary(cars)

    ##      speed           dist       
    ##  Min.   : 4.0   Min.   :  2.00  
    ##  1st Qu.:12.0   1st Qu.: 26.00  
    ##  Median :15.0   Median : 36.00  
    ##  Mean   :15.4   Mean   : 42.98  
    ##  3rd Qu.:19.0   3rd Qu.: 56.00  
    ##  Max.   :25.0   Max.   :120.00

Including Plots
---------------

You can also embed plots, for example:

![](Web_Scrap_files/figure-markdown_strict/pressure-1.png)

Note that the `echo = FALSE` parameter was added to the code chunk to
prevent printing of the R code that generated the plot.

Install rvest
=============

Install.packages('rvest')

    library(rvest)

    ## Loading required package: xml2

WEB SCRAPING
============

    content <- read_html('https://news.ycombinator.com/')
    content

    ## {xml_document}
    ## <html op="news">
    ## [1] <head>\n<meta http-equiv="Content-Type" content="text/html; charset= ...
    ## [2] <body><center><table id="hnmain" border="0" cellpadding="0" cellspac ...
    ## [3] <script type="text/javascript" src="hn.js?ZlOjL55sRmhJBqfwi2jb"></sc ...

    title <- content %>% html_nodes('a.storylink') %>% html_text()
    title

    ##  [1] "Dirt Poor: Have Fruits and Vegetables Become Less Nutritious?"               
    ##  [2] "Facebook’s tracking of non-users ruled illegal again in Europe"              
    ##  [3] "Eight Years On, Google Fiber Is a Faint Echo of the Disruption Promised"     
    ##  [4] "Show HN: The king of the sidewalk: Extreme pimping of my sons ride-on"       
    ##  [5] "A week-long programming retreat"                                             
    ##  [6] "An iOS App in Assembly (2014)"                                               
    ##  [7] "The efforts of Edo-era doctors to figure out beriberi in Japan"              
    ##  [8] "Satan Comes to Dinner (1997)"                                                
    ##  [9] "45 year CPU evolution – one law and two equations"                           
    ## [10] "A whirlwind introduction to dataflow graphs"                                 
    ## [11] "Tracking where your time went with Lego workstream visualisation"            
    ## [12] "Chuck Feeney: a billionaire who gave it all away"                            
    ## [13] "Tracing from JavaScript to the DOM and Back Again"                           
    ## [14] "Hiroshima and Nagasaki: The Long Term Health Effects (2012)"                 
    ## [15] "A UI Experiment with the iPhone X’s Front-Facing Camera"                     
    ## [16] "MacPaint and QuickDraw Source Code (2010)"                                   
    ## [17] "The virus hunter: In a bygone era, C.J. Peters learned how to bend the rules"
    ## [18] "CircuitHub Is Hiring Electronics CAD Engineers"                              
    ## [19] "Images of Los Angeles when it was covered in wetlands"                       
    ## [20] "Sndio: a small audio and MIDI framework part of the OpenBSD project"         
    ## [21] "Creating a WebAssembly-powered library for the modern web"                   
    ## [22] "Elm, Elixir, and Phoenix: Reflecting on a Functional Full-Stack Project"     
    ## [23] "RIP Cert.org"                                                                
    ## [24] "For whom, the bell tolls"                                                    
    ## [25] "Spooky action at a distance, how an AWS outage ate our load balancer"        
    ## [26] "Technology firms as a threat to basic liberties"                             
    ## [27] "A 'Brief' History of Game AI Up to AlphaGo"                                  
    ## [28] "The next great urban reset"                                                  
    ## [29] "The Drugging of the American Boy (2014)"                                     
    ## [30] "(2007) Joshua Bloch: How to Design a Good API and Why It Matters"

    link_domain <- content %>% html_nodes('span.sitestr') %>% html_text()
    link_domain

    ##  [1] "scientificamerican.com" "techcrunch.com"        
    ##  [3] "vice.com"               "ihackshit.com"         
    ##  [5] "facebook.com"           "github.com"            
    ##  [7] "atlasobscura.com"       "erights.org"           
    ##  [9] "arxiv.org"              "fgiesen.wordpress.com" 
    ## [11] "joejag.com"             "irishtimes.com"        
    ## [13] "v8project.blogspot.com" "columbia.edu"          
    ## [15] "fastcodesign.com"       "computerhistory.org"   
    ## [17] "statnews.com"           "circuithub.com"        
    ## [19] "businessinsider.com"    "sndio.org"             
    ## [21] "hackernoon.com"         "teamgaslight.com"      
    ## [23] "riskbasedsecurity.com"  "economist.com"         
    ## [25] "hostedgraphite.com"     "ocregister.com"        
    ## [27] "andreykurenkov.com"     "cnu.org"               
    ## [29] "esquire.com"            "youtube.com"

    score <- content %>% html_nodes('span.score') %>% html_text()
    score

    ##  [1] "93 points"  "819 points" "138 points" "13 points"  "380 points"
    ##  [6] "34 points"  "48 points"  "19 points"  "20 points"  "35 points" 
    ## [11] "63 points"  "126 points" "27 points"  "43 points"  "92 points" 
    ## [16] "54 points"  "4 points"   "47 points"  "86 points"  "3 points"  
    ## [21] "40 points"  "187 points" "64 points"  "56 points"  "55 points" 
    ## [26] "41 points"  "24 points"  "112 points" "27 points"

    age <- content %>% html_nodes('span.age') %>% html_text()
    age

    ##  [1] "1 hour ago"     "13 hours ago"   "6 hours ago"    "22 minutes ago"
    ##  [5] "10 hours ago"   "3 hours ago"    "3 hours ago"    "2 hours ago"   
    ##  [9] "3 hours ago"    "4 hours ago"    "5 hours ago"    "9 hours ago"   
    ## [13] "4 hours ago"    "6 hours ago"    "9 hours ago"    "8 hours ago"   
    ## [17] "2 hours ago"    "1 hour ago"     "9 hours ago"    "11 hours ago"  
    ## [21] "1 hour ago"     "2 hours ago"    "15 hours ago"   "8 hours ago"   
    ## [25] "7 hours ago"    "1 hour ago"     "8 hours ago"    "6 hours ago"   
    ## [29] "15 hours ago"   "2 hours ago"
