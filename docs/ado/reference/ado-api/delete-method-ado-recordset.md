---
description: Método Delete (Conjunto de registros ADO)
title: Método Delete (conjunto de registros ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a43aa64d970865b8de706fc4297bba9fd0d18786
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974087"
---
# <a name="delete-method-ado-recordset"></a>Método Delete (Conjunto de registros ADO)
Exclui o registro atual ou um grupo de registros.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *AffectRecords*  
 Um valor [AffectEnum](../../../ado/reference/ado-api/affectenum.md) que determina quantos registros o método **delete** afetará. O valor padrão é **adAffectCurrent**.  
  
> [!NOTE]
>  **adAffectAll** e **adAffectAllChapters** não são argumentos válidos para **exclusão**.  
  
## <a name="remarks"></a>Comentários  
 O uso do método **delete** marca o registro atual ou um grupo de registros em um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) para exclusão. Se o objeto **Recordset** não permitir a exclusão de registros, ocorrerá um erro. Se você estiver no modo de atualização imediata, as exclusões ocorrerão imediatamente no banco de dados. Se um registro não puder ser excluído com êxito (devido a violações de integridade do banco de dados, por exemplo), o registro permanecerá no modo de edição após a chamada para [Atualizar](../../../ado/reference/ado-api/update-method.md). Isso significa que você deve cancelar a atualização com [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) antes de sair do registro atual (por exemplo, com [fechar](../../../ado/reference/ado-api/close-method-ado.md), [mover](../../../ado/reference/ado-api/move-method-ado.md)ou [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 Se você estiver no modo de atualização do lote, os registros serão marcados para exclusão do cache e a exclusão real ocorrerá quando você chamar o método [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) . Use a propriedade [filtro](../../../ado/reference/ado-api/filter-property.md) para exibir os registros excluídos.  
  
 A recuperação de valores de campo do registro excluído gera um erro. Depois de excluir o registro atual, o registro excluído permanece atual até que você se mova para um registro diferente. Quando você sai do registro excluído, ele não é mais acessível.  
  
 Se você aninhar exclusões em uma transação, poderá recuperar registros excluídos com o método [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) . Se você estiver no modo de atualização do lote, poderá cancelar uma exclusão pendente ou grupo de exclusões pendentes com o método [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) .  
  
 Se a tentativa de excluir registros falhar devido a um conflito com os dados subjacentes (por exemplo, um registro já foi excluído por outro usuário), o provedor retornará avisos para a coleção de [erros](../../../ado/reference/ado-api/errors-collection-ado.md) , mas não interromperá a execução do programa. Um erro de tempo de execução ocorrerá somente se houver conflitos em todos os registros solicitados.  
  
 Se a propriedade dinâmica da [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) for definida e o **conjunto de registros** for o resultado da execução de uma operação JOIN em várias tabelas, o método **delete** excluirá somente as linhas da tabela denominada na propriedade [Table exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Delete (VB)](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [Exemplo do método Delete (VBScript)](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [Exemplo do método Delete (VC + +)](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Método Delete (coleção de campos ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Método Delete (coleção de parâmetros ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Método DeleteRecord (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
