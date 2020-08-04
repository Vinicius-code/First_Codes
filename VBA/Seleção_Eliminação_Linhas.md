'SELECIONAR A ÚLTIMA LINHA EM UMA COLUNA

Sheets("Plan1").Select
linha = Range("A1048576").End(x1Up).Row
Cells(linha,1).Value = "Karyna"



'REMOVER LINHAS VAZIAS

Range("A:A").Select
 
 Selection.SpecialCells(xlCellTypeBlanks).Select
 Selection.EntireRow.Delete
 Range("a1").Select
