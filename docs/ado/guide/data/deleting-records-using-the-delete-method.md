---
title: Excluindo registros usando o método Delete | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, deleting records
- deleting records [ADO]
- editing data [ADO], Delete method
- Delete method [ADO]
ms.assetid: bfed5cfa-7f57-463b-9da2-0c612a079d30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a099b033422e7c10214371772edd090f0cc15fd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718164"
---
# <a name="deleting-records-using-the-delete-method"></a>Excluir registros usando o método Delete
Usando o **exclua** método marca o registro atual ou um grupo de registros em uma **Recordset** objeto para exclusão. Se o **Recordset** objeto não permite exclusão de registros, ocorrerá um erro. Se você estiver no modo de atualização imediata, exclusões ocorrem no banco de dados imediatamente. Se um registro não pode ser excluído com êxito (devido a violações de integridade de banco de dados, por exemplo), o registro permanecerá no modo de edição após a chamada para **atualização.** Isso significa que você deve cancelar a atualização usando [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) antes de passar fora do registro atual (por exemplo, usando [Close](../../../ado/reference/ado-api/close-method-ado.md), [mover](../../../ado/reference/ado-api/move-method-ado.md), ou [ NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 Se você estiver no modo de atualização em lotes, os registros marcados para exclusão do cache e a exclusão real acontece quando você chama o **UpdateBatch** método. (Para exibir os registros excluídos, defina a **filtro** propriedade **adFilterAffectedRecords** após **excluir** é chamado.)  
  
 A tentativa de recuperar valores de campo do registro excluído gera um erro. Depois de excluir o registro atual, o registro excluído permanece atual até que você mova para um registro diferente. Quando você se afasta o registro excluído, ele não está mais acessível.  
  
 Caso você aninhe exclusões em uma transação, você pode recuperar registros excluídos usando o **RollbackTrans** método. Se você estiver no modo de atualização em lotes, você pode cancelar uma exclusão pendente ou o grupo de pendentes exclusões usando o **CancelBatch** método.  
  
 Se a tentativa de excluir registros falhar devido a um conflito com os dados subjacentes (por exemplo, um registro já foi excluído por outro usuário), o provedor retornará avisos para o **erros** coleção, mas não interromper o programa execução. Um erro de tempo de execução ocorre somente se houver conflitos em todos os registros solicitados.  
  
 Se o **tabela exclusiva** dinâmico estiver definida e o **conjunto de registros** é o resultado da execução de uma operação de junção em várias tabelas, o **excluir** método excluirá linhas somente da tabela nomeada na **tabela exclusiva** propriedade.  
  
 O **exclua** método usa um argumento opcional que permite que você especifique quais registros são afetados pela **excluir** operação. Os únicos valores válidos para esse argumento são qualquer uma das seguinte ADO **AffectEnum** constantes enumeradas:  
  
-   **adAffectCurrent** afeta somente o registro atual.  
  
-   **adAffectGroup** afeta somente os registros que atendem a atual **filtro** configuração da propriedade. O **filtro** propriedade deve ser definida como um **FilterGroupEnum** valor ou uma matriz de **indicadores** para usar essa opção.  
  
 O código a seguir mostra um exemplo da especificação **adAffectGroup** ao chamar o **excluir** método. Este exemplo adiciona alguns registros para a amostra **Recordset** e atualiza o banco de dados. Em seguida, ele filtra o **conjunto de registros** usando o **adFilterAffectedRecords** constante enumerada filtro, que deixa apenas os registros adicionados recentemente visível no **conjunto de registros.** Por fim, ele chama o **exclua** método e especifica que todos os registros que satisfazem atual **filtro** (os novos registros) de configuração de propriedade deve ser excluída.  
  
```  
'BeginDeleteGroup  
    'add some bogus records  
    With objRs  
        For i = 0 To 8  
            .AddNew  
            .Fields("CompanyName") = "Shipper Number " & i + 1  
            .Fields("Phone") = "(425) 555-000" & (i + 1)  
            .Update  
        Next i  
  
        ' update  
        .UpdateBatch  
  
        'filter on newly added records  
        .Filter = adFilterAffectedRecords  
        Debug.Print "Deleting the " & .RecordCount & _  
                    " records you just added."  
  
        'delete the newly added bogus records  
        .Delete adAffectGroup  
        .Filter = adFilterNone  
        Debug.Print .RecordCount & " records remain."  
    End With  
'EndDeleteGroup  
```
