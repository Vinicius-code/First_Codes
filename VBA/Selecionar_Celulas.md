'SELECIONAR E MUDAR VALOR

Range("A1").Select
Range("A1").Value = "Minha Linda"


 
'COPIAR COLAR

Range("A1:A3").Select
Selection.Copy
Range("B1").Select
Activesheet.paste



'SELECIONAR COM VARIÁVEL

linha = Range("E1").Value
Cells(linha,coluna).Value = "Minha Linda"

Cells(linha, 1).Value = "Minha Linda"



'SELECIONAR VÁRIAS CÉLULAS

Sheets("Plan1").Select
For Each celula In Range("B2:G6")
	celula.Value = "Minha Linda"
Next
