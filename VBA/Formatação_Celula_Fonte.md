Range("A1").Select

With Selection.
	Font.Bold = True
	Font.Italic = True
End With


With Selection.
	Font.Name = "Arial"
End With

----OU----

Range("A1").Select
Selection.Font.Name = "Arial"
