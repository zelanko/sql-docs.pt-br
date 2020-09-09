---
description: Sintaxe da hierarquia de objetos (Transact-SQL)
title: Sintaxe de hierarquia de objeto (Transact-SQL) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 81db44bae57dec8bb0298e872221998ac45e0a3a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542049"
---
# <a name="object-hierarchy-syntax-transact-sql"></a>Sintaxe da hierarquia de objetos (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  O parâmetro *PropertyName* de sp_OAGetProperty e sp_OASetProperty e o parâmetro *MethodName* de sp_OAMethod dão suporte a uma sintaxe de hierarquia de objeto semelhante à do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] . Quando essa sintaxe especial for usada, esses parâmetros têm o seguinte formato geral.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
'TraversedObject.PropertyOrMethod'  
```  
  
## <a name="arguments"></a>Argumentos  
 *TraversedObject*  
 É um objeto OLE na hierarquia sob o *objecttoken* especificado no procedimento armazenado. Use a sintaxe do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para especificar uma série de coleções, propriedades de objeto e métodos que retornam objetos. Cada especificador de objeto na série deve ser separado por um ponto (.).  
  
 Um item na série pode ser o nome de uma coleção. Use esta sintaxe para especificar uma coleção:  
  
 Coleção ("*Item*")  
  
 As aspas duplas (") são necessárias. [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]Não há suporte para a sintaxe do ponto de exclamação (!) para coleções.  
  
 *PropertyOrMethod*  
 É o nome de uma propriedade ou método do *TraversedObject*.  
  
 Para especificar todos os parâmetros de método ou índice com o uso dos parâmetros sp_OAGetProperty, sp_OASetProperty ou sp_OAMethod (incluindo suporte para parâmetros de saída sp_OAMethod), use a seguinte sintaxe:  
  
 *PropertyOrMethod*  
  
 Para especificar todos os parâmetros de método ou índice dentro dos parênteses (fazendo com que todos os parâmetros de método ou índice de sp_OAGetProperty, sp_OASetProperty ou sp_OAMethod sejam ignorados) use a seguinte sintaxe:  
  
 *PropertyOrMethod*([ *ParameterName*: =] "*parâmetro*" [,...])  
  
 As aspas duplas (") são necessárias. Todos os parâmetros nomeados deverão ser especificados depois que todos os parâmetros posicionais forem especificados.  
  
## <a name="remarks"></a>Comentários  
 Se *TraversedObject* não for especificado, *PropertyOrMethod* será necessário.  
  
 Se *PropertyOrMethod* não for especificado, o *TraversedObject* será retornado como um parâmetro de saída de token de objeto do procedimento armazenado de automação OLE. Se *PropertyOrMethod* for especificado, a propriedade ou o método de *TraversedObject* será chamado, e o valor da propriedade ou o valor de retorno do método será retornado como um parâmetro de saída do procedimento armazenado de automação OLE.  
  
 Se qualquer item na lista *TraversedObject* não retornar um objeto OLE, um erro será gerado.  
  
 Para obter mais informações sobre a sintaxe de objeto OLE do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], consulte a documentação do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].  
  
 Para obter mais informações sobre códigos de retorno HRESULT, consulte [sp_OACreate &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 A seguir são fornecidos exemplos de sintaxe de hierarquia de objeto que usam um objeto SQL-DMO SQLServer.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Script de exemplo de automação OLE](../../relational-databases/stored-procedures/ole-automation-sample-script.md)   
 [Procedimentos armazenados de Automação OLE &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
  
