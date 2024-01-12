Per the instructions at https://pdos.csail.mit.edu/6.828/2014/tools.html,
I'm going to have to build my own toolchain.

Installing via yum isn't working, so I'll be manually uploading files here.

Also, trying to compile was throwing absense of gcc errors:

```
[ec2-user@ip-172-31-16-160 build]$ ../configure --prefix=/usr/local \
    --target=i386-jos-elf --disable-werror \
    --disable-libssp --disable-libmudflap --with-newlib \
    --without-headers --enable-languages=c
checking build system type... x86_64-unknown-linux-gnu
checking host system type... x86_64-unknown-linux-gnu
checking target system type... i386-jos-elf
checking for a BSD-compatible install... /usr/bin/install -c
checking whether ln works... yes
checking whether ln -s works... yes
checking for a sed that does not truncate output... /usr/bin/sed
checking for gawk... gawk
checking for gcc... no
checking for cc... no
checking for cl.exe... no
configure: error: in `/home/ec2-user/mit6.828/Building_Compiler_Toolchain/gcc-4.6.1/build':
configure: error: no acceptable C compiler found in $PATH
See `config.log' for more details.
[ec2-user@ip-172-31-16-160 build]$ gcc --versiom
-bash: gcc: command not found
```

So I had to install gcc manally:

`[ec2-user@ip-172-31-16-160 /]$ sudo yum install gcc`

See these docs for why I didn't expect to need to install gcc:
https://docs.aws.amazon.com/linux/al2023/ug/c-cplusplus.html
And this stackoverflow post for some poor sap who apparently already had gcc:
https://stackoverflow.com/questions/25092009/amazon-linux-gcc-command-not-found
And finally this output from my gcc install:

```
[ec2-user@ip-172-31-16-160 /]$ sudo yum install gcc
Last metadata expiration check: 8:44:12 ago on Thu Jan 11 19:01:47 2024.
Dependencies resolved.
================================================================================
 Package               Arch      Version                   Repository      Size
================================================================================
Installing:
 gcc                   x86_64    11.4.1-2.amzn2023.0.2     amazonlinux     32 M
Installing dependencies:
 annobin-docs          noarch    10.93-1.amzn2023.0.1      amazonlinux     92 k
 annobin-plugin-gcc    x86_64    10.93-1.amzn2023.0.1      amazonlinux    887 k
 cpp                   x86_64    11.4.1-2.amzn2023.0.2     amazonlinux     10 M
 gc                    x86_64    8.0.4-5.amzn2023.0.2      amazonlinux    105 k
 glibc-devel           x86_64    2.34-52.amzn2023.0.7      amazonlinux     45 k
 glibc-headers-x86     noarch    2.34-52.amzn2023.0.7      amazonlinux    446 k
 guile22               x86_64    2.2.7-2.amzn2023.0.3      amazonlinux    6.4 M
 kernel-headers        x86_64    6.1.66-93.164.amzn2023    amazonlinux    1.4 M
 libmpc                x86_64    1.2.1-2.amzn2023.0.2      amazonlinux     62 k
 libtool-ltdl          x86_64    2.4.7-1.amzn2023.0.3      amazonlinux     38 k
 libxcrypt-devel       x86_64    4.4.33-7.amzn2023         amazonlinux     32 k
 make                  x86_64    1:4.3-5.amzn2023.0.2      amazonlinux    534 k

Transaction Summary
================================================================================
Install  13 Packages

Total download size: 52 M
Installed size: 168 M
Is this ok [y/N]: y
Downloading Packages:
(1/13): libmpc-1.2.1-2.amzn2023.0.2.x86_64.rpm  957 kB/s |  62 kB     00:00    
(2/13): libtool-ltdl-2.4.7-1.amzn2023.0.3.x86_6 554 kB/s |  38 kB     00:00    
(3/13): kernel-headers-6.1.66-93.164.amzn2023.x  15 MB/s | 1.4 MB     00:00    
(4/13): gc-8.0.4-5.amzn2023.0.2.x86_64.rpm      3.1 MB/s | 105 kB     00:00    
(5/13): make-4.3-5.amzn2023.0.2.x86_64.rpm       19 MB/s | 534 kB     00:00    
(6/13): annobin-plugin-gcc-10.93-1.amzn2023.0.1  16 MB/s | 887 kB     00:00    
(7/13): glibc-devel-2.34-52.amzn2023.0.7.x86_64 2.9 MB/s |  45 kB     00:00    
(8/13): cpp-11.4.1-2.amzn2023.0.2.x86_64.rpm     46 MB/s |  10 MB     00:00    
(9/13): libxcrypt-devel-4.4.33-7.amzn2023.x86_6 403 kB/s |  32 kB     00:00    
(10/13): guile22-2.2.7-2.amzn2023.0.3.x86_64.rp  27 MB/s | 6.4 MB     00:00    
(11/13): annobin-docs-10.93-1.amzn2023.0.1.noar 1.5 MB/s |  92 kB     00:00    
(12/13): glibc-headers-x86-2.34-52.amzn2023.0.7  11 MB/s | 446 kB     00:00    
(13/13): gcc-11.4.1-2.amzn2023.0.2.x86_64.rpm    62 MB/s |  32 MB     00:00    
--------------------------------------------------------------------------------
Total                                            60 MB/s |  52 MB     00:00     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                        1/1 
  Installing       : libmpc-1.2.1-2.amzn2023.0.2.x86_64                    1/13 
  Installing       : cpp-11.4.1-2.amzn2023.0.2.x86_64                      2/13 
  Installing       : glibc-headers-x86-2.34-52.amzn2023.0.7.noarch         3/13 
  Installing       : annobin-docs-10.93-1.amzn2023.0.1.noarch              4/13 
  Installing       : gc-8.0.4-5.amzn2023.0.2.x86_64                        5/13 
  Installing       : libtool-ltdl-2.4.7-1.amzn2023.0.3.x86_64              6/13 
  Installing       : guile22-2.2.7-2.amzn2023.0.3.x86_64                   7/13 
  Installing       : make-1:4.3-5.amzn2023.0.2.x86_64                      8/13 
  Installing       : kernel-headers-6.1.66-93.164.amzn2023.x86_64          9/13 
  Installing       : libxcrypt-devel-4.4.33-7.amzn2023.x86_64             10/13 
  Installing       : glibc-devel-2.34-52.amzn2023.0.7.x86_64              11/13 
  Installing       : gcc-11.4.1-2.amzn2023.0.2.x86_64                     12/13 
  Running scriptlet: gcc-11.4.1-2.amzn2023.0.2.x86_64                     12/13 
  Installing       : annobin-plugin-gcc-10.93-1.amzn2023.0.1.x86_64       13/13 
  Running scriptlet: annobin-plugin-gcc-10.93-1.amzn2023.0.1.x86_64       13/13 
  Verifying        : kernel-headers-6.1.66-93.164.amzn2023.x86_64          1/13 
  Verifying        : libmpc-1.2.1-2.amzn2023.0.2.x86_64                    2/13 
  Verifying        : libtool-ltdl-2.4.7-1.amzn2023.0.3.x86_64              3/13 
  Verifying        : cpp-11.4.1-2.amzn2023.0.2.x86_64                      4/13 
  Verifying        : gc-8.0.4-5.amzn2023.0.2.x86_64                        5/13 
  Verifying        : guile22-2.2.7-2.amzn2023.0.3.x86_64                   6/13 
  Verifying        : make-1:4.3-5.amzn2023.0.2.x86_64                      7/13 
  Verifying        : annobin-plugin-gcc-10.93-1.amzn2023.0.1.x86_64        8/13 
  Verifying        : glibc-devel-2.34-52.amzn2023.0.7.x86_64               9/13 
  Verifying        : libxcrypt-devel-4.4.33-7.amzn2023.x86_64             10/13 
  Verifying        : gcc-11.4.1-2.amzn2023.0.2.x86_64                     11/13 
  Verifying        : annobin-docs-10.93-1.amzn2023.0.1.noarch             12/13 
  Verifying        : glibc-headers-x86-2.34-52.amzn2023.0.7.noarch        13/13 

Installed:
  annobin-docs-10.93-1.amzn2023.0.1.noarch                                      
  annobin-plugin-gcc-10.93-1.amzn2023.0.1.x86_64                                
  cpp-11.4.1-2.amzn2023.0.2.x86_64                                              
  gc-8.0.4-5.amzn2023.0.2.x86_64                                                
  gcc-11.4.1-2.amzn2023.0.2.x86_64                                              
  glibc-devel-2.34-52.amzn2023.0.7.x86_64                                       
  glibc-headers-x86-2.34-52.amzn2023.0.7.noarch                                 
  guile22-2.2.7-2.amzn2023.0.3.x86_64                                           
  kernel-headers-6.1.66-93.164.amzn2023.x86_64                                  
  libmpc-1.2.1-2.amzn2023.0.2.x86_64                                            
  libtool-ltdl-2.4.7-1.amzn2023.0.3.x86_64                                      
  libxcrypt-devel-4.4.33-7.amzn2023.x86_64                                      
  make-1:4.3-5.amzn2023.0.2.x86_64                                              

Complete!
```






