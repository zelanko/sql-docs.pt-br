---
title: Excluir método (conjunto de registros ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Delete
- Recordset15::Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 1eb9209c-602c-4507-b0c2-6527a599b67d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 272b953a39a9ccbb01d94acc59d374304bda3ad0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770330"
---
# <a name="delete-method-ado-recordset"></a>Método Delete (Conjunto de registros ADO)
Exclui o registro atual ou um grupo de registros.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *AffectRecords*  
 Uma [AffectEnum](../../../ado/reference/ado-api/affectenum.md) valor que determina quantos registros o **excluir** método afetará. O valor padrão é **adAffectCurrent**.  
  
> [!NOTE]
>  **adAffectAll** e **adAffectAllChapters** não são argumentos válidos **excluir**.  
  
## <a name="remarks"></a>Comentários  
 Usando o **exclua** método marca o registro atual ou um grupo de registros em uma [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto para exclusão. Se o **Recordset** objeto não permite exclusão de registros, ocorrerá um erro. Se você estiver no modo de atualização imediata, exclusões ocorrem no banco de dados imediatamente. Se um registro não pode ser excluído com êxito (devido a violações de integridade de banco de dados, por exemplo), o registro permanecerá no modo de edição após a chamada para [atualização](../../../ado/reference/ado-api/update-method.md). Isso significa que você deve cancelar a atualização com [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) antes de passar fora do registro atual (por exemplo, com [Close](../../../ado/reference/ado-api/close-method-ado.md), [mover](../../../ado/reference/ado-api/move-method-ado.md), ou [ NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 Se você estiver no modo de atualização em lotes, os registros marcados para exclusão do cache e a exclusão real acontece quando você chama o [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método. Use o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade para exibir os registros excluídos.  
  
 Recuperar valores de campo do registro excluído gera um erro. Depois de excluir o registro atual, o registro excluído permanece atual até que você mova para um registro diferente. Quando você se afasta o registro excluído, ele não está mais acessível.  
  
 Se você aninhar exclusões em uma transação, você pode recuperar registros excluídos com o [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) método. Se você estiver no modo de atualização em lotes, você pode cancelar uma exclusão pendente ou o grupo de pendentes exclusões com o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) método.  
  
 Se a tentativa de excluir registros falhar devido a um conflito com os dados subjacentes (por exemplo, um registro já foi excluído por outro usuário), o provedor retornará avisos para o [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção, mas não interromper o programa execução. Um erro de tempo de execução ocorre somente se houver conflitos em todos os registros solicitados.  
  
 Se o [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) dinâmica propriedade for definida e o **conjunto de registros** é o resultado da execução de uma operação de junção em várias tabelas, em seguida, a **excluir** método excluirá apenas linhas da tabela nomeada na [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) propriedade.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Excluir exemplo de método (VB)](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [Excluir exemplo de método (VBScript)](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [Excluir exemplo de método (VC + +)](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Método Delete (coleção de campos ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Excluir método (coleção de parâmetros ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Método DeleteRecord (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
