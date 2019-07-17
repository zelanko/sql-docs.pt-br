---
title: Método DeleteRecord (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_DeleteRecord
- _Record::DeleteRecord
helpviewer_keywords:
- DeleteRecord method [ADO]
ms.assetid: 2726498c-dbd8-4266-983b-ae7d62c39142
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 409c4e21395b7b903cf4ff03726fbd37a2a218d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919079"
---
# <a name="deleterecord-method-ado"></a>Método DeleteRecord (ADO)
Exclui uma entidade representada por uma [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Record.DeleteRecord Source, Async  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Source*  
 Opcional. Um **cadeia de caracteres** valor que contém uma URL que identifica a entidade (por exemplo, o arquivo ou diretório) a ser excluído. Se *fonte* for omitido ou especifica uma cadeia de caracteres vazia, a entidade representada por atual [registro](../../../ado/reference/ado-api/record-object-ado.md) é excluído. Se o registro é um registro de coleção ([RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md) dos **adCollectionRecord**, como um diretório) todos os filhos (por exemplo, subdiretórios) também serão excluídos.  
  
 *Async*  
 Opcional. Um **Boolean** valor que, quando **verdadeiro**, especifica que a operação de exclusão é assíncrona.  
  
## <a name="remarks"></a>Comentários  
 Operações no objeto representado por este **registro** pode falhar após a conclusão desse método. Depois de chamar **DeleteRecord**, o **registro** deve ser fechado porque o comportamento dos **registro** podem se tornar imprevisível dependendo de quando o provedor de atualizações a **Registro** com a fonte de dados.  
  
 Se este **registro** foi obtido um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md), em seguida, os resultados dessa operação não serão refletidos imediatamente no **conjunto de registros**. Atualizar o **conjunto de registros** fechando e abri-lo novamente, ou executando o **conjunto de registros** [Requery](../../../ado/reference/ado-api/requery-method.md) método, o [atualização](../../../ado/reference/ado-api/update-method.md) método, ou o [Ressincronizar](../../../ado/reference/ado-api/resync-method.md) método.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [absoluta e relativa URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método Delete (coleção de campos ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Excluir método (coleção de parâmetros ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Método Delete (Conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)
