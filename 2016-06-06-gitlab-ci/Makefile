BLOG_DIR := ../../jz-home
POST_DIR := $(BLOG_DIR)/_posts
IMAGE_DIR := $(BLOG_DIR)/images/2016-06-06-gitlab-ci

## This target generates post files if necessary and copies them
## into the proper location to be seen on the blog
.PHONY: deploy
deploy : 
	@echo --- Moving markdown output to blog ---
	@cp 2016-06-06-gitlab-ci.md $(POST_DIR)/. 
	@echo --- Copying image files to: $(IMAGE_DIR) ---
	@mkdir -p $(IMAGE_DIR)
	@cp images/*.* $(IMAGE_DIR)/.


.PHONY: clean
clean:
	rm -f $(POST_DIR)/2016-06-02-knitr.md
	rm -rf $(IMAGE_DIR)


