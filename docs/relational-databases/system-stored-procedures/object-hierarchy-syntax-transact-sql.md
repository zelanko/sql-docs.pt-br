---
title: Sintaxe de hierarquia (Transact-SQL) do objeto | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], hierarchy syntax
ms.assetid: 7ed8df86-9fd2-4e09-96bc-5381fec85f65
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3fe5e6b71836854fc6cdcc409e61ef1936641def
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47679644"
---
# <a name="object-hierarchy-syntax-transact-sql"></a>Sintaxe da hierarquia de objetos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  O *propertyname* parâmetro de sp_OAGetProperty e sp_OASetProperty e o *methodname* parâmetro de sp_OAMethod dá suporte a uma sintaxe de hierarquia de objeto que é semelhante do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Quando essa sintaxe especial for usada, esses parâmetros têm o seguinte formato geral.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
'TraversedObject.PropertyOrMethod'  
```  
  
## <a name="arguments"></a>Argumentos  
 *TraversedObject*  
 É um objeto OLE na hierarquia sob a *objecttoken* especificado no procedimento armazenado. Use a sintaxe do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para especificar uma série de coleções, propriedades de objeto e métodos que retornam objetos. Cada especificador de objeto na série deve ser separado por um ponto (.).  
  
 Um item na série pode ser o nome de uma coleção. Use esta sintaxe para especificar uma coleção:  
  
 Coleção ("*item*")  
  
 As aspas duplas (") são necessárias. O [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] não há suporte para a sintaxe de ponto de exclamação (!) para coleções.  
  
 *PropertyOrMethod*  
 É o nome de uma propriedade ou método as *TraversedObject*.  
  
 Para especificar todos os parâmetros de método ou índice usando os parâmetros de sp_OAGetProperty, sp_OASetProperty ou sp_OAMethod (incluindo suporte para parâmetros de saída sp_OAMethod), use a seguinte sintaxe:  
  
 *PropertyOrMethod*  
  
 Para especificar o método ou índice de todos os parâmetros dentro dos parênteses (fazendo com que todos os parâmetros de método ou índice de sp_OAGetProperty, sp_OASetProperty ou sp_OAMethod sejam ignorados) usam a seguinte sintaxe:  
  
 *PropertyOrMethod*([ *ParameterName*: =] "*parâmetro*" [,...])  
  
 As aspas duplas (") são necessárias. Todos os parâmetros nomeados deverão ser especificados depois que todos os parâmetros posicionais forem especificados.  
  
## <a name="remarks"></a>Comentários  
 Se *TraversedObject* não for especificado, *PropertyOrMethod* é necessária.  
  
 Se *PropertyOrMethod* não for especificado, o *TraversedObject* é retornado como um parâmetro de saída de token de objeto do procedimento armazenado de automação OLE. Se *PropertyOrMethod* for especificado, a propriedade ou método da *TraversedObject* é chamado, e o valor da propriedade ou o valor retornado do método é retornado como um parâmetro de saída de automação OLE procedimento armazenado.  
  
 Se qualquer item na *TraversedObject* lista não retorna um objeto OLE, ocorrerá um erro.  
  
 Para obter mais informações sobre a sintaxe de objeto OLE do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], consulte a documentação do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].  
  
 Para obter mais informações sobre códigos de retorno HRESULT, consulte [sp_OACreate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 A seguir estão exemplos de sintaxe da hierarquia de objeto que usam um objeto SQL-DMO SQLServer.  
  
```  
-- Get the AdventureWorks2012 Person.Address Table object.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address")',  
   @table OUT  
  
-- Get the Rows property of the AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").Rows',  
   @rows OUT  
  
-- Call the CheckTable method to validate the   
-- AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAMethod @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").CheckTable',  
   @checkoutput OUT  
```  
  
## <a name="see-also"></a>Consulte também  
 [Script de exemplo de automação OLE](../../relational-databases/stored-procedures/ole-automation-sample-script.md)   
 [Procedimentos armazenados de Automação OLE &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
  
