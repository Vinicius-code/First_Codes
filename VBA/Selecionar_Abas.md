 'SELECIONAR VÁRIAS ABAS

	For Each aba in ThisWorkbook.Sheets
		If aba.Name <> "Instruções" Then
			aba.Select
			Range("H5").Value = "Karyna"
		End If
	Next
 
