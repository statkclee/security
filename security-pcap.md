# xwMOOC 안전한 R
 


## 1. `pcap` 파일 합치기 [^merge-pcap]

[^merge-pcap]: [D.8. mergecap: Merging multiple capture files into one](https://www.wireshark.org/docs/wsug_html_chunked/AppToolsmergecap.html)

다수 `.pcap` 파일이 존재할 경우 데이터 분석을 위해서 이를 하나로 병합하는 것이 유용할 수 있다.
이런 경우 `mergecap` 명령어를 사용한다. 즉, `dhcp-capture.pcapng`, `imap-1.pcapng` 파일을 합쳐서 
`outfile.pcapng` 출력파일로 저장하는 명령어는 다음과 같다.


```r
$ mergecap -w outfile.pcapng dhcp-capture.pcapng imap-1.pcapng
```
