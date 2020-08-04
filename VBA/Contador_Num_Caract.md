    Dim texto As String
    Dim letra As String
    Dim contador As Integer

    x = Timer

    texto = 1234445

    For i = 1 To Len(texto)
        letra = Mid(texto, i, 1)
    
        If letra = 4 Then
            contador = contador + 1
        End If
    Next

    MsgBox (contador)
