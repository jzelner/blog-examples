.PHONY: post
IMAGE_DIR := ../../jz-home/images/2016-06-02-knitr
post: ../../jz-home/_posts/2016-06-02-knitr.md output/figures/d_density.png
	@echo --- Generating post ---
	@echo --- Making output image directory: $(IMAGE_DIR) ---
	@mkdir -p $(IMAGE_DIR)
	@cp output/figures/*.* $(IMAGE_DIR)/.

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


../../jz-home/_posts/2016-06-02-knitr.md : 2016-06-02-knitr.Rmd data/parameters.csv output/*.* output/figures/*.* 
	@echo ----Translating RMD to Markdown ----
	Rscript \
		-e "require(knitr)" \
                -e "knitr::render_jekyll()"\
		-e "knitr::knit('$<','$@')"

.PHONY: clean
clean:
	rm ../../jz-home/_posts/2016-06-02-knitr.md
	rm -r output
	rm -r $(IMAGE_DIR)


