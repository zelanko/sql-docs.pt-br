---
title: "Excluindo registros usando o método Delete | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, deleting records
- deleting records [ADO]
- editing data [ADO], Delete method
- Delete method [ADO]
ms.assetid: bfed5cfa-7f57-463b-9da2-0c612a079d30
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f681e4453751deb6c191ee5f4baa42b77471b34b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="deleting-records-using-the-delete-method"></a>Excluindo registros usando o método Delete
Usando o **excluir** método marca o registro atual ou um grupo de registros em um **registros** objeto para exclusão. Se o **registros** objeto não permite a exclusão do registro, ocorrerá um erro. Se você estiver no modo de atualização imediata, exclusões ocorrerem no banco de dados imediatamente. Se um registro não pode ser excluído com êxito (devido a violações de integridade de banco de dados, por exemplo), o registro permanecerá no modo de edição após a chamada a **atualização.** Isso significa que você deve cancelar a atualização usando [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) antes de mover fora do registro atual (por exemplo, usando [fechar](../../../ado/reference/ado-api/close-method-ado.md), [mover](../../../ado/reference/ado-api/move-method-ado.md), ou [ NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 Se você estiver no modo de atualização em lotes, os registros marcados para exclusão do cache e a exclusão real acontece quando você chamar o **UpdateBatch** método. (Para exibir os registros excluídos, defina o **filtro** propriedade **adFilterAffectedRecords** depois **excluir** é chamado.)  
  
 Tentativa de recuperar valores de campo do registro excluído gera um erro. Depois de excluir o registro atual, o registro excluído permanece atual até que você mova para um registro diferente. Uma vez sair de registro excluído, ele não é mais acessível.  
  
 Se você aninhar exclusões em uma transação, você pode recuperar os registros excluídos por meio de **RollbackTrans** método. Se você estiver no modo de atualização em lotes, você pode cancelar uma exclusão pendente ou grupo de pendente exclusões usando o **CancelBatch** método.  
  
 Se a tentativa de excluir registros falhar devido a um conflito com os dados subjacentes (por exemplo, um registro já foi excluído por outro usuário), o provedor retornará avisos para o **erros** coleção, mas não pare o programa execução. Um erro de tempo de execução ocorre somente se houver conflitos em todos os registros solicitados.  
  
 Se o **tabela exclusiva** dinâmico está definida e o **registros** é o resultado da execução de uma operação de junção em várias tabelas, o **excluir** método excluirá linhas somente da tabela nomeada no **tabela exclusiva** propriedade.  
  
 O **excluir** método usa um argumento opcional que permite que você especifique quais registros são afetados pelo **excluir** operação. Os únicos valores válidos para esse argumento são qualquer uma das seguinte ADO **AffectEnum** constantes enumeradas:  
  
-   **adAffectCurrent** afeta somente o registro atual.  
  
-   **adAffectGroup** afeta somente os registros que satisfazem atual **filtro** configuração de propriedade. O **filtro** propriedade deve ser definida um **FilterGroupEnum** valor ou uma matriz de **indicadores** para usar essa opção.  
  
 O código a seguir mostra um exemplo da especificação **adAffectGroup** ao chamar o **excluir** método. Este exemplo adiciona alguns registros para o exemplo **registros** e atualiza o banco de dados. Em seguida, ele filtra o **registros** usando o **adFilterAffectedRecords** constante enumerada filtro, que deixa somente novos registros visíveis no **conjunto de registros.** Finalmente, ele chama o **excluir** método e especifica que todos os registros que atendem a atual **filtro** (os novos registros) de configuração de propriedade deve ser excluída.  
  
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
