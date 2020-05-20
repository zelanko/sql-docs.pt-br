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
author: rothja
ms.author: jroth
ms.openlocfilehash: a8da01b9c92aeec9c01527370e19c8edfb751da9
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763617"
---
# <a name="deleting-records-using-the-delete-method"></a>Excluir registros usando o método Delete
O uso do método **delete** marca o registro atual ou um grupo de registros em um objeto **Recordset** para exclusão. Se o objeto **Recordset** não permitir a exclusão de registros, ocorrerá um erro. Se você estiver no modo de atualização imediata, as exclusões ocorrerão imediatamente no banco de dados. Se um registro não puder ser excluído com êxito (devido a violações de integridade do banco de dados, por exemplo), o registro permanecerá no modo de edição após a chamada para **Atualizar.** Isso significa que você deve cancelar a atualização usando [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) antes de sair do registro atual (por exemplo, usando [fechar](../../../ado/reference/ado-api/close-method-ado.md), [mover](../../../ado/reference/ado-api/move-method-ado.md)ou [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 Se você estiver no modo de atualização do lote, os registros serão marcados para exclusão do cache e a exclusão real ocorrerá quando você chamar o método **UpdateBatch** . (Para exibir os registros excluídos, defina a propriedade de **filtro** para **AdFilterAffectedRecords** após a **exclusão** ser chamada.)  
  
 A tentativa de recuperar valores de campo do registro excluído gera um erro. Depois de excluir o registro atual, o registro excluído permanece atual até que você se mova para um registro diferente. Quando você sai do registro excluído, ele não é mais acessível.  
  
 Se você aninhar exclusões em uma transação, poderá recuperar os registros excluídos usando o método **RollbackTrans** . Se você estiver no modo de atualização do lote, poderá cancelar uma exclusão pendente ou grupo de exclusões pendentes usando o método **CancelBatch** .  
  
 Se a tentativa de excluir registros falhar devido a um conflito com os dados subjacentes (por exemplo, um registro já foi excluído por outro usuário), o provedor retornará avisos para a coleção de **erros** , mas não interromperá a execução do programa. Um erro de tempo de execução ocorrerá somente se houver conflitos em todos os registros solicitados.  
  
 Se a propriedade dinâmica da **tabela exclusiva** for definida e o **conjunto de registros** for o resultado da execução de uma operação de junção em várias tabelas, o método **delete** excluirá linhas somente da tabela nomeada na propriedade **Table exclusiva** .  
  
 O método **delete** usa um argumento opcional que permite especificar quais registros são afetados pela operação de **exclusão** . Os únicos valores válidos para esse argumento são das seguintes constantes enumeradas do ADO **AffectEnum** :  
  
-   **adAffectCurrent** Afeta apenas o registro atual.  
  
-   **adAffectGroup** Afeta somente os registros que atendem à configuração de propriedade de **filtro** atual. A propriedade **Filter** deve ser definida como um valor **FilterGroupEnum** ou uma matriz de **indicadores** para usar essa opção.  
  
 O código a seguir mostra um exemplo de especificação de **adAffectGroup** ao chamar o método **delete** . Este exemplo adiciona alguns registros ao conjunto de **registros** de exemplo e atualiza o banco de dados. Em seguida, ele filtra o **conjunto de registros** usando a constante enumerada do filtro **adFilterAffectedRecords** , que deixa apenas os registros recém-adicionados visíveis no **conjunto de registros.** Por fim, ele chama o método **delete** e especifica que todos os registros que satisfazem a configuração de propriedade de **filtro** atual (os novos registros) devem ser excluídos.  
  
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
