---
title: "Método (ADO) Clear | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Errors::raw_Clear
- Errors::Clear
helpviewer_keywords:
- Clear method [ADO]
ms.assetid: 0a61ba7a-20b8-426a-91a0-9040e7c5a98a
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 831ec9b295ca4e3d81707cfc2c1cc14169d1527c
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="clear-method-ado"></a>Método Clear (ADO)
Remove todos os [erro](../../../ado/reference/ado-api/error-object.md) objetos do [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>Comentários  
 Use o **limpar** método o [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção para remover todas as existentes [erro](../../../ado/reference/ado-api/error-object.md) objetos da coleção. Quando ocorre um erro, ADO limpa automaticamente o **erros** coleção e a preenche com **erro** objetos com base no novo erro.  
  
 Algumas propriedades e métodos retornam os avisos que aparecem como **erro** objetos no **erros** coleção, mas não interromper a execução do programa. Antes de chamar o [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) métodos em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto; o [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método em um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto; ou defina o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade em uma **Recordset** de objeto, chame o **limpar**método sobre o **erros** coleção. Dessa forma, você pode ler o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade o **erros** avisos retornados de coleção para testar.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Errors (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Execute, repetir e limpar o exemplo de métodos (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute, repetir e limpar o exemplo de métodos (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, repetir e limpar o exemplo de métodos (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método Delete (coleção de campos do ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Excluir método (coleção de parâmetros do ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Excluir método (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Propriedade de filtro](../../../ado/reference/ado-api/filter-property.md)   
 [Sincronizar de método](../../../ado/reference/ado-api/resync-method.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)

