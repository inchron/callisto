#
# Sample Makefile
#
# emf4cpp is a free implementation of the EMF Ecore framework for C++.
# See https://github.com/inchron/emf4cpp
#
OUTPUT=output
EMF4CPP=/opt/inchron/emf4cpp/bin/emf4cpp.generator.sh


all: $(OUTPUT)/.stamp

# emf4cpp does not change any files if there is no need for, hence we use 
# a .stamp marker for a successful code generation.
$(OUTPUT)/.stamp: callisto.ecore
	@mkdir -p $(OUTPUT)
	$(EMF4CPP) -c -o $(OUTPUT) callisto.ecore 
	@touch $@

clean:
	rm -rf ./output

