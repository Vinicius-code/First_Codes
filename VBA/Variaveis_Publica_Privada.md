
'Declara uma variável para usar em outras macros
'Private = Só pode ser usado dentro do módulo
'Public = Pode ser usado em toda a pasta de trabalho

    Private myVariable1 As Double
    Const myName As String = "Daniel Strong, cool dude"

    Sub MyExample1()
    myVar = 50
    MsgBox myVar

'Chama uma outra macro dentro do mesmo módulo

    Call myVariableDec

    MsgBox myVariable1
    End Sub

-------------

    Sub myVariableDec()
    Dim hi As String
    Dim hello As Double
    Dim myDate1 As Date

    hi = "Hello World!"

'Variável declarada em outra macro, mas pode ser usada

    myVariable1 = 634.85
    myDate1 = "12/31/2014"
    MsgBox myName
    End Sub
