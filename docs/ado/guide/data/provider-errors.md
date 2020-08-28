---
description: Erros do provedor
title: Erros do provedor | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b31f530bafd69d59c98893cc2ead29039372dea9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979977"
---
# <a name="provider-errors"></a>Erros do provedor
Quando ocorre um erro de provedor, um erro de tempo de execução de-2147467259 é retornado. Ao receber esse erro, verifique a coleção de **erros** do objeto de **conexão** ativa, que conterá um ou mais erros que descrevem o que ocorreu.  
  
## <a name="the-ado-errors-collection"></a>A coleção de erros do ADO  
 Como uma operação ADO específica pode produzir vários erros de provedor, o ADO expõe uma coleção de objetos de erro por meio do objeto de **conexão** . Essa coleção não contém objetos se uma operação for concluída com êxito e contiver um ou mais objetos de **erro** se algo tiver ficado errado e o provedor tiver gerado um ou mais erros. Examine cada objeto de erro para determinar a causa exata do erro.  
  
 Assim que terminar de lidar com quaisquer erros ocorridos, você poderá limpar a coleção chamando o método **Clear** . É especialmente importante limpar explicitamente a coleção de **erros** antes de chamar o método **Ressync**, **UpdateBatch**ou **CancelBatch** em um objeto **Recordset** , o método **Open** em um objeto **Connection** ou definir a propriedade **Filter** em um objeto **Recordset** . Limpando a coleção explicitamente, você pode ter certeza de que qualquer objeto de **erro** na coleção não será deixado de uma operação anterior.  
  
 Algumas operações podem gerar avisos além de erros. Os avisos também são representados por objetos de **erro** na coleção de **erros** . Quando um provedor adiciona um aviso à coleção, ele não gera um erro em tempo de execução. Verifique a propriedade **Count** da coleção de **erros** para determinar se um aviso foi produzido por uma determinada operação. Se a contagem for um ou maior, um objeto de **erro** será adicionado à coleção. Assim que você determinar que a coleção de **erros** contém erros ou avisos, você pode iterar pela coleção e recuperar informações sobre cada objeto de **erro** que ele contém. O exemplo de breve Visual Basic a seguir demonstra isso:  
  
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
  
 A rotina de tratamento de erros inclui um loop **for each** que examina cada objeto na coleção de **erros** . Neste exemplo, ele acumula uma mensagem para exibição. Em um programa funcional, você escreveria código para executar uma tarefa apropriada para cada erro, como fechar todos os arquivos abertos e desligar o programa de maneira ordenada.  
  
## <a name="the-error-object"></a>O objeto de erro  
 Ao examinar um objeto de **erro** , você pode determinar qual erro ocorreu e, mais importante, qual aplicativo ou qual objeto causou o erro. O objeto de **erro** tem as seguintes propriedades:  
  
|Nome da propriedade|Descrição|  
|-------------------|-----------------|  
|**Descrição**|Uma descrição de texto do erro que ocorreu.|  
|**HelpContext, HelpFile**|Refere-se ao tópico da ajuda e ao arquivo de ajuda que contém uma descrição do erro que ocorreu.|  
|**NativeError**|O número do erro específico do provedor.|  
|**Número**|Um inteiro longo que representa o número (listado no **ErrorValueEnum**) do erro que ocorreu.|  
|**Origem**|Indica o nome do objeto ou aplicativo que gerou um erro.|  
|**SQLState**|Um código de erro de cinco caracteres que o provedor retorna durante o processo de uma instrução SQL.|  
  
 O objeto de **erro** ADO é muito semelhante ao objeto padrão Visual Basic **Err** . Suas propriedades descrevem o erro que ocorreu. Além do número do erro, você também recebe duas partes de informação relacionadas. A propriedade **NativeError** contém um número de erro específico para o provedor que você está usando. No exemplo anterior, o provedor é o provedor de OLE DB da Microsoft para SQL Server, portanto **NativeError** conterá erros específicos para SQL Server. A propriedade **SQLSTATE** tem um código de cinco letras que descreve um erro em uma instrução SQL.  
  
## <a name="event-related-errors"></a>Erros relacionados a eventos  
 O objeto de **erro** também é usado quando ocorrem erros relacionados a eventos. Você pode determinar se ocorreu um erro no processo que gerou um evento ADO verificando o objeto de **erro** passado como um parâmetro de evento.  
  
 Se a operação que causa um evento for concluída com êxito, o parâmetro *adStatus* do manipulador de eventos será definido como *adStatusOK*. Por outro lado, se a operação que gerou o evento não tiver sido bem-sucedida, o parâmetro *adStatus* será definido como *adStatusErrorsOccurred*. Nesse caso, o parâmetro *perror* conterá um objeto de **erro** que descreve o erro.
