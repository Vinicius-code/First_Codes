'Puxar fórmula SOMASES
#Célula_Final.Value = WorksheetFunction.SumIfs(Intervalo_Soma, Intervalo_Critérios, Critério)

Range("H2").Value = WorksheetFunction.SumIfs(Range("D2:D3"), Range("C2:C3"), Range("G2"))
