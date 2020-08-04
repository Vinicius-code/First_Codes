A = 80000

B = 200000

anos = 0

txA = 0.03

txB = 0.015

'Soma +1 ano a cada vez que o Loop ocorre

While A < B
  
  anos = anos + 1
  A = A + (A * txA)
  B = B + (B * txB)

Wend

Range("A13").Value = A
Range("A14").Value = B
Range("A15").Value = anos
