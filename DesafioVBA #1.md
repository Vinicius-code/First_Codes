
Sumário:

# BaseAlunos

## 1. Inserir dados com Useform
## 2. Exportar dados para outra tabela

# Notas Turmas

## 3. Enumerar linhas
## 4. Inserir notas de acordo com matrícula
## 5. Calcular situação

.
.
.
.
.
.

### 1. Inserir dados com _Useform_

Private Sub ToggleButton1_Click()

**'Primeiramente foi criado um UseForm nomeado de Cadastro**

**'Após a criação, ao clicar no commandbutton foi aberto essa Sub para iniciar a Macro.**

**'O evento selecionado foi o Click, ou seja, acontecerá tudo aqui após o click.**

**'Foi definido qual será a última linha a ser preenchida**

	linha = Range("A1").End(xlDown).Row + 1

**'Essa condição impede que seja colocado na matrícula um valor de texto**

		If Not IsNumeric(matricula_aluno) Then
			MsgBox ("Número de Matrícula inválido")
			Exit Sub
		Else
	End If

**'Definição das células e colunas. O objeto atribuído veio do UseForm**

	Cells(linha, 1) = nome_aluno.Value
	Cells(linha, 2) = matricula_aluno.Value
	Cells(linha, 3) = turma_aluno.Value

**'Após a seleção na última linha, foi gravado uma macro para ordenar a tabela em ordem alfabética**

    With ActiveWorkbook.Worksheets("BaseAlunos").Sort
        .SetRange Range("A2:A" & linha)
        .Apply
    End With
                        
**'Mensagem final**

	MsgBox ("Alunx cadastrado com sucesso")

**'Caso seja necessário outro input**

	resposta = MsgBox("Deseja inserir outro alunx?", vbYesNo, "Inserir")

**'Essa condição recarrega o formulário.**

**'Basicamente, caso seja necessário inserir outro cadastro, o VBA vai fechar o Useforms e abri-lo novamente.**

	If resposta = vbYes Then
    Unload Cadastro
    Cadastro.Show
	Else
    	Unload Cadastro

	End If

	End Sub


### 2. Exportar dados para outra tabela


Sub Macro4()
    
_'Lógica do algoritmo: Filtrar a tabela base de alunos de acordo com uma condição._

_'Copiar a tabela toda e colar na nova pasta de trabalho.  

	Range("A1").Select
    	Selection.AutoFilter
    	ActiveSheet.Range("$A$1:$C$50000").AutoFilter Field:=3, Criteria1:="EQ101" 'O critério é a turma

**'Seleciona um Range grande pois o filtro não muda as linhas**

    Range(Cells(1, 1).Offset(1, 0), Cells(100000, 2).End(xlUp)).Copy

**'Abre a nova pasta de trabalho e cola.**

    Workbooks.Open("C:\Users\Vinicius Machado\Downloads\MM projeto\Turmas.xlsx").Activate
    Worksheets("EQ101").Activate
    Range("B2").PasteSpecial
    Range("B2").Select
 
**'Retorna a pasta de trabalho Base Alunos.**

    Workbooks("BaseAlunos.xlsm").Activate
    Worksheets("BaseAlunos").Activate

**'Repete o processo para a outra turma.**

	Range("A1").Select
	    Selection.AutoFilter
	    ActiveSheet.Range("$A$1:$C$50000").AutoFilter Field:=3, Criteria1:="EQ201"
	    Range(Cells(1, 1).Offset(1, 0), Cells(100000, 2).End(xlUp)).Copy
	    Workbooks.Open("C:\Users\Vinicius Machado\Downloads\MM projeto\Turmas.xlsx").Activate
	    Worksheets("EQ201").Activate
	    Range("B2").PasteSpecial
	    Range("B2").Select

**'Após concluir, o novo arquivo é salvo e encerrado.**

	ActiveWorkbook.Save
	ActiveWorkbook.Close

**'Retorna-se a Base de Alunos e retira o filtro**

    Workbooks("BaseAlunos.xlsm").Activate
    Worksheets("BaseAlunos").Activate
    Range("A1").Select
    Selection.AutoFilter
  
	End Sub

### 3. Enumerar linhas

   **'Este procedimento atribui automaticamente um número de chamada para cada aluno cadastrado na primeira _
    célula de cada linha**
    
    Dim contador As Integer
    
   **'Para automatizar o contador: (lembrete: ".Row" retorna o número da linha de uma célula)**
        **'Inicialmente seleciona-sa a primeira célula com cadastro de nome de alunos (B2)**
        **'Em seguida, utilizou-se o artifício Ctrl+shift+seta(para baixo), **
				**'com isso, o contador estará _relacionado ao numero de alunos cadastrados**
        **'Por fim retorna-se na coluna "A" o número da chamada dos alunos cadastrados**
        **'Foi necessário adicionar um "If" para evitar um erro caso não tenha sido feito cadastro de alunos**
        
    Range("B2").Select
    If Selection = "" Then
        Exit Sub
    Else
        For contador = 2 To Selection.End(xlDown).Row
            Cells(contador, 1).Value = Cells(contador, 1).Row - 1
        Next
    End If
    
    
   **'Esta parte do código será responsável por classificar em ordem alfabética**
       
    With ActiveWorkbook.Worksheets("EQ101").Sort
        .SetRange Range("B2:C" & contador)
        .Apply
    End With
    
	End Sub

### 4. Inserir notas de acordo com matrícula

	Private Sub BotãoOk_Click()
	    Dim turma As Range
	    Dim posicao As Integer
	    Dim msg As String
	    Dim ans As Integer
    
   **'Configura o tratamento de erros para matrículas não encontradas**
    
    On Error GoTo MatriculaErrada
    
   **'Determinando o Range de alunos cadastrado**
    
    Range("B2").Select
    Set turma = Range(Selection, Selection.End(xlDown))
    If Not IsNumeric(numMatrícula) Then
        ans = MsgBox("Insira um número de matrícula válido.", vbExclamation, "")
        Exit Sub
    End If
    
   **'Busca a matrícula digitada**
    
    posicao = turma.Find(numMatrícula).Row
    If Not IsNumeric(Nota) Then
        ans = MsgBox("Insira uma nota.", vbExclamation, "")
        Exit Sub
    End If
    
   **'Cadastra a Nota**
   
    If OpçãoProva1 Then Cells(posicao, 4) = Nota.Value
    If OpçãoProva2 Then Cells(posicao, 5) = Nota.Value
    If OpçãoPF Then Cells(posicao, 7) = Nota.Value
    If Not OpçãoProva1 And Not OpçãoProva2 And Not OpçãoPF Then
        ans = MsgBox("Selecione uma prova para cadastrar a nota.", vbExclamation, "")
    End If
    
   **'Limpa os controles para a próxima entrada**
   
    numMatrícula = ""
    Nota = ""
    numMatrícula.SetFocus
    Exit Sub
    
	MatriculaErrada:
	    msg = "Matrícula não encontrada, certifique-se de que o número digitado está correto."
	    ans = MsgBox(msg, vbExclamation, "")
	End Sub



### 5. Calcular situação

Sub Medias_Situacoes()

**'Realiza os calculos das médias e indica a situação dos alunos.**

    Dim contador As Integer
    Dim M1 As Double
    Dim Mf As Double
    
   **'Para realizar as funções para cada aluno de forma automática, utilizou-se um loop "for" _
    tendo como base um contador automático que engloba todos os alunos cadastrados na turma.**

	   Range("B2").Select
	    If Selection = "" Then
		Exit Sub
	    Else
		For contador = 2 To Selection.End(xlDown).Row
        
   **'Adicionou-se um "If" para realizar os calculos de M1 apenas se as notas da P1 e P2 estiverem cadastradas.**
        
            If Cells(contador, 4).Value <> "" And Cells(contador, 5).Value <> "" Then
                M1 = (Cells(contador, 4).Value + Cells(contador, 5).Value) / 2
                Cells(contador, 6).Value = M1
                
   **'Utilizou-se a estrutura "select case" para determinar as situações pós P1 e P2.**
                
		Select Case M1
                
   **'Falta acrescentar cores de fundo**
                    
		    Case Is < 3
                        Cells(contador, 8).Value = M1
                        Cells(contador, 9).Value = "RP"
                    Case Is < 7
                        Cells(contador, 9).Value = "PF"
                    Case Is >= 7
                        Cells(contador, 8).Value = M1
                        Cells(contador, 9).Value = "AP"
                End Select
                
   **'Adicionou-se um "IF" para realizar os calculos de MF apenas se a nota da PF estiver cadastrada.**
                
                If Cells(contador, 7) <> "" Then
                    Mf = (M1 + Cells(contador, 7).Value) / 2
                    Cells(contador, 8).Value = Mf
		    
   **'Utilizou-se a estrutura "Select case" para de terminar as situações pós PF.**
                    
		    Select Case Mf
                    
                        Case Is < 5
                        Cells(contador, 9).Value = "RP"
                    Case Is >= 5
                        Cells(contador, 9).Value = "AP"
                    End Select
                End If
            End If
        Next
    End If
End Sub









