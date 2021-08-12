# Safra
import time
import csv
from glob import glob
with open((glob('Bases/teste3.csv/*.csv')[0]), 'r') as inp, open('Bases/teste5 '+time.strftime("%Y%m%d %H%M%S")+'.txt', 'w') as out:
    for line in inp:
        line = line.replace(',', ':')
        out.write(line)
