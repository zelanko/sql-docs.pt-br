---
description: Método DeleteRecord (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 94423c36dd89d6ea14ea39b7546ef1a5bef7c620
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444098"
---
# <a name="deleterecord-method-ado"></a>Método DeleteRecord (ADO)
Exclui uma entidade representada por um [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Record.DeleteRecord Source, Async  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Opcional. Um valor de **cadeia de caracteres** que contém uma URL que identifica a entidade (por exemplo, o arquivo ou diretório) a ser excluída. Se a *origem* for omitida ou especificar uma cadeia de caracteres vazia, a entidade representada pelo [registro](../../../ado/reference/ado-api/record-object-ado.md) atual será excluída. Se o registro for um registro de coleção ([RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md) de **adCollectionRecord**, como um diretório), todos os filhos (por exemplo, subdiretórios) também serão excluídos.  
  
 *Async*  
 Opcional. Um valor **booliano** que, quando **true**, especifica que a operação de exclusão é assíncrona.  
  
## <a name="remarks"></a>Comentários  
 As operações no objeto representado por esse **registro** podem falhar após a conclusão desse método. Depois de chamar **DeleteRecord**, o **registro** deve ser fechado porque o comportamento do **registro** pode se tornar imprevisível, dependendo de quando o provedor atualizar o **registro** com a fonte de dados.  
  
 Se esse **registro** foi obtido de um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md), os resultados dessa operação não serão refletidos imediatamente no **conjunto de registros**. Atualize o **conjunto de registros** fechando-o e reabrindo-o, ou executando o método [Requery](../../../ado/reference/ado-api/requery-method.md) do **conjunto de registros** , o método [Update](../../../ado/reference/ado-api/update-method.md) ou o método [Ressync](../../../ado/reference/ado-api/resync-method.md) .  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método Delete (coleção de campos ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Método Delete (coleção de parâmetros ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Método Delete (Conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)
