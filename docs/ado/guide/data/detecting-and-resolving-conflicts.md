---
description: Detectando e solucionando conflitos
title: Detectando e resolvendo conflitos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- conflicts [ADO], detecting and resolving
- ADO, detecting and resolving conflicts
ms.assetid: b28fdd26-c1a4-40ce-a700-2b0c9d201514
author: rothja
ms.author: jroth
ms.openlocfilehash: c9ab7dd72816d47b4f8a1c7aa55ba8751399e41a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453508"
---
# <a name="detecting-and-resolving-conflicts"></a>Detectando e solucionando conflitos
Se você estiver lidando com o conjunto de registros no modo imediato, haverá muito menos chances de ocorrer problemas de simultaneidade. Por outro lado, se seu aplicativo usar a atualização do modo de lote, poderá haver uma boa chance de que um usuário altere um registro antes que as alterações feitas por outro usuário editando o mesmo registro sejam salvas. Nesse caso, você desejará que seu aplicativo manipule normalmente o conflito. Pode ser que você queira que a última pessoa envie uma atualização para o servidor "WINS". Ou talvez você queira permitir que o usuário mais recente decida qual atualização deve ter precedência fornecendo-lhe uma opção entre os dois valores conflitantes.  
  
 Seja qual for o caso, o ADO fornecerá as propriedades subdependent e OriginalValue do objeto Field para lidar com esses tipos de conflitos. Use essas propriedades em combinação com o método de ressincronização e a propriedade Filter do conjunto de registros.  
  
## <a name="remarks"></a>Comentários  
 Quando o ADO encontra um conflito durante uma atualização do lote, um aviso será adicionado à coleção de erros. Portanto, você sempre deve verificar se há erros imediatamente depois de chamar BatchUpdate e, se encontrá-los, começar a testar a suposição de que você encontrou um conflito. A primeira etapa é definir a propriedade Filter no conjunto de registros igual a adFilterConflictingRecords. Isso limita a exibição no conjunto de registros somente aos registros que estão em conflito. Se a propriedade RecordCount for igual a zero após essa etapa, você saberá que o erro foi gerado por algo diferente de um conflito.  
  
 Quando você chama BatchUpdate, o ADO e o provedor estão gerando instruções SQL para executar atualizações na fonte de dados. Lembre-se de que determinadas fontes de dados têm limitações sobre quais tipos de colunas podem ser usados em uma cláusula WHERE.  
  
 Em seguida, chame o método Ressync no conjunto de registros com o argumento AffectRecords definido igual a adAffectGroup e o argumento ResyncValues definido igual a adResyncUnderlyingValues. O método Ressync atualiza os dados no objeto Recordset atual do banco de dados subjacente. Usando o adAffectGroup, você está garantindo que apenas os registros visíveis com a configuração de filtro atual, ou seja, apenas os registros conflitantes, sejam ressincronizados com o banco de dados. Isso pode fazer uma diferença significativa no desempenho se você estiver lidando com um grande conjunto de registros. Ao definir o argumento ResyncValues como adResyncUnderlyingValues ao chamar a ressincronização, você garante que a propriedade subdependent conterá o valor (conflitante) do banco de dados, que a propriedade Value manterá o valor inserido pelo usuário e que a propriedade OriginalValue manterá o valor original do campo (o valor que ele tinha antes da última chamada UpdateBatch bem-sucedida foi feita). Você pode usar esses valores para resolver o conflito programaticamente ou exigir que o usuário selecione o valor que será usado.  
  
 Essa técnica é mostrada no exemplo de código a seguir. O exemplo cria artificialmente um conflito usando um conjunto de registros separado para alterar um valor na tabela subjacente antes que UpdateBatch seja chamado.  
  
```  
'BeginConflicts  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT * FROM Shippers WHERE ShipperID = 2"  
  
    'Open Rs and change a value  
    Set objRs1 = New ADODB.Recordset  
    Set objRs2 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Introduce a conflict at the db...  
    objRs2.Open strSQL, strConn, adOpenKeyset, adLockOptimistic, adCmdText  
    objRs2("Phone") = "(999) 555-9999"  
    objRs2.Update  
    objRs2.Close  
    Set objRs2 = Nothing  
  
    On Error Resume Next  
    objRs1.UpdateBatch  
  
    If objRs1.ActiveConnection.Errors.Count <> 0 Then  
        Dim intConflicts As Integer  
  
        intConflicts = 0  
  
        objRs1.Filter = adFilterConflictingRecords  
  
        intConflicts = objRs1.RecordCount  
  
        'Resync so we can see the UnderlyingValue and offer user a choice.  
        'This sample only displays all three values and resets to original.  
        objRs1.Resync adAffectGroup, adResyncUnderlyingValues  
  
        If intConflicts > 0 Then  
            strMsg = "A conflict occurred with updates for " & intConflicts & _  
                     " record(s)." & vbCrLf & "The values will be restored" & _  
                     " to their original values." & vbCrLf & vbCrLf  
  
            objRs1.MoveFirst  
            While Not objRs1.EOF  
              strMsg = strMsg & "SHIPPER = " & objRs1("CompanyName") & vbCrLf  
              strMsg = strMsg & "Value = " & objRs1("Phone").Value & vbCrLf  
              strMsg = strMsg & "UnderlyingValue = " & _  
                                 objRs1("Phone").UnderlyingValue & vbCrLf  
              strMsg = strMsg & "OriginalValue = " & _  
                                 objRs1("Phone").OriginalValue & vbCrLf  
              strMsg = strMsg & vbCrLf & "Original value has been restored."  
  
              MsgBox strMsg, vbOKOnly, _  
                    "Conflict " & objRs1.AbsolutePosition & _  
                    " of " & intConflicts  
  
              objRs1("Phone").Value = objRs1("Phone").OriginalValue  
              objRs1.MoveNext  
            Wend  
  
            objRs1.UpdateBatch adAffectGroup  
        Else  
            'Other error occurred. Minimal handling in this example.  
             strMsg = "Errors occurred during the update. " & _  
                        objRs1.ActiveConnection.Errors(0).Number & " " & _  
                        objRs1.ActiveConnection.Errors(0).Description  
        End If  
  
        On Error GoTo 0  
    End If  
  
    objRs1.MoveFirst  
    objRs1.Close  
    Set objRs1 = Nothing  
'EndConflicts  
```  
  
 Você pode usar a propriedade status do registro atual ou de um campo específico para determinar que tipo de conflito ocorreu.  
  
 Para obter informações detalhadas sobre o tratamento de erros, consulte [tratamento de erros](../../../ado/guide/data/error-handling.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Modo de lote](../../../ado/guide/data/batch-mode.md)
