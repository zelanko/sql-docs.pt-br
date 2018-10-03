---
title: Detectar e resolver conflitos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a27a8ff70a995ab24dcf762d0ada731e0de6fa92
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47625276"
---
# <a name="detecting-and-resolving-conflicts"></a>Detectando e solucionando conflitos
Se você estiver lidando com seu conjunto de registros no modo imediato, há muito menos chance de problemas de simultaneidade ocorram. Por outro lado, se seu aplicativo usa a atualização do modo em lote, pode haver uma boa chance de que um usuário será alterado de um registro antes de salvar alterações que foram feitas por outro usuário editar o mesmo registro. Nesse caso, você desejará que seu aplicativo para tratar normalmente o conflito. Pode ser seu desejo que a última pessoa a enviar uma atualização para o servidor "vence". Ou talvez você queira permitir que o usuário mais recente para decidir qual atualização deve ter precedência, fornecendo-lhe uma opção entre os dois valores conflitantes.  
  
 Seja qual for o caso, o ADO fornece as propriedades UnderlyingValue e OriginalValue do objeto de campo para lidar com esses tipos de conflitos. Use essas propriedades em combinação com o método de ressincronização e a propriedade de filtro do conjunto de registros.  
  
## <a name="remarks"></a>Comentários  
 Quando o ADO encontra um conflito durante uma atualização em lotes, um aviso será adicionado à coleção de erros. Portanto, você sempre deve verificar erros imediatamente após chamar BatchUpdate e se você encontrá-los, começar a testar a suposição de que você encontrou um conflito. A primeira etapa é definir a propriedade de filtro em igual o conjunto de registros para adFilterConflictingRecords. Isso limita a exibição em seu conjunto de registros a apenas os registros que estão em conflito. Se a propriedade RecordCount for igual a zero após essa etapa, você sabe que o erro foi gerado por algo diferente de um conflito.  
  
 Quando você chama BatchUpdate, ADO e o provedor estiver gerando instruções SQL para realizar atualizações na fonte de dados. Lembre-se de que determinadas fontes de dados tem limitações na qual os tipos de colunas podem ser usados em uma cláusula WHERE.  
  
 Em seguida, chame o método de ressincronização no conjunto de registros com o argumento de AffectRecords definido igual a adAffectGroup e o argumento de ResyncValues definido igual ao adResyncUnderlyingValues. O método de ressincronização atualiza os dados no objeto de conjunto de registros atual do banco de dados subjacente. Ao usar adAffectGroup, você garante que somente os registros visíveis com a configuração, ou seja, somente os registros conflitantes, de filtro atual são sincronizados novamente com o banco de dados. Se você estiver lidando com um grande conjunto de registros, isso pode tornar uma diferença significativa de desempenho. Definindo o argumento ResyncValues como adResyncUnderlyingValues ao chamar a ressincronização, você certifique-se de que a propriedade UnderlyingValue conterá o valor (conflitante) do banco de dados, que a propriedade Value manterá o valor inserido pelo usuário, e Se a propriedade OriginalValue conterá o valor original para o campo (o valor que tinha antes da última chamada bem-sucedida de UpdateBatch foi feita). Em seguida, você pode usar esses valores para resolver o conflito de forma programática ou exigir que o usuário selecionar o valor que será usado.  
  
 Essa técnica é mostrada no exemplo de código a seguir. O exemplo cria artificialmente um conflito usando um conjunto de registros separado para alterar um valor na tabela subjacente antes de UpdateBatch é chamado.  
  
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
  
 Para obter informações detalhadas sobre o tratamento de erro, consulte [tratamento de erro](../../../ado/guide/data/error-handling.md).  
  
## <a name="see-also"></a>Consulte também  
 [Modo de lote](../../../ado/guide/data/batch-mode.md)
