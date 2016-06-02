.PHONY: post
post: ../../jz-home/_posts/2016-06-02-knitr.md


../../jz-home/_posts/2016-06-02-knitr.md : 2016-06-02-knitr.Rmd
	@echo ----Translating RMD to Markdown ----
	Rscript \
		-e "require(knitr)" \
                -e "knitr::render_jekyll()"\
		-e "knitr::knit('$<','$@')"

.PHONY: clean
clean:
	rm ../../jz-home/_posts/2016-06-02-knitr.md

