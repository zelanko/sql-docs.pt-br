---
title: Erros do provedor | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors collection [ADO]
- provider errors [ADO]
- event-related errors [ADO]
- errors [ADO], provider
- Error object [ADO], provider errors
ms.assetid: cc7d6ff9-2034-45c6-9d61-90b177010054
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 56fff67f882eceec3c07553e5c465da65a69ce65
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718683"
---
# <a name="provider-errors"></a>Erros do provedor
Quando ocorre um erro do provedor, um erro de tempo de execução de -2147467259 é retornado. Quando você recebe esse erro, verifique as **erros** coleção de ativo **Conexão** objeto, que irá conter um ou mais erros que descreve o que ocorreu.  
  
## <a name="the-ado-errors-collection"></a>A coleção de erros ADO  
 Porque uma determinada operação ADO pode produzir vários erros de provedor, o ADO expõe uma coleção de objetos de erro por meio de **Conexão** objeto. Esta coleção não contém objetos se uma operação é concluído com êxito e contém um ou mais **erro** objetos se algo deu errado e o provedor gerado de um ou mais erros. Examine cada objeto de erro para determinar a causa exata do erro.  
  
 Assim que terminar de tratamento de erros que ocorreram, você pode limpar a coleção, chamando o **limpar** método. É especialmente importante limpar explicitamente o **erros** coleção antes de chamar o **ressincronizar**, **UpdateBatch**, ou **CancelBatch**método em uma **conjunto de registros** objeto, o **abrir** método em um **Conexão** de objeto, ou definir o **filtro** propriedade em um **Recordset** objeto. Limpando explicitamente a coleção, você pode ter certeza de que qualquer **erro** objetos na coleção não provêm de uma operação anterior.  
  
 Algumas operações podem gerar avisos além dos erros. Avisos também são representados por **erro** objetos na **erros** coleção. Quando um provedor adiciona um aviso na coleção, ele não gera um erro de tempo de execução. Verifique as **contagem** propriedade do **erros** coleção para determinar se um aviso foi produzido por uma operação específica. Se a contagem é um ou mais, uma **erro** objeto foi adicionado à coleção. Assim que você determinou que o **erros** coleção contém erros ou avisos, você pode iterar pela coleção e recuperar informações sobre cada **erro** objeto que ele contém. Pequeno exemplo de Visual Basic a seguir demonstra isso:  
  
```  
' BeginErrorHandlingVB02  
Private Function DeleteCustomer(ByVal CompanyName As String) As Long  
    On Error GoTo DeleteCustomerError  
  
    rst.Find "CompanyName='" & CompanyName & "'"  
DeleteCustomerError:  
Dim objError As ADODB.Error  
Dim strError As String  
  
    If cnn.Errors.Count > 0 Then  
        For Each objError In cnn.Errors  
            strError = strError & "Error #" & objError.Number & _  
                " " & objError.Description & vbCrLf & _  
                "NativeError: " & objError.NativeError & vbCrLf & _  
                "SQLState: " & objError.SQLState & vbCrLf & _  
                "Reported by: " & objError.Source & vbCrLf & _  
                "Help file: " & objError.HelpFile & vbCrLf & _  
                "Help Context ID: " & objError.HelpContext  
        Next  
        MsgBox strError  
    End If  
End Function  
' EndErrorHandlingVB02  
```  
  
 A rotina de tratamento de erro inclui um **para cada** loop que examina cada objeto na **erros** coleção. Neste exemplo, ele acumula uma mensagem para exibição. Em um programa de trabalho, você deve escrever código para executar uma tarefa apropriada para cada erro, como fechar todos os arquivos abertos e desligar o programa de forma ordenada.  
  
## <a name="the-error-object"></a>O objeto de erro  
 Examinando uma **erro** objeto você pode determinar o erro e mais importante, o aplicativo ou o objeto causou o erro. O **erro** objeto tem as seguintes propriedades:  
  
|Nome da propriedade|Descrição|  
|-------------------|-----------------|  
|**Descrição**|Uma descrição de texto do erro que ocorreu.|  
|**HelpContext, HelpFile**|Refere-se para o arquivo de Ajuda e o tópico da Ajuda que contém uma descrição do erro que ocorreu.|  
|**NativeError**|O número de erro específico do provedor.|  
|**número**|Um inteiro longo que representa o número (listados na **ErrorValueEnum**) do erro que ocorreu.|  
|**Origem**|Indica o nome do objeto ou aplicativo que gerou um erro.|  
|**SQLState**|Um código de erro de cinco caracteres que o provedor retorna durante o processo de uma instrução SQL.|  
  
 O ADO **erro** objeto é muito semelhante ao padrão Visual Basic **Err** objeto. Suas propriedades descrevem o erro que ocorreu. Além do número do erro, você também receberá dois conjuntos relacionados de informações. O **NativeError** propriedade contém um número de erro específica do provedor que você está usando. No exemplo anterior, o provedor é o Microsoft OLE DB Provider para SQL Server, portanto **NativeError** conterá os erros específicos ao SQL Server. O **SQLState** propriedade tem um código de cinco letras que descreve um erro em uma instrução SQL.  
  
## <a name="event-related-errors"></a>Erros relacionados a eventos  
 O **erro** objeto também é usado quando ocorrem erros relacionados a eventos. Você pode determinar se ocorreu um erro no processo que disparou um evento de ADO, verificando o **erro** objeto passado como um parâmetro de evento.  
  
 Se a operação que faz com que um evento seja concluída com êxito, o *adStatus* parâmetro do manipulador de eventos será definido como *adStatusOK*. Por outro lado, se a operação que gerou o evento foi bem-sucedida, o *adStatus* parâmetro for definido como *adStatusErrorsOccurred*. Nesse caso, o *pError* parâmetro conterá um **erro** objeto que descreve o erro.
