---
title: Método Clear (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Errors::raw_Clear
- Errors::Clear
helpviewer_keywords:
- Clear method [ADO]
ms.assetid: 0a61ba7a-20b8-426a-91a0-9040e7c5a98a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 96bd13f130966b1830d07e49633842e4154b52b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920061"
---
# <a name="clear-method-ado"></a>Método Clear (ADO)
Remove todos os objetos de [erro](../../../ado/reference/ado-api/error-object.md) da coleção de [erros](../../../ado/reference/ado-api/errors-collection-ado.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>Comentários  
 Use o método **Clear** na coleção de [erros](../../../ado/reference/ado-api/errors-collection-ado.md) para remover todos os objetos de [erro](../../../ado/reference/ado-api/error-object.md) existentes da coleção. Quando ocorre um erro, o ADO limpa automaticamente a coleção de **erros** e a preenche com objetos de **erro** com base no novo erro.  
  
 Algumas propriedades e métodos retornam avisos que aparecem como objetos de **erro** na coleção de **erros** , mas não interrompem a execução de um programa. Antes de chamar os métodos [Ressync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) em um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ; o método [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) em um objeto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) ; ou defina a propriedade [Filter](../../../ado/reference/ado-api/filter-property.md) em um objeto **Recordset** , chame o método **Clear** na coleção **Errors** . Dessa forma, você pode ler a propriedade [Count](../../../ado/reference/ado-api/count-property-ado.md) da coleção de **erros** para testar os avisos retornados.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Errors (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Execute, Requery e Clear (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Exemplo dos métodos Execute, Requery e Clear (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Exemplo dos métodos Execute, Requery e Clear (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método Delete (coleção de campos ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Método Delete (coleção de parâmetros ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Método Delete (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Propriedade de filtro](../../../ado/reference/ado-api/filter-property.md)   
 [Método de ressincronização](../../../ado/reference/ado-api/resync-method.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
