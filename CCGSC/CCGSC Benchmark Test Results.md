[[0 CCGSC_Manuscript_Organizer_Dashboard]]
[[Related Resources CCGSC]]




4000000000 on mvp demo v1 with 3 workers took 4 minutes

3 laptops and 2 mobiles 
4000000000 on mvp demo v1 with 8 workers took 2 minutes 23 seconds 
4000000000 on mvp demo v1 with 10 workers took 3 minutes 13 seconds 
4000000000 on mvp demo v1 with 10 workers took 1 minutes 44 seconds 
4000000000 on mvp demo v1 with 10 workers took 2 minutes 13 seconds 
4000000000 on mvp demo v1 with 10 workers took 2 minutes 12 seconds 




Device name	DESKTOP-KD0A63N
Processor	Intel(R) Core(TM) i7-8665U CPU @ 1.90GHz (2.11 GHz)
Installed RAM	48.0 GB (47.7 GB usable)
Device ID	F1968C6F-0CCB-40DE-BB77-C2F36AB17246
Product ID	00330-53024-26684-AAOEM
System type	64-bit operating system, x64-based processor
Pen and touch	No pen or touch input is available for this display

Edition	Windows 11 Pro
Version	24H2
Installed on	‎3/‎22/‎2025
OS build	26100.4652
Experience	Windows Feature Experience Pack 1000.26100.128.0


C/C++ code - 10000000000 was finished in 25, 30, 40, 50, 55, 60 seconds on single machine vs code 



C/C++ code - 10000000000 was finished in 
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> & .\'PrimeNumST.exe'
Single-Threaded: 455052511 primes found up to 10000000000
Time: 1063.71 seconds
seconds on single machine vs code 

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> cd ..       
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> cd 'f:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output'
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> & .\'PrimeNumST.exe'
Single-Threaded: 189961812 primes found up to 4000000000
Time: 475.609 seconds

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrmNumParallel.cpp -o exec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> ./exec             
OpenMP Parallel: 51189037 primes found up to 1000000000
Threads Used: 8
Time: 2.5733 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrmNumParallel.cpp -o exec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> ./exec             
OpenMP Parallel: 455321822 primes found up to 10000000000
Threads Used: 8
Time: 26.6869 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrmNumParallel.cpp -o exec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> ./exec             
OpenMP Parallel: 190279251 primes found up to 400,0,000,000
Threads Used: 8
Time: 10.3733 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrmNumParallel.cpp -o exec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> ./exec             
OpenMP Parallel: 1711984104 primes found up to 4000,0,000,000
Threads Used: 8
Time: 100.88 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> cd 'f:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output'
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> & .\'PrNumMTh.exe'
Multi-Threaded: 50847534 primes found up to 100,0,000,000
Time: 189.043 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> 

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> cd 'f:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output'
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> & .\'PrNumMTh.exe'
Multi-Threaded: 189961812 primes found up to 400,0,000,000
Time: 786.853 seconds

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 455052510 primes found up to 1000,0,000,000
Threads Used: 1 ??
Time: 372.444 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 189961810 primes found up to 4000000000
Threads Used: 1 ??
Time: 117.985 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 


PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 1
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 1
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 1
Threads Used: 1
Time: 372.444 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 189961810 primes found up to 4000000000
Threads Used: 1
Time: 117.985 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=8; .\PrNumMthrPllexec
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 8
Time: 89.5849 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=7; .\PrNumMthrPllexec
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 7
Time: 92.2407 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=12; .\PrNumMthrPllexec
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 12
Time: 86.5817 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=16; .\PrNumMthrPllexec
Parallel (OpenMP): 455052509 primes found up to 10000000000
Threads Used: 16
Time: 90.3403 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 455052509 primes found up to 10000000000
Threads Used: 16
Time: 83.9289 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=8; .\PrNumMthrPllexec 
Parallel (OpenMP): 189961810 primes found up to 4000000000
Threads Used: 8
Time: 32.5304 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=8; .\PrNumMthrPllexec
Parallel (OpenMP): 189961810 primes found up to 4000000000
Threads Used: 8
Time: 32.8301 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=10; .\PrNumMthrPllexec
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 10
Time: 31.615 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=12; .\PrNumMthrPllexec
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 12
Time: 31.097 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 12
Time: 32.6545 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=3; .\PrNumMthrPllexec 
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 3
Time: 42.632 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=4; .\PrNumMthrPllexec
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 4
Time: 39.5737 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=5; .\PrNumMthrPllexec
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 5
Time: 37.9129 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=1; .\PrNumMthrPllexec
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 1
Time: 60.0763 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 1
Time: 61.4759 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=20; .\PrNumMthrPllexec
Parallel (OpenMP): 189961811 primes found up to 4000000000
Threads Used: 20
Time: 31.4253 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 




Device name	DESKTOP-NAF9NIA
Processor	12th Gen Intel(R) Core(TM) i5-12500 (3.00 GHz)
Installed RAM	32.0 GB (31.7 GB usable)
Device ID	910D44DE-668F-4BF4-9E41-D5955B4988CD
Product ID	00331-10000-00001-AA359
System type	64-bit operating system, x64-based processor
Pen and touch	No pen or touch input is available for this display
Edition	Windows 11 Pro
Version	24H2
Installed on	‎1/‎23/‎2025
OS build	26100.4652
Experience	Windows Feature Experience Pack 1000.26100.128.0


PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM> cd .\C_CPP_tests\
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> clang++ -O3 -std=c++17 -fopenmp PrimeNumST.cpp -o PrimeNumST.exe
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> ./PrimeNumST.exe   
Single-Threaded: 189961812 primes found up to 4000000000
Time: 85.9909 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests>](<PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM%3E cd .\C_CPP_tests\
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> clang++ -O3 -std=c++17 -fopenmp PrimeNumST.cpp -o PrimeNumST.exe
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> ./PrimeNumST.exe   
Single-Threaded: 189961812 primes found up to 4000000000
Time: 85.9909 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> ./PrimeNumST.exe
Single-Threaded: 189961812 primes found up to 4000000000
Time: 81.9499 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests>>)

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM> cd 'f:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output'
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> & .\'PrNumMTh.exe'
Multi-Threaded: 189961812 primes found up to 4000000000
Time: 326.46 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> 

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM> cd 'f:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output'
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> & .\'PrNumMTh.exe'
Multi-Threaded 4: 189961812 primes found up to 4000000000
Time: 326.46 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> cd 'f:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output'
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> & .\'PrNumMTh.exe'
Multi-Threaded 12 : 189961812 primes found up to 4000000000
Time: 284.476 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> 


PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> clang++ -O3 -std=c++17 -fopenmp PrNumMTh.cpp -o PrNumMTh.exe
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> ./PrNumMTh.exe
Multi-Threaded 12: 455052511 primes found up to 10000000000
Time: 179.71 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> clang++ -O3 -std=c++17 -fopenmp PrNumMTh.cpp -o PrNumMTh.exe
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> ./PrNumMTh.exe
Multi-Threaded: 189961812 primes found up to 4000000000
Time: 74.2165 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> clang++ -O3 -std=c++17 -fopenmp PrNumMTh.cpp -o PrNumMTh.exe
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> ./PrNumMTh.exe
Multi-Threaded: 12 threads: 189961812 primes found up to 4000000000
Time: 72.7228 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> clang++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec.exe
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec.exe
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 12
Time: 16.5859 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec.exe
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 12
Time: 16.5625 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> clang++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec.exe
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec.exe                                                       
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 12
Time: 16.6553 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec.exe
Parallel (OpenMP): 189961812 primes found up to 4000000000
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> clang++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec.exe
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec.exe
Parallel (OpenMP): 1711955433 primes found up to 40000000000
Threads Used: 12
Time: 201.26 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> clang++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec.exe
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 12
Time: 45.8352 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=8; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 8
Time: 44.903 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=4; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 4
Time: 50.1002 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=4; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 4
Time: 49.2022 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=3; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 3
Time: 53.0658 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=2; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 2
Time: 61.6214 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=1; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 1
Time: 81.5576 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=1; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 1
Time: 81.5566 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=1; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 1
Time: 85.4897 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=2; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 2
Time: 65.9215 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=2; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 2
Time: 65.4062 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=3; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 3
Time: 57.6446 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=3; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 3
Time: 55.5326 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=4; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 4
Time: 50.0391 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=4; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 4
Time: 49.959 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=5; .\PrNumMthrPllexec.exe 
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 5
Time: 48.6285 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=5; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 5
Time: 49.6575 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=6; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 6
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 5
Time: 48.6285 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=5; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 5
Time: 49.6575 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=6; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 6
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 5
Time: 49.6575 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=6; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 6
Threads Used: 5
Time: 49.6575 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=6; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 6
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=6; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 6
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 6
Threads Used: 6
Time: 47.9135 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=6; .\PrNumMthrPllexec.exe
Time: 47.9135 seconds
Time: 47.9135 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=6; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 6
Time: 46.2927 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=8; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 8
Time: 45.1217 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=12; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 12
Time: 45.8011 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=12; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 12
Time: 46.0917 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests>







[[CCGSC Benchmark Test Results]] 
4000000000 on mvp demo v1 with 3 workers took 4 minutes

3 laptops and 2 mobiles 
4000000000 on mvp demo v1 with 8 workers took 2 minutes 23 seconds 
4000000000 on mvp demo v1 with 10 workers took 3 minutes 13 seconds 
4000000000 on mvp demo v1 with 10 workers took 1 minutes 44 seconds 
4000000000 on mvp demo v1 with 10 workers took 2 minutes 13 seconds 
4000000000 on mvp demo v1 with 10 workers took 2 minutes 12 seconds 




Device name	DESKTOP-KD0A63N
Processor	Intel(R) Core(TM) i7-8665U CPU @ 1.90GHz (2.11 GHz)
Installed RAM	48.0 GB (47.7 GB usable)
Device ID	F1968C6F-0CCB-40DE-BB77-C2F36AB17246
Product ID	00330-53024-26684-AAOEM
System type	64-bit operating system, x64-based processor
Pen and touch	No pen or touch input is available for this display

Edition	Windows 11 Pro
Version	24H2
Installed on	‎3/‎22/‎2025
OS build	26100.4652
Experience	Windows Feature Experience Pack 1000.26100.128.0


C/C++ code - 10000000000 was finished in 25, 30, 40, 50, 55, 60 seconds on single machine vs code 



C/C++ code - 10000000000 was finished in 
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output%3E & .\'PrimeNumST.exe'
Single-Threaded: 455052511 primes found up to 10000000000
Time: 1063.71 seconds
seconds on single machine vs code 

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> cd ..       
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> cd 'f:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output'
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> & .\'PrimeNumST.exe'
Single-Threaded: 189961812 primes found up to 4000000000
Time: 475.609 seconds

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrmNumParallel.cpp -o exec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> ./exec             
OpenMP Parallel: 51189037 primes found up to 1000000000
Threads Used: 8
Time: 2.5733 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrmNumParallel.cpp -o exec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> ./exec             
OpenMP Parallel: 455321822 primes found up to 10000000000
Threads Used: 8
Time: 26.6869 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrmNumParallel.cpp -o exec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> ./exec             
OpenMP Parallel: 190279251 primes found up to 400,0,000,000
Threads Used: 8
Time: 10.3733 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrmNumParallel.cpp -o exec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> ./exec             
OpenMP Parallel: 1711984104 primes found up to 4000,0,000,000
Threads Used: 8
Time: 100.88 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> cd 'f:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output'
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> & .\'PrNumMTh.exe'
Multi-Threaded: 50847534 primes found up to 100,0,000,000
Time: 189.043 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> 

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> cd 'f:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output'
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output> & .\'PrNumMTh.exe'
Multi-Threaded: 189961812 primes found up to 400,0,000,000
Time: 786.853 seconds

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 455052510 primes found up to 1000,0,000,000
Threads Used: 1 ??
Time: 372.444 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 189961810 primes found up to 4000000000
Threads Used: 1 ??
Time: 117.985 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 


PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 1
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 1
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 1
Threads Used: 1
Time: 372.444 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 189961810 primes found up to 4000000000
Threads Used: 1
Time: 117.985 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=8; .\PrNumMthrPllexec
Parallel (OpenMP): 455052510 primes found up to 10000000000
Threads Used: 8
Time: 89.5849 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=7; .\PrNumMthrPllexec
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 7
Time: 92.2407 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=12; .\PrNumMthrPllexec
Parallel (OpenMP): 455052511 primes found up to 10000000000
Threads Used: 12
Time: 86.5817 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=16; .\PrNumMthrPllexec
Parallel (OpenMP): 455052509 primes found up to 10000000000
Threads Used: 16
Time: 90.3403 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 455052509 primes found up to 10000000000
Threads Used: 16
Time: 83.9289 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=8; .\PrNumMthrPllexec 
Parallel (OpenMP): 189961810 primes found up to 4000000000
Threads Used: 8
Time: 32.5304 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=8; .\PrNumMthrPllexec
Parallel (OpenMP): 189961810 primes found up to 4000000000
Threads Used: 8
Time: 32.8301 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=10; .\PrNumMthrPllexec
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 10
Time: 31.615 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=12; .\PrNumMthrPllexec
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 12
Time: 31.097 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> g++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 12
Time: 32.6545 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=3; .\PrNumMthrPllexec 
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 3
Time: 42.632 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=4; .\PrNumMthrPllexec
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 4
Time: 39.5737 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=5; .\PrNumMthrPllexec
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 5
Time: 37.9129 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=1; .\PrNumMthrPllexec
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 1
Time: 60.0763 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexec 
Parallel (OpenMP): 189961812 primes found up to 4000000000
Threads Used: 1
Time: 61.4759 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=20; .\PrNumMthrPllexec
Parallel (OpenMP): 189961811 primes found up to 4000000000
Threads Used: 20
Time: 31.4253 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 
Parallel (OpenMP): 2925699539 primes found up to 70000000000
Threads Used: 4
Time: 437.316 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> clang++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec.exe
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=12; .\PrNumMthrPllexec.exe                 
Parallel (OpenMP): 4118054812 primes found up to 100000000000
Threads Used: 12
Time: 574.123 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=8; .\PrNumMthrPllexec.exe 
Parallel (OpenMP): 4118054812 primes found up to 100000000000
Threads Used: 8
exe
exe
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=12; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 8007105058 primes found up to 200000000000
Threads Used: 12
Time: 1219.65 seconds
PS F:\GitHubDesktop\GitHubClo$env:OMP_NUM_THREADS=18; .\PrNumMthrPllexec.exe
Parallel (OpenMP): 8007105058 primes found up to 200000000000
Threads Used: 18
Time: 1155.44 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> $env:OMP_NUM_THREADS=18; .\PrNumMthrPllexec.exe
 *  History restored 

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM> cd 'f:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests\output'
 *  History restored 

PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM> clang++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec.exe
clang++: error: no such file or directory: 'PrNumMthrPrll.cpp'
clang++: error: no input files
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM> cd .\C_CPP_tests\
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> clang++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexecOFFICE.exe
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexecOFFICE.exe     
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM> clang++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexec.exe
clang++: error: no such file or directory: 'PrNumMthrPrll.cpp'
clang++: error: no input files
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM> cd .\C_CPP_tests\
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> clang++ -O3 -std=c++17 -fopenmp -march=native PrNumMthrPrll.cpp -o PrNumMthrPllexecOFFICE.exe
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> .\PrNumMthrPllexecOFFICE.exe                                                                 
Parallel (OpenMP): 8007105058 primes found up to 200000000000
Threads Used: 12
Time: 1098.98 seconds
PS F:\GitHubDesktop\GitHubCloneFiles\Webassembly\CCGS_WASM\C_CPP_tests> 


[[CCGSC Benchmark Test Results]]

[[CCGSC Test11 Bench-marking prime_distributed_projectPrlCc1B (Dev)]]  open with txt or notepad
[[CCGSC Test22 Bench-marking prime_distributed_projectPrlCc1B (Dev)]] open with txt or notepad
[[CCGSC Test33 Bench-marking prime_distributed_projectPrlCc1B (Dev)]] open with txt or notepad
[[CCGSC Test34B Bench-marking prime_distributed_projectPrlCc1B (Dev)]] open with txt or notepad
[[CCGSC Test34ABC Bench-marking prime_distributed_projectPrlCc1B (Dev)]] open with txt or notepad
[[CCGSC Test35ABC Bench-marking prime_distributed_projectPrlCc1B (Dev)]] open with txt or notepad
[[CCGSC Test335ABC Bench-marking prime_distributed_projectPrlCc1B (Dev)]] open with txt or notepad
[[CCGSC Test345ABC Bench-marking prime_distributed_projectPrlCc1B (Dev)]] open with txt or notepad

[[CCGSC Test37A Bench-marking prime_distributed_projectPrlCc1B (Dev).txt]]
[[CCGSC Test37BB Bench-marking prime_distributed_projectPrlCc1B (Dev).txt]]


[[CCGSC Test38A Bench-marking prime_distributed_projectPrlCc1B (Dev).txt]]


[[CCGSC Test38ABC 3 Pages Bench-marking prime_distributed_projectPrlCc1B (Dev).txt]]

