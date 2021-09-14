from openpyxl import workbook
import requests
import re 
import openpyxl

import xlsxwriter
from tqdm import tqdm
url_header = "https://www.ncbi.nlm.nih.gov/sra/?term="

gsm_source_file = input("Enter the input filename(.xlsx): ")
gsm_source_path = input("Enter the input file directory: ")
row = int(input("Enter the number of row: "))
gsm_sheet_name = ""

def getSRX(GSM_index):
    url = url_header+GSM_index
    try:
        content = requests.get(url).text 
        m = re.search("SRX[0-9]+", content)
        srx = (m.group(0))
        return srx
    except:
        return ""  

def getSRR(SRX_index):
    url = url_header+SRX_index
    try:
        # print("start fetching data")
        content = requests.get(url).text
        # print("fetching data finished") 
        m = re.findall("SRR[0-9]+", content)
        srr = (m.group(0))
        return srr
    except:
        return ""  

# print(getSRR("SRX1025880"))

def getLibrary(SRX_index):
    url = url_header+SRX_index
    try:
        content = requests.get(url).text 
        m = re.search("Layout:\ <span>(.*)<\/span><\/div><div>", content)
        library = (m.group(1))
        return library
    except:
        return ""  



def processGSMList(gsm_source, gsm_target):
    wb_obj = openpyxl.load_workbook(gsm_source)
    sheet = wb_obj['sheet1']
    srx_values_texts = []
    srr_values_texts = []
    library_values_texts = []
    workbook = xlsxwriter.Workbook(gsm_target)
    worksheet = workbook.add_worksheet()
    for i in tqdm(range(2,row)):
        cell_name = "A" + str(i)
        cell_value = sheet[cell_name].value
        
        srx_values_texts = getSRX(cell_value)
        library_values_texts = getLibrary(cell_value)
        srr_values = getSRR(cell_value)
        srr_values_texts = ";".join(srr_values)

        # print(srx_values_texts)
        # print(library_values_texts)
        # print(type(srr_values_texts))


        worksheet.write(i-2,0,cell_value)
        worksheet.write(i-2,1,srx_values_texts)
        worksheet.write(i-2,2,library_values_texts)

    workbook.close()

        
    
processGSMList(gsm_source_path+"/"+gsm_source_file, "SRAfinder_output.xlsx")

