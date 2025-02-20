# Find all .yaml files in the current directory and all subdirectories
YAML_FILES := $(shell find . -type f -name "*.yaml")

# Generate the list of target .smd files by replacing .yaml with .smd
SMD_FILES := $(YAML_FILES:.yaml=.smd)

# Default target
all: $(SMD_FILES)

# Rule to convert .yaml to .smd
%.smd: %.yaml
	@echo "Converting $< to $@"
	@./mergedocs $< 

smd: $(SMD_FILES)
		@echo "All YAML files have been converted to SMD"

# Clean target to remove all generated .smd files
clean:
	@echo "Cleaning up generated .smd files"
	@rm -f $(SMD_FILES)

# Publish target to push all .smd files to the online site
publish: smd
	@echo "Publishing all .smd files"
	for file in $(SMD_FILES); do \
		echo "Publishing $$file"; \
		./publish $$file || exit 1; \
	done
	@echo "All files published successfully"

# Publish a single file (usage: make publish-file FILE=path/to/file.smd)
publish-file:
	if [ -z "$(FILE)" ]; then \
		@echo "Please specify a file with FILE=path/to/file.smd"; \
		exit 1; \
	fi
	if [ ! -f "$(FILE)" ]; then \
		@echo "File $(FILE) does not exist"; \
		exit 1; \
	fi
	@echo "Publishing $(FILE)"
	@publish $(FILE)

# Phony targets
.PHONY: all clean publish publish-file print

# Print the list of YAML files and their corresponding SMD files
print:
	@echo "YAML files:"
	@echo $(YAML_FILES)
	@echo "SMD files:"
	@echo $(SMD_FILES)
