# NAME: Quentin Truong
# EMAIL: quentintruong@gmail.com
# ID: 404782322
.SILENT:

CC = gcc
FLAGS = -Wall -Wextra

lab0:
	$(CC) $(FLAGS) lab0.c -o lab0

check: lab0 stdin_to_stdout stdin_to_outfile infile_to_stdout infile_to_outfile fail_infile fail_outfile unrecognized_argument segfault catch_segfault

stdin_to_stdout:
	echo "expectedinput" | ./lab0 &>/dev/null; \
	if [[ $$? -eq 0 ]]; then echo "Success stdin_to_stdout"; else echo "Fail stdin_to_stdout"; fi

stdin_to_outfile:
	echo "expectedinput" | ./lab0 -o outfile; \
	if [[ $$? -eq 0 ]]; then echo "Success stdin_to_outfile"; else echo "Fail stdin_to_outfile"; fi
	rm -f outfile

infile_to_stdout:
	echo "expectedinput" > infile; \
	if [[ $$? -eq 0 ]]; then echo "Success infile_to_stdout"; else echo "Fail infile_to_stdout"; fi
	rm -f infile

infile_to_outfile:
	echo "expectedinput" > infile
	chmod 777 infile
	./lab0 -i infile -o outfile; \
	if [[ $$? -eq 0 ]]; then echo "Success infile_to_outfile"; else echo "Fail infile_to_outfile"; fi
	rm -f infile outfile

fail_infile:
	echo "expectedinput" > infile
	chmod u-r infile
	echo | ./lab0 -i infile &>/dev/null; \
	if [[ $$? -eq 2 ]]; then echo "Success fail_infile"; else echo "Fail fail_infile"; fi
	rm -f infile

fail_outfile:
	echo "expectedinput" > infile
	touch outfile
	chmod u-w outfile
	./lab0 -i infile -o outfile &>/dev/null; \
	if [[ $$? -eq 3 ]]; then echo "Success fail_outfile"; else echo "Fail fail_outfile"; fi; \
	rm -f infile outfile;

unrecognized_argument:
	./lab0 --asdf &>/dev/null; \
	if [[ $$? -eq 1 ]]; then echo "Success unrecognized_argument"; else echo "Fail unrecognized_argument"; fi

segfault:
	./lab0 --segfault &>/dev/null; \
	if [[ $$? -ne 0 ]]; then echo "Success segfault"; else echo "Fail segfault"; fi

catch_segfault:
	./lab0 --segfault --catch &>/dev/null; \
	if [[ $$? -eq 4 ]]; then echo "Success catch_segfault"; else echo "Fail catch_segfault"; fi

clean:
	rm -f lab0 lab0-404782322.tar.gz

dist: 
	tar -czf lab0-404782322.tar.gz lab0.c Makefile README backtrace.png breakpoint.png
