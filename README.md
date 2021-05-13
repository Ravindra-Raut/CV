#Fallow the steps:
1. Install package\
devtools::install_github('nstrayer/datadrivencv')
 
 2. to see more details\
?datadrivencv::use_datadriven_cv

3. To run the package\
datadrivencv::use_datadriven_cv(
    full_name = "Ravindra Raut",
    data_location = "https://docs.google.com/spreadsheets/d/1vSZcNnmwqgQBbtCp1SAwGIUB8cqqa3y6VgNqH3C6Jv8/edit#gid=0",
    pdf_location = "https://github.com/Ravindra-Raut/resume/cv.pdf",
    html_location = "https://github.com/Ravindra-Raut/resume/cv.html",
    source_location = "https://github.com/Ravindra-Raut/resume"
  )

# Knit the HTML version
rmarkdown::render("cv.rmd",
                  params = list(pdf_mode = FALSE),
                  output_file = "cv.html")

# Knit the PDF version to temporary html location
tmp_html_cv_loc <- fs::file_temp(ext = ".html")
rmarkdown::render("cv.rmd",
                  params = list(pdf_mode = TRUE),
                  output_file = tmp_html_cv_loc)

# Convert to PDF using Pagedown
pagedown::chrome_print(input = tmp_html_cv_loc,
                       output = "cv.pdf")


rmarkdown::pandoc_convert("raut_resume.html", to = "pdf")




## Ravindra Raut's pagedown rendered CV

This repo contains the source-code and results of my CV built with the [pagedown package](https://pagedown.rbind.io) and a modified version of the 'resume' template. 

The main files are:

- `raut_index.Rmd`: Source template for the cv, contains a variable `PDF_EXPORT` in the header that changes styles for pdf vs html. 
- `raut_index.html`: The final output of the template when the header variable `PDF_EXPORT` is set to `FALSE`.
- `positions.csv`: A csv with columns encoding the various fields needed for a position entry in the CV. A column `section` is also available so different sections know which rows to use.
- `css/`: Directory containing the custom CSS files used to tweak the default 'resume' format from pagedown. (From `nstrayer/cv`.)
- `parsing_functions.R`: Functions used to parse and properly format position data. (From `nstrayer/cv`.)
- `strayer_template/`: Original CV and resume documents forked from `nstrayer/cv`.

## Acknowledgments

Special thanks to [Nick Strayer](http://nickstrayer.me) for providing his [pagedown CV template on GitHub](https://github.com/nstrayer/cv) and adding customization instructions.
