#### Sub ProcurarPastas()

    Dim wb As Workbook, ws As Worksheet

'Função necessária para o VBA entender o objeto como um Arquivo (Folder)

    Set fso = CreateObject("Scripting.FileSystemObject")

'Aqui vai ficar o caminho da pasta, basta ir em propriedades e copiaR

    Set fldr = fso.GetFolder("C:\Users\Vinicius Machado\Downloads\Excel\VBA\The excel ultimatem programmer\Temp\")

'Deletar os dados da planilha para atualização

    ThisWorkbook.Sheets("sheet1").Range(Cells(2, 1), Cells(Rows.Count, 6)).Delete

'Método para encontrar a última linha

    y = ThisWorkbook.Sheets("Sheet1").Cells(Rows.Count, 1).End(xlUp).Row + 1

'Aqui começa o Loop dentro da pasta pelos arquivos

    For Each wbFile In fldr.Files

        'O tipo de arquivo tem que ser xlsx (Excel files)

        If fso.GetExtensionName(wbFile.Name) = "xlsx" Then

          'Vai abrir temporariamente o arquivo

          Set wb = Workbooks.Open(wbFile.Path)

          'Fará o loop dentro do arquivo aberto
          For Each ws In wb.Sheets
              wsUL = ws.Cells(Rows.Count, 1).End(xlUp).Row

              'Aqui você pode colocar as colunas do arquivo. Sendo sempre fixa, basta alterar com o editor de texto do VBA
              For x = 2 To wsUL
                ThisWorkbook.Sheets("sheet1").Cells(y, 1) = ws.Cells(x, 1) 'col 1
                ThisWorkbook.Sheets("sheet1").Cells(y, 2) = CDate(ws.Cells(x, 2)) 'col 2 CDate para manter formatação data
                ThisWorkbook.Sheets("sheet1").Cells(y, 3) = ws.Cells(x, 3) 'col 3
                ThisWorkbook.Sheets("sheet1").Cells(y, 4) = ws.Cells(x, 4) 'col 4
                ThisWorkbook.Sheets("sheet1").Cells(y, 5) = ws.Cells(x, 5) 'col 5
                ThisWorkbook.Sheets("sheet1").Cells(y, 6) = ws.Cells(x, 6) 'col 6
                y = y + 1
              Next x


          Next ws

          'Vai fechar a pasta aberta temporariamente
          wb.Close
        End If

    Next wbFile

#### End Sub
