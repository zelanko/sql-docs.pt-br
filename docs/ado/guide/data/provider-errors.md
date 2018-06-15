---
title: Erros do provedor | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- errors collection [ADO]
- provider errors [ADO]
- event-related errors [ADO]
- errors [ADO], provider
- Error object [ADO], provider errors
ms.assetid: cc7d6ff9-2034-45c6-9d61-90b177010054
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a4f551876f97f04f99bd8f2e722cd9e8a89f264
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272335"
---
# <a name="provider-errors"></a>Erros do provedor
Quando ocorre um erro de provedor, um erro de tempo de execução de -2147467259 é retornado. Quando você receber esse erro, verifique o **erros** coleção de ativo **Conexão** objeto, que contém um ou mais erros que descreve o que ocorreu.  
  
## <a name="the-ado-errors-collection"></a>A coleção de erros de ADO  
 Como uma determinada operação ADO pode gerar vários erros de provedor, o ADO expõe uma coleção de objetos de erro por meio de **Conexão** objeto. Esta coleção não contém objetos se uma operação é concluída com êxito e contém um ou mais **erro** objetos se algo deu errado e o provedor gerado um ou mais erros. Examine cada objeto de erro para determinar a causa exata do erro.  
  
 Assim que terminar de tratamento de erros que ocorreram, você pode limpar a coleção, chamando o **limpar** método. É especialmente importante limpar explicitamente o **erros** coleção antes de chamar o **Resync**, **UpdateBatch**, ou **CancelBatch**método em um **Recordset** objeto, o **abrir** método em um **Conexão** de objeto, ou definir o **filtro** propriedade em um **Registros** objeto. Limpando explicitamente a coleção, você pode ter certeza de que qualquer **erro** objetos na coleção não provêm de uma operação anterior.  
  
 Algumas operações podem gerar avisos além de erros. Avisos também são representados por **erro** objetos no **erros** coleção. Quando um provedor adiciona um aviso para a coleção, ele não gera um erro de tempo de execução. Verifique o **contagem** propriedade o **erros** coleção para determinar se um aviso foi gerado por uma determinada operação. Se a contagem é um ou mais recente, uma **erro** objeto foi adicionado à coleção. Assim que você determinou que o **erros** coleção contém erros ou avisos, você pode iterar pela coleção e recuperar informações sobre cada **erro** objeto que ele contém. O seguinte exemplo do Visual Basic curto demonstra isso:  
  
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
  
 A rotina de tratamento de erro inclui um **para cada** loop que examina cada objeto o **erros** coleção. Neste exemplo, são acumulados uma mensagem para exibição. Em um programa, você escreve código para executar uma tarefa apropriada para cada erro, como fechar todos os arquivos abertos e desligar o programa de forma ordenada.  
  
## <a name="the-error-object"></a>O objeto de erro  
 Examinando um **erro** objeto, você pode determinar o erro e o mais importante, o aplicativo ou o objeto causou o erro. O **erro** objeto tem as seguintes propriedades:  
  
|Nome da propriedade|Description|  
|-------------------|-----------------|  
|**Descrição**|Uma descrição de texto do erro que ocorreu.|  
|**HelpContext, HelpFile**|Refere-se para o arquivo de Ajuda e o tópico da Ajuda que contém uma descrição do erro que ocorreu.|  
|**NativeError**|O número do erro específico do provedor.|  
|**Número**|Um inteiro longo que representa o número (listados no **ErrorValueEnum**) do erro que ocorreu.|  
|**Origem**|Indica o nome do objeto ou aplicativo que gerou um erro.|  
|**SQLState**|Um código de erro de cinco caracteres que o provedor retorna durante o processo de uma instrução SQL.|  
  
 O ADO **erro** objeto é muito semelhante do Visual Basic padrão **Err** objeto. As propriedades descrevem o erro que ocorreu. Além do número do erro, você também receberá dois tipos relacionados de informações. O **NativeError** propriedade contém um número de erro específica do provedor que você está usando. No exemplo anterior, o provedor é o Microsoft OLE DB Provider para SQL Server, portanto **NativeError** conterá erros específicos do SQL Server. O **SQLState** propriedade tem um código de cinco letras que descreve um erro em uma instrução SQL.  
  
## <a name="event-related-errors"></a>Erros relacionados a eventos  
 O **erro** objeto também é usado quando ocorrem erros relacionados a eventos. Você pode determinar se ocorreu um erro no processo que disparou um evento de ADO, verificando o **erro** objeto passado como um parâmetro de evento.  
  
 Se a operação que faz com que um evento seja concluída com êxito, o *adStatus* parâmetro do manipulador de eventos será definido como *adStatusOK*. Por outro lado, se a operação que gerou o evento foi bem-sucedida, o *adStatus* parâmetro está definido como *adStatusErrorsOccurred*. Nesse caso, o *pError* parâmetro conterá um **erro** objeto que descreve o erro.
