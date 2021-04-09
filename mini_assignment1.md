# GCC and LLVM
GCC is an optimizing compiler produced by GNU project. It is one of the biggest open source software. It is supported by many programming languages like c,c++,Objective-c,Objective-C++, Fortran, Java, Ada, D and Go. Operating systems like Windows, Android, iOS, Solaris, HP-UX, AIX and DOS. It is also available for many embedded systems, including ARM-based and Power ISA-based chips. 

LLVM stands for low level virtual machine.basically it is a project started in 2000 at University of Illinois to focus on virtual machines . Now its research is broadened to commercial and open source projects. It is written in c++ and it can help in building compilers . There are many language compilers that use LLVM like ActionScript, Ada, C#, Common Lisp, Crystal, CUDA, D, Delphi, Dylan, Fortran, Graphical G, Halide, Haskell etc 

### short note on various options in common compilers: GCC and LLVM.
Let’s make it clear what does options mean? these are the instructions/commands that performs specific job/task depending on the instruction . Some options control  preprocessing and a few control compiler and a bunch of control assembler and linker. These options may be single letters or multi letter words.
Lets look into to the options of gcc:
> gcc/g++ filename.c / filename.cpp  
	=> this is a basic command , it is used to compile filename.c/.cpp , where the object file 	created after compiling  is stored in a.out file.
gcc/g++ filename.c / filename.cpp -o object 
	=> this is similar to above , execpt instead of a.out, here object stores the compiled 	object file. 
	
To execute the object file created above, use ./a.out for running and gdb ./a.out for debugging
The above two are basic commands one must know to compile eighter c or c++ file.
Now lets look into other command options:
lets look the below options with this example . suppose in your folder named “programming”there is a file.c programme. Now lets look into the following commands
> gcc  -c  file.c 
	=> here we used extra “-c” command  , the main job of it is not to link unlike above. 
	Eg: so after executing this command , a new file named file.o is generated. But it wont be 	       suitable for running . 
gcc -o file file.o -lm 
	=> here command -o file  is  used ,which tells comipler to name the executable as hello .
	  And here the -lm command is used for linking purpose , where in the above command we 	  missed linking part.
	Eg: so after executing this command also, we will get an extra file named file , which is now 	     suitable for execution.
gcc -Wall file.c
	=> it enables all the warning symbols, which help us to find bugs.
Gcc -w file.c 
	=> it is opposite to the above command , which enables all the warning symbols.
Gcc -glevel
	=> it generates debugging information , for gdb usage.
Gcc -Llib
  	=> it helps to link with library files.
  	
Lets look into to the options of LLVM:
here in the clang to compile and run a code there are 6 phases like driver,preprocessing,parsing and semantic analysis, Code Generation and Optimization , Assembler ,linker.
Now lets see opttions for stage selection:
> -E  => to run the preprocessor stage mentioned above.
-fsyntax-only => to run the preprocessor,parser and type checking stages.
-s => run the previous stage as well as LLVM code generation and optimization phase target-	specific code generation,to  produce an assembly file.
-c => to run all of the above, plus the assembler,to generate a target “.o” object file.

Now for language selection and mode options:
> -x c/c++/fortan etc..
	  => it treats the input file as the language what we written after “x”.
-std=c89/c90/iso9899:199409/gnu89/gnu90/c11/c17 etc..
	=>it specifies the language standards which to be run.by default c takes gnu17.similarly for 	    c++ also and by default c++ choose gnu++14.
-stdlib=libstdc++ / libc++ 
	=> specify which c++ libray to use
-rtlib=libgcc/compiler-rt   
	=> specifies which compile time library to use

and some other options like:
> -arch <architecture>
	=>  specify the architecture to build for
-mcpu=?, -mtune=?
  	=>  Acts as an alias for --print-supported-cpus.

### Write a note on the various frontends that these compilers support.
In frontend part compilers convert source programme to intermediate code  and in the backend part this intermediate code is converted to machine code.
Let’s make this point clear, LLVM is not exactly a compiler like GCC . It works like a frame work to generate object code.
GCC supports many frontends like : 
>	    language	       		 GCC front end 	      	
		c			        	gcc			
		c++			        	g++				
		fortran		    		gnufortran			
		ada			         	GNAT			
		Go			        	gccgo			
		D 			        	GDC

LLVM  supports many front ends like:
 >	    language			LLVM front ends
		c			    	clang
		c++			    	clang
		D			    	LDC(LLVM D compiler)
		fortran				flang
		Haskel				Utrecht
		objective-C			clang
		Rust(uses LLVM as its compiler framework)
		Swift (uses LLVM as a core component of its tool chain)

### Use these compilers to generate code for various architectures using its various backends and report your findings 
In backend part convertion of  intermediate code to machine executable code takes place. 
Here in this case i used cross compilation to run a code on arm-32  and arm-64
Here as an example i run my “add.c(which adds 2 numbers taken input from console) programme in  x_86(my original architecture)  , in arm-32 bit and in arm-64 bit  architectures . 

The main difference i found in these files are the sizes of these files
>     architecture		    gcc		            	clang
    x86_64      	    	16.8 kB          		16.5 kB
    arm-32 		          579.7 kB		 
    arm-64		        662.5 kB


which means the x86_64 < Arm-32 bit < Arm-64 bit . This is the sizes order 
ths difference is because different architectures use differnt kind of execution so these sizes are diifferent. 

### Compilers come with various optimization levels: Focusing on options O0, O1, O2, O3 as well as -Os, -Oz, run various codes using these predetermined passes and report your findings. 

gcc provides optimization levels, In order to control compilation-time and compiler memory usage whose numbers/levels vary from 0 to 3. we already know two of these i.e o0,o1. it is similar to nothing and -o. which we did in general compilations like “gcc filename.c “ and “gcc filename.c -0 executable” . 
-o0 or no -o option
here it is called as zero optimization level in which no kind of optimization takes place and it  compile the given source code into executable as it is with out any modifications in the source code.  It is helpful in the case of debugging.

-o1 or -o option:
this level activates the foremost common sorts of optimization that don't require any speed-space tradeoffs. With this option the execution will be faster that -o0 . Expensive schedulings like instruction scheduling are not used here. Due to simple optimizations the amount of data will be reduced , so compile time also improves than -o0.

-o2 option:
in this level the extra optimizations are instruction scheduling, only the non speed-space required optimizations are used, which make executable size not to increase. So,The compiler will take longer time to compile programs and it requires more memory than with -o1. Without increasing size of executables it gives best optimization. 


-o3 option:
this in option more expensive optimizations are taking place, like function inlining  in addition to all the optimizations of -o0,o1,o2. It increases the speed  of compiling as well as the size of the executable as compared to o2. Due to increase in size in few ccases it may also lead to increase in time taken.

-os option:
in these optimizations size of the executable file is reduced. We wont focus on time constraints here in some cases due to low memory of executables the execution may speedup due to better cache usage.

-oz option:
its main aim is to reduce size of the executable as in os, with out using link-time-optimization(LTO) . It also wont focus on time constraints. It instructs compilers to optimize code size only not the performance which results in slower code.

lets look into the variation in time and size of the executable while varying options for roundrobin scheduling algorithm

>        options              time                  size
        o0                  0.055 sec            17.2
        o1                  0.054 sec            17.2
        o2                  0.041 sec            17.2
        o3                  0.038 sec            17.2
        os                  0.091 sec            17.2
        oz                  0.066 sec            17.2

there may be slight variations in these values but they are almost accurate.



https://github.com/G-Venkata-Surya-Sai/compilers1/new/main



