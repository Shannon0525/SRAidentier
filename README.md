# SRAfinder
Use crawler to quickly obtain SRAid based on GEOid
This tool is used to get SRA information use GSM number. There are some requests to use it:

1. The input file must be xlsx file, and the sheet contains GSM number must be named as "sheet1".

2. Several python packages are necessary, including `openpyxl`, `requests`, `xlsxwriter`. These packages can be installed via command `python3 install -r requirements.txt`.

3. Put the GSM number file and the python file into same directory.

Currently it can only get SRXid,SRRid and layout.

