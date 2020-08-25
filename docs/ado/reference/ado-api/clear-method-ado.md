---
description: Método Clear (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8b7ed940248230d1c7b74f6782abcb555a538021
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776265"
---
# <a name="clear-method-ado"></a>Método Clear (ADO)
Remove todos os objetos de [erro](./error-object.md) da coleção de [erros](./errors-collection-ado.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>Comentários  
 Use o método **Clear** na coleção de [erros](./errors-collection-ado.md) para remover todos os objetos de [erro](./error-object.md) existentes da coleção. Quando ocorre um erro, o ADO limpa automaticamente a coleção de **erros** e a preenche com objetos de **erro** com base no novo erro.  
  
 Algumas propriedades e métodos retornam avisos que aparecem como objetos de **erro** na coleção de **erros** , mas não interrompem a execução de um programa. Antes de chamar os métodos [Ressync](./resync-method.md), [UpdateBatch](./updatebatch-method.md)ou [CancelBatch](./cancelbatch-method-ado.md) em um objeto [Recordset](./recordset-object-ado.md) ; o método [Open](./open-method-ado-connection.md) em um objeto [Connection](./connection-object-ado.md) ; ou defina a propriedade [Filter](./filter-property.md) em um objeto **Recordset** , chame o método **Clear** na coleção **Errors** . Dessa forma, você pode ler a propriedade [Count](./count-property-ado.md) da coleção de **erros** para testar os avisos retornados.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Errors (ADO)](./errors-collection-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Execute, Requery e Clear (VB)](./execute-requery-and-clear-methods-example-vb.md)   
 [Exemplo dos métodos Execute, Requery e Clear (VBScript)](./execute-requery-and-clear-methods-example-vbscript.md)   
 [Exemplo dos métodos Execute, Requery e Clear (VC + +)](./execute-requery-and-clear-methods-example-vc.md)   
 [Método CancelBatch (ADO)](./cancelbatch-method-ado.md)   
 [Método Delete (coleção de campos ADO)](./delete-method-ado-fields-collection.md)   
 [Método Delete (coleção de parâmetros ADO)](./delete-method-ado-parameters-collection.md)   
 [Método Delete (conjunto de registros ADO)](./delete-method-ado-recordset.md)   
 [Propriedade de filtro](./filter-property.md)   
 [Método de ressincronização](./resync-method.md)   
 [Método UpdateBatch](./updatebatch-method.md)