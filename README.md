# common-linux

This is a list of most common Linux command lines tips and tricks. Includes both for C-Shell and Bash.

# Linux Admin
+ Modifying user

		Usermod -u uid -g gid [username]

+ IP address

		ip a 

+ To go to another terminal screen

		ctrl-alt-f[screennumber]  

where screen number is the number you want

+ Kill process (savage)

		kill $(ps aux | grep '[p]ython csp_build.py' | awk '{print $2}')

+ Run program even when ssh connection is terminated

		nohup [command] > logfile

+ Find process by a certain user

		ps -u username

+ Check logs

		dmesg

+ Check cpu usage every 2 seconds for 5 iterations

		mpstat 2 5

+ Find process by pattern

		ps -fC pattern

+ Kill process by pattern

		kill -f pattern

# Common

+ Find row based on maximum value of a certain column (looking at second column)

		awk 'BEGIN{max=0}{if(($2)>max) {max=($2);i=($1)}END {print max, i}' 

+ Find and move

		find path_A -name '*AAA*' -exec mv -t path_B {} +

+ Find files large than certain size

		find ./ -size +4G

+ Find files/binaries that was access x mins ago

		find ./ -amin -x

+ Two ways of executing on find results (ok asks for confirmation)
		
		find ./ -exec rm {} \;
		find ./ -ok rm {} \;

+ Output starting from 25th line

		tail -n +25 file.log

+ Finding characters at the end of the line

		grep '0,0$' file

+ Print every 10 lines

		sed -n "1~10 p" file 

+ Print every 10 lines and 1 line after each of the 10 lines

		sed -n "1~10, +1p" file

+ Only report line numbers for grep

		grep -n file | cut -f1 -d

+ grep showing filename for occurence of fine

		find ./ -name "Makefile" -exec grep AVX {} /dev/null  \;

+ Inline for loop (csh)

		echo 'foreach f ( 1 2 3 )\n echo $f \n end' | tcsh

+ Inline for loop (bash)

		for i in {1..5}; do COMMAND-HERE; done

+ Count column

		head -2 english_dataset.csv |tail -1  | sed 's/[^,]//g' | wc -c

+ Replace substring and save back to file

		sed -i 's/original/new/g' file.txt

# SeismicUnix
+ Creating waveform

		uwaveform tape=ricker1 fpeak=(fdommax) dt=(sample rate in seconds) > wavename.su

+ Wave viewing

		suxwigb < wavename.su 

+ Get summary of wave (print all traces' header in summary, 0 values omitted)

		surange < wave.su 

+ Converting su files to segy files.

		segyhdrs < wavename.su  

		segywrite tape=wavename.segy < wavename.su 

+  Viewing frequency spectrum of wavelet

		sufft < [sufile] | suamp mode=amp | suxwigb

+ Perc with tpow (for shot gathers)

		sugain tpow < [shotgathers.su]

+ Perc with stacked images (migrated)

		sugain epow < [image.su]

+ Filter out frequency from a to b so that it's amplitude goes from c to d
		
		sufilter f=a,b amp=c,d < [suwave]

+ Change value of a header property

		suchw  key1=dt key2=scalel a=0 b=25000 e=0 c=0 d=1 < input_su_name > output_su_name

# Other commands
+ Running MPI

		mpirun -np 3 --machinefile hostfile ./executable argument_files.arg

+ Run only a single testcase for python unittest

		python testMyCase.py MyCase.testItIsHot

+ Disable ssl verification for cloning

		git -c http.sslVerify=false clone [addr]

+ Adding proxy to git (%5C is backslash, %40 is @)

		git config --global https.proxy https://company%5Cuname:password%40@170.28.2.1:8080

+ Viewing status of tracked files

		git status --untracked-files=no 

+ Create a new branch, with modified files to be commited to new branch

		git checkout -b [branch name]

+ Revert to certain commit 

		git reset --hard [commit_id]
		