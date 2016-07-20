---
layout: post
title: 使用Python转换Excel单元格
category: tech
guid:
tags: [Python]

---
{% include JB/setup %}

使用Python将Excel中的每个非第一行、第一列的单元格转换成`{'name': rowIndex_colIndex, 'value': value, 'row_header': '', 'col_header':'', 'id':''}`的形式,代码如下:

<pre>
<code class="Python">

# -*- coding:utf-8 -*-
'''
使用Python处理Excel文件
required:
  openpyxl
'''
import time
count = 0
ts = int(time.time())

def int2base(x, base):
  import string
  digs = string.digits + string.letters
  
  if x < 0: 
    sign = -1
  elif x == 0: 
    return digs[0]
  else: 
    sign = 1
  
  x *= sign
  digits = []
  while x:
    digits.append(digs[x % base])
    x /= base
  if sign < 0:
    digits.append('-')
  digits.reverse()
  return ''.join(digits)

def genId():
  global count
  global ts
  cts = int(time.time())
  if cts == ts:
    count += 1
  else:
    count = 0
    ts = cts
  
  return int2base(ts,36) + '_' + int2base(count, 36)


def readExcelToGrid(file_path, header=True):
  """
  读取excel文件中的单元格到Grid列表中, 除去第一行和第一列
  网格的编号从1,1开始, 即B2其编号为1_1
  """
  from openpyxl import Workbook, load_workbook
  import re
  
  ptn = re.compile(".*(indoor|outdoor).*")
  wb = load_workbook(file_path, data_only=True)
  
  grids = [['id', 'group_type', 'group_name', 'group_value', 'subject_name', 'subject_value']]  
  
  for sheet_name in wb.get_sheet_names(): 
    sht = wb.get_sheet_by_name(sheet_name)
    for row in sht.rows:
      for cell in row:
        id = genId()
        group = sheet_name
        subject_name = str(cell.row - 1) + '_' + str(cell.col_idx - 1)
        subject_value = ''
        
        percent_flag = False
        
        if cell.data_type == 's':
          subject_value = cell.value.encode('utf-8')
        elif cell.data_type == 'n':
          if cell.value <= 1:
            percent_flag = True
          
          subject_value = str(cell.value)
        
        if percent_flag and ptn.match(sheet_name):
          subject_value += ',0,0,1'
        
        grids.append([id, group, subject_name, subject_value])
    
  return grids
  


def writeExcelFromGridArray(grids, output_path):
  from openpyxl import Workbook
    
  wb = Workbook()
  ws = wb.active
  
  for grid in grids:
    ws.append(grid)
    
  wb.save(output_path)


def main():
  file_path = 'grid_raw.xlsx'
  writeExcelFromGridArray(grids, 'grid.xlsx')
  

if __name__ == '__main__':
  main()
  
</code>
</pre>



