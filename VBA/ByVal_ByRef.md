Sub CallingSub()

      a = 10
      b = 20
      CalledSub a, b

    MsgBox a
    MsgBox b

End Sub
________
Sub CalledSub(ByRef y, ByVal z)

    y = 100

    MsgBox y
    MsgBox z
    
End Sub
________
    ByVal = dentro da macro, a referencia usada, substituirá a da mesma Sub. Nesse caso z = b
    ByRef = o inverso da ByVal. Nesse caso a = y
