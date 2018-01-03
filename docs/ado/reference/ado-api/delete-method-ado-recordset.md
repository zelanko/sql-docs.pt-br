---
title: "Método (conjunto de registros ADO) Delete | Microsoft Docs"
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
apitype: COM
f1_keywords:
- Recordset15::raw_Delete
- Recordset15::Delete
helpviewer_keywords: Delete method [ADO]
ms.assetid: 1eb9209c-602c-4507-b0c2-6527a599b67d
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ff78b2827f8bd6aa22ded6429f0468617b7a83d9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="delete-method-ado-recordset"></a>Excluir método (conjunto de registros ADO)
Exclui o registro atual ou um grupo de registros.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *AffectRecords*  
 Um [AffectEnum](../../../ado/reference/ado-api/affectenum.md) valor que determina quantos registros o **excluir** método afetará. O valor padrão é **adAffectCurrent**.  
  
> [!NOTE]
>  **adAffectAll** e **adAffectAllChapters** não são argumentos válidos para **excluir**.  
  
## <a name="remarks"></a>Remarks  
 Usando o **excluir** método marca o registro atual ou um grupo de registros em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto para exclusão. Se o **registros** objeto não permite exclusão do registro, ocorrerá um erro. Se você estiver no modo de atualização imediata, exclusões ocorrerem no banco de dados imediatamente. Se um registro não pode ser excluído com êxito (devido a violações de integridade de banco de dados, por exemplo), o registro permanecerá no modo de edição após a chamada a [atualização](../../../ado/reference/ado-api/update-method.md). Isso significa que você deve cancelar a atualização com [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) antes de mover fora do registro atual (por exemplo, com [fechar](../../../ado/reference/ado-api/close-method-ado.md), [mover](../../../ado/reference/ado-api/move-method-ado.md), ou [ NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 Se você estiver no modo de atualização em lotes, os registros marcados para exclusão do cache e a exclusão real acontece quando você chamar o [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método. Use o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade para exibir os registros excluídos.  
  
 Recuperando valores de campo do registro excluído gera um erro. Depois de excluir o registro atual, o registro excluído permanece atual até que você mova para um registro diferente. Uma vez sair de registro excluído, ele não é mais acessível.  
  
 Se você aninhar exclusões em uma transação, você pode recuperar os registros excluídos com o [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) método. Se você estiver no modo de atualização em lotes, você pode cancelar uma exclusão pendente ou grupo de pendente exclusões com o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) método.  
  
 Se a tentativa de excluir registros falhar devido a um conflito com os dados subjacentes (por exemplo, um registro já foi excluído por outro usuário), o provedor retornará avisos para o [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção, mas não pare o programa execução. Um erro de tempo de execução ocorre somente se houver conflitos em todos os registros solicitados.  
  
 Se o [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) propriedade dinâmica estiver definida e o **registros** é o resultado da execução de uma operação de junção em várias tabelas, o **excluir** método excluirá apenas linhas da tabela nomeada no [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) propriedade.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Excluir exemplo de método (VB)](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [Excluir exemplo de método (VBScript)](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [Excluir exemplo de método (VC + +)](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Método Delete (coleção de campos do ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Excluir método (coleção de parâmetros do ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Método DeleteRecord (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
