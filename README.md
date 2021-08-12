# Safra
import time
import csv
with open('Bases/teste3.csv/teste.csv', 'r') as inp, open('Bases/teste5 '+time.strftime("%Y%m%d-%H%M%S")+'.txt', 'w') as out:
    for line in inp:
        line = line.replace(',', ':')
        out.write(line)
