BLOG_DIR := ../../jz-home
POST_DIR := $(BLOG_DIR)/_posts
IMAGE_DIR := $(BLOG_DIR)/images/2016-06-02-knitr

## This target generates post files if necessary and copies them
## into the proper location to be seen on the blog
.PHONY: deploy
deploy : post
	@echo --- Moving markdown output to blog ---
	@cp output/2016-06-02-knitr.md $(POST_DIR)/. 
	@echo --- Copying image files to: $(IMAGE_DIR) ---
	@mkdir -p $(IMAGE_DIR)
	@cp output/figures/*.* $(IMAGE_DIR)/.

## This target just makes the post files locally
.PHONY: post
post: output/2016-06-02-knitr.md 
	@echo --- Generating post ---

## First, extract parameters from the text-based makefile into an R
## list saved into an RDS object file. This just makes it easier to access
## parameters by name during model execution and post-processing
output/parameters.Rds : munge/extract_parameters.R  data/parameters.csv
	@echo --- Extracting parameters from CSV ---
	@mkdir -p $(@D)
	./$< -o $@ -p $(word 2, $^)


## Using the parameter values from the input data, simulate a data file
output/samples.csv : src/simdata.R output/parameters.Rds
	@echo --- Simulating data ---
	@mkdir -p $(@D)
	./$< -o $@ -p $(word 2, $^)

output/figures/d_density.png : src/data_figure.R output/samples.csv
	@echo --- Generating data figure ---
	@mkdir -p $(@D)
	./$< -o output/figures -d $(word 2, $^)


output/2016-06-02-knitr.md : 2016-06-02-knitr.Rmd data/parameters.* output/figures/d_density.png 
	@echo ----Translating RMD to Markdown ----
	@mkdir -p $(@D)
	Rscript \
		-e "require(knitr)" \
                -e "knitr::render_jekyll()"\
		-e "knitr::knit('$<','$@')"

.PHONY: clean
clean:
	rm -rf output
	rm -f $(POST_DIR)/2016-06-02-knitr.md
	rm -rf $(IMAGE_DIR)


