USRP 
=========

Environment setup:
1. [install GNU radio first](https://github.com/gnuradio/gnuradio) and it will install UHD from source code (the latest version).
    - to reinstall gnu radio: `pybombs remove uhd`  
    - sometimes an "assertion error" may happen. that's because of the incompatbility of different yaml library versions. reinstall the environment using requirements.txt.
    - default directory: `~/prefix/default/share/gnuradio/examples/uhd/usrp_spectrum_sense.py`
    - gnu radio installation issues:
        - qt errors => reinstall qt
        - boost errors = > i use ubuntu 18 which come with boost 1.65
        - for each re-installation, update the pybombs from github and manually clean and refetch
            ```
            pip install git+https://github.com/gnuradio/pybombs.git
            sudo rm /usr/local/src/gnuradio -rf
            sudo pybombs -v fetch gnuradio
            sudo pybombs install gr-gsm
            ```

2. run `sudo apt-get install libuhd-dev` to install uhd-dev. 


Common issues: 
1. Cannot import gnuradio error in python
    - try python 2.7
    - If you install via pybombs there is a “activate” script inside the prefix. Make sure to source that first. For the assertion error: instead of pip install pybombs, git clone it and sudo pip install it. 

[USRP Hardware Driver and USRP Manual](https://files.ettus.com/manual/page_usrp_x3x0.html)


[Update USRP FPGA](https://files.ettus.com/manual/page_usrp_x3x0.html)

[configure gcc version](https://gist.github.com/application2000/73fd6f4bf1be6600a2cf9f56315a2d91)
[update boost version1](https://askubuntu.com/questions/397939/how-to-uninstall-boost-1-49-and-install-boost-1-54-in-ubuntu)
[update boost version - better post](https://ubuntuforums.org/showthread.php?t=2363177)

`sudo apt-get --purge remove gcc-4.9`

`gnuradio-companion`
`pybombs run gnuradio-companion`


[USRP Bandwidth: analog, processing, network](https://kb.ettus.com/About_USRP_Bandwidths_and_Sampling_Rates)

Common commands:

`cd /home/kim/uhd/host/build/examples`
1. `uhd_find_devices` find connected USRP devices.
2. `uhd_usrp_probe --args addr=192.168.10.32` verify if the USRP works.
3. `sudo ./rx_samples_to_file --args="addr0=192.168.10.31" --type=float --ant=TX/RX --freq=2450e6 --rate=1e5 --file="/home/kim/Desktop/t_1min_1e5.dat" --duration 60`
    -  `./rx_samples_to_file --args="addr0=192.168.10.32" --type=short --ant=TX/RX --freq=2470e6 --rate=20e6 --file="2470-rotation-emptybottle.dat" --duration 5`
4. `sudo ./rx_multi_samples --args="addr0=192.168.10.31" --subdev "A:0 B:0" --channels "0,1"`
5. `sudo ./rx_samples_to_file --args="addr0=192.168.10.31" --type=float --ant=TX/RX --freq=2450e6 --rate=1e5 --file="/home/kim/Desktop/t_1min_1e5.dat" --duration 60 --ref=external`
6. Two antenna on the same usrp: `./rx_multi_receive --args="addr0=192.168.10.31" --gain 30 --ant "TX/RX, RX2" --subdev "A:0 B:0" --channels "0,1"  --prefix="nothing"   --type=float --freq=2450e6 --rate=1e5  --duration 30 `
    - if the two ports are on the same channel, the 2nd port will not work.
7. Use RX2 in the usrp: `./rx_multi_receive --args="addr0=192.168.10.31" --gain 30 --ant "RX2" --subdev "A:0" --channels "0"  --prefix="nothing"   --type=float --freq=2450e6 --rate=1e5  --duration 30`
8. Two usrps one antenna each: `./rx_multi_receive --args="addr0=192.168.10.31,addr1=192.168.10.32" --gain 30 --subdev "A:0 B:0" --channels "0"  --prefix="nothing"   --type=float --freq=2450e6 --rate=1e5    --duration 30 --ref=external`
9. One USRP one antenna: `./rx_multi_receive --args="addr0=192.168.10.31" --gain 30 --ant "TX/RX" --subdev "A:0" --channels "0"  --prefix="nothing"   --type=float --freq=2450e6 --rate=1e5  --duration 30`
folder: `/home/kim/uhd.20180601144807/host/build/examples`
10. Two usrp one antenna each, continuous signals: `./rx_multi_receive --args="addr0=192.168.10.31,addr1=192.168.10.32" --gain 0 --subdev "A:0" --channels "0,1"  --prefix="nothing"  --ant="TX/RX,TX/RX"   --type=float --freq=2450e6 --rate=1e5    --ref=external`  
11. `./rx_multi_receive --args="addr0=192.168.10.31,addr1=192.168.10.32" --gain 0 --subdev "A:0" --channels "0,1"  --prefix="nothing"  --ant="TX/RX,TX/RX"   --type=float --freq=2450e6 --rate=1e5    --ref=external`
12. Three usrp one antenna each, countuous signals (Note that only USRPs of the same type can be combined.): `./rx_multi_receive --args="addr0=192.168.10.31,addr1=192.168.10.32,addr2=192.168.10.8" --gain 0 --subdev "A:0" --channels "0,1,2"  --prefix="nothing"  --ant="TX/RX,TX/RX,TX/RX"  --type=float --freq=2450e6 --rate=1e5    --ref=external`


```
ping 192.168.10.31

```

Nov. 25 command:
1. `./rx_multi_receive --args="addr0=192.168.10.31,addr1=192.168.10.32" --gain 0 --subdev "A:0" --channels "0,1"  --prefix="nothing"  --ant="TX/RX,TX/RX"   --type=float --freq=2444e6 --rate=10e6    --ref=external`

Oct. 1 night command:
1. `./rx_multi_receive --args="addr0=192.168.10.31,addr1=192.168.10.32" --gain 0 --subdev "A:0" --channels "0,1"  --prefix="nothing"  --ant="TX/RX,TX/RX"   --type=float --freq=2450e6 --rate=1e6    --ref=external`

0812 command:
1. `./rx_samples_to_file --args="addr0=192.168.10.32" --type=float --ant=TX/RX --freq=2450e6 --rate=1e5 --file="an1noantenuate.dat" --gain 0 --duration 3`
2. `./rx_multi_receive --args="addr0=192.168.10.32" --gain 0 --subdev "A:0" --channels "0"  --prefix="nothing"   --type=float --freq=2450e6 --rate=1e5    --ref=external`

Dev: 

1. `cd ~/uhd/host/build; cmake ..` to compile the cpp files into executables
2. Executables would be at `~/uhd/host/build/examples`
3. THe source files are at `~/uhd/host/examples`
4. [complete guide](https://kb.ettus.com/Getting_Started_with_UHD_and_C%2B%2B)


`scp kim@128.237.112.106:~/projects/microwave/usrpcode/*.dat .`


`matlab -softwareopengl`
`close all`






 plot(abs(x_1))
K>> plot(abs(fftshift(fft(x_1))))
K>> spectrogram(x_1,128,64,[],10,'yaxis","center")
 spectrogram(x_1,128,64,[],10,'yaxis","center")
                              ↑
Error: Character vector is not terminated properly.
 
K>> spectrogram(x_1,128,64,[],10,'y-axis","center")
 spectrogram(x_1,128,64,[],10,'y-axis","center")
                              ↑
Error: Character vector is not terminated properly.
 
K>> spectrogram(x_1)
K>> 


>> spectrogram((static0(7150:7250)),96,50,[],10,'yaxis','center');
>> spectrogram((static0(7000:7500)),128,64,[],10,'yaxis','center');
>> plot(abs(fft(static0(7150:7250))))
>> plot(abs(fft(static0(6950:7050))))
>> figure;
>> plot(abs(fft(static0(7150:7250))))
>> figure; 
>> spectrogram((static0(1:8000)),128,64,[],10,'yaxis','center');
plot(angle(static0(1:8000)./static1(1:8000)))

 align_two_signals(part0(:,1), part1(:,1))

filter_usrp_signal(static0, 1, 1e5, true);

shell script: 

cd /home/kim/uhd/host/build/examples
sudo ./rx_samples_to_file --args="addr0=192.168.10.31" --type=float --ant=TX/RX --freq=2450e6 --rate=1e5 --file="/home/kim/Desktop/$1-1e5-31.dat" --duration 60 --ref=external & 
sudo ./rx_samples_to_file --args="addr0=192.168.10.32" --type=float --ant=TX/RX --freq=2450e6 --rate=1e5 --file="/home/kim/Desktop/$1-1e5-32.dat" --duration 60 --ref=external

zxc







one usrp, two ports

 ./rx_multi_receive --args="addr0=192.168.10.31" --gain 30 --subdev "A:0 B:0" --channels "0,1"  --prefix="nothing"   --type=float --freq=2450e6 --rate=1e5  --duration 30




 ##### LimeSDR

```
#make sure that STREAM is one of the available connections
LimeUtil --info

#now run LimeUtil with --find to locate devices on the system
LimeUtil --find

 #make sure that lime is one of the available factories 
SoapySDRUtil --info

#now run SoapySDRUtil with --find to locate devices on the system
SoapySDRUtil --find="driver=lime"
```


#### HackerRF & GNU Radio

0. [uhd binary install](https://files.ettus.com/manual/page_install.html)
1. sudo apt-get install gr-osmosdr
2. sudo apt-get install hackrf-tools
3. hackrf_info
4. sudo apt-get install gnuradio