# xwMOOC 안전한 R
 


## 1. `pcap` 파일 합치고 쪼개고 [^merge-split-pcap]

### 1.1. `pcap` 파일 병합 [^merge-pcap]

[^merge-pcap]: [D.8. mergecap: Merging multiple capture files into one](https://www.wireshark.org/docs/wsug_html_chunked/AppToolsmergecap.html)

다수 `.pcap` 파일이 존재할 경우 데이터 분석을 위해서 이를 하나로 병합하는 것이 유용할 수 있다.
이런 경우 `mergecap` 명령어를 사용한다. 즉, `dhcp-capture.pcapng`, `imap-1.pcapng` 파일을 합쳐서 
`outfile.pcapng` 출력파일로 저장하는 명령어는 다음과 같다.


```r
$ mergecap -w outfile.pcapng dhcp-capture.pcapng imap-1.pcapng
```

### 1.2. `pcap` 파일 쪼개기 [^split-pcap]

[^split-pcap]: [how to split a pcap file into a set of smaller ones](https://serverfault.com/questions/131872/how-to-split-a-pcap-file-into-a-set-of-smaller-ones)

매우 커다란 `.pcap` 파일이 패킷을 캡쳐하여 담고 있는 경우, 분석을 위해서 혹은 필요한 데이터만 끄집어 내기 위해서 `.pcap` 파일을 쪼갤 필요가 있다.
이런 경우 `tcpdump` 명령어를 사용한다. 


```r
$ tcpdump -r target_file -w splitted_files -C 100
```
- `-r` : 목표가 되는 크기가 큰 `.pcap` 파일
- `-w` : 커다란 `.pcap` 파일이 쪼개서 저장될 파일명
- `-C` : 얼마 단위로 쪼갤지 결정할 크기 - 100 MB

다음 명령어는 `Office.pcapng` 1GB 파일을 100MB 기준으로 10조각 내게 된다. 


```r
$ tcpdump -r Office.pcapng -w office_test.pcap -C 100
reading from file Office.pcapng, link-type E
$ ls -alh
total 1.9G
drwxr-xr-x 1 rstudio rstudio    0 Sep  5 01:26 .
drwxr-xr-x 1 rstudio rstudio    0 Aug 29 07:48 ..
-rwxr-xr-x 1 rstudio rstudio  96M Sep  5 01:30 office_test.pcap
-rwxr-xr-x 1 rstudio rstudio  96M Sep  5 01:30 office_test.pcap1
-rwxr-xr-x 1 rstudio rstudio  96M Sep  5 01:30 office_test.pcap2
-rwxr-xr-x 1 rstudio rstudio  96M Sep  5 01:30 office_test.pcap3
-rwxr-xr-x 1 rstudio rstudio  96M Sep  5 01:30 office_test.pcap4
-rwxr-xr-x 1 rstudio rstudio  96M Sep  5 01:30 office_test.pcap5
-rwxr-xr-x 1 rstudio rstudio  96M Sep  5 01:30 office_test.pcap6
-rwxr-xr-x 1 rstudio rstudio  96M Sep  5 01:30 office_test.pcap7
-rwxr-xr-x 1 rstudio rstudio  96M Sep  5 01:31 office_test.pcap8
-rwxr-xr-x 1 rstudio rstudio  76M Sep  5 01:31 office_test.pcap9
-rwxr-xr-x 1 rstudio rstudio 954M Sep  5 01:26 Office.pcapng
```

## 2. `tshark` 설치 [^install-tshark]

[^install-tshark]: [How to install tshark on Ubuntu 14.10 (Utopic Unicorn)](https://www.howtoinstall.co/en/ubuntu/utopic/tshark)


```r
$ sudo apt-get update
$ sudo apt-get install tshark
```

