'Criando função!

Converter Libra -> Quilograma

    1 lbs = 0,45359

'Escrever diretamente na planilha
 
    Range("A1") = 0,4539 'fator conversão Kg

'VBA

    Funcion KGrams(lbs)

    KGrams = lbs * Range("A1").Value
    
    End Function

OU

    Funcion KGrams(lbs)
    
    KGrams = lbs * 0,4539

    End Function
