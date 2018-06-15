---
title: Método ExcluirRegistro (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_DeleteRecord
- _Record::DeleteRecord
helpviewer_keywords:
- DeleteRecord method [ADO]
ms.assetid: 2726498c-dbd8-4266-983b-ae7d62c39142
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 168b53d0ad68f55656e005f7523a0c09ba599004
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277635"
---
# <a name="deleterecord-method-ado"></a>Método ExcluirRegistro (ADO)
Exclui uma entidade representada por um [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Record.DeleteRecord Source, Async  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Opcional. Um **cadeia de caracteres** valor que contém uma URL que identifica a entidade (por exemplo, o arquivo ou diretório) a ser excluído. Se *fonte* for omitido ou especifica uma cadeia de caracteres vazia, a entidade representada por atual [registro](../../../ado/reference/ado-api/record-object-ado.md) é excluído. Se o registro é um registro de coleção ([RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md) de **adCollectionRecord**, como um diretório) todos os filhos (por exemplo, subdiretórios) também serão excluídos.  
  
 *Async*  
 Opcional. Um **booliano** valor que, quando **True**, especifica que a operação de exclusão é assíncrona.  
  
## <a name="remarks"></a>Remarks  
 Operações no objeto representado por esse **registro** pode falhar depois que esse método é concluído. Depois de chamar **ExcluirRegistro**, o **registro** devem ser fechados porque o comportamento do **registro** pode se tornar imprevisível dependendo de quando o provedor de atualizações do **Registro** com a fonte de dados.  
  
 Se este **registro** foi obtido um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), em seguida, os resultados dessa operação não serão refletidos imediatamente no **conjunto de registros**. Atualizar o **registros** , feche e reabra-lo, ou executando o **registros** [Requery](../../../ado/reference/ado-api/requery-method.md) método, o [atualização](../../../ado/reference/ado-api/update-method.md) método, ou o [Resync](../../../ado/reference/ado-api/resync-method.md) método.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [Absolute e URLs relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método Delete (coleção de campos do ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Excluir método (coleção de parâmetros do ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Método Delete (Conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)
