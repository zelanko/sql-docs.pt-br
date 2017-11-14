---
title: Detectando e resolvendo conflitos | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conflicts [ADO], detecting and resolving
- ADO, detecting and resolving conflicts
ms.assetid: b28fdd26-c1a4-40ce-a700-2b0c9d201514
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 00a768c70b1945bc573aaca6c48841e665780081
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="detecting-and-resolving-conflicts"></a>Detectando e solucionando conflitos
Se você estiver lidando com o conjunto de registros no modo imediato, há muito menos chance de problemas de simultaneidade ocorra. Por outro lado, se seu aplicativo usa a atualização do modo de lote, pode haver uma boa chance de que um usuário será alterado um registro antes de salvar as alterações feitas por outro usuário editando o mesmo registro. Nesse caso, você desejará seu aplicativo para lidar com o conflito. Pode ser seu desejo que a última pessoa a enviar uma atualização para o servidor "vence". Ou talvez você queira permitir que o usuário mais recente para decidir qual atualização deve ter precedência, fornecendo-lhe uma opção entre os dois valores conflitantes.  
  
 Seja qual for o caso, o ADO fornece as propriedades UnderlyingValue e OriginalValue do objeto Field para lidar com esses tipos de conflitos. Use essas propriedades em combinação com o método de ressincronização e a propriedade de filtro do conjunto de registros.  
  
## <a name="remarks"></a>Comentários  
 Quando o ADO encontra um conflito durante uma atualização em lotes, um aviso será adicionado à coleção de erros. Portanto, você deve sempre verificar erros imediatamente após chamar BatchUpdate e se você encontrá-los, começar a testar a suposição de que você encontrou um conflito. A primeira etapa é definir a propriedade de filtro em adFilterConflictingRecords de igualdade conjunto de registros. Isso limita a exibição em seu conjunto de registros somente os registros que estão em conflito. Se a propriedade RecordCount for igual a zero após essa etapa, você saberá que o erro foi gerado por algo diferente de um conflito.  
  
 Quando você chama BatchUpdate, ADO e o provedor estão gerando instruções SQL para realizar atualizações na fonte de dados. Lembre-se de que certas fontes de dados têm limitações em que os tipos de colunas podem ser usados em uma cláusula WHERE.  
  
 Em seguida, chame o método de ressincronização no conjunto de registros com o argumento AffectRecords definido como adAffectGroup e o argumento ResyncValues definido como adResyncUnderlyingValues. O método de ressincronização atualiza os dados no objeto de conjunto de registros atual do banco de dados subjacente. Usando adAffectGroup, você garante que somente os registros visíveis com o filtro atual de configuração, ou seja, somente os registros conflitantes, são sincronizados novamente com o banco de dados. Se você estiver lidando com um grande conjunto de registros, isso pode tornar uma diferença de desempenho significativa. Configurar o argumento ResyncValues adResyncUnderlyingValues quando chamar ressincronização, você garante que a propriedade UnderlyingValue conterá o valor (conflitante) do banco de dados, que a propriedade de valor manterá o valor inserido pelo usuário, e Se a propriedade OriginalValue irá conter o valor original para o campo (o valor que tinha antes da última chamada UpdateBatch bem-sucedida foi feita). Você pode usar esses valores para resolver o conflito de forma programática ou exigir que o usuário selecionar o valor que será usado.  
  
 Essa técnica é mostrada no exemplo de código a seguir. O exemplo cria artificialmente um conflito com um conjunto de registros separado para alterar um valor na tabela subjacente antes UpdateBatch é chamado.  
  
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
  
 Você pode usar a propriedade de Status do registro atual ou de um campo específico para determinar que tipo de um conflito ocorreu.  
  
 Para obter informações detalhadas sobre o tratamento de erros, consulte [tratamento de erros](../../../ado/guide/data/error-handling.md).  
  
## <a name="see-also"></a>Consulte também  
 [Modo de lote](../../../ado/guide/data/batch-mode.md)

