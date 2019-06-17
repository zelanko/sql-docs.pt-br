---
title: Remodelagem | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- reshaping previously shaped Recordset [ADO]
- data shaping [ADO], reshaping
ms.assetid: b1c965b7-3dad-4de6-9e0e-502ca8785be3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6d7137d67c14cd435ffe814a3bfbf0e42a7be976
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700431"
---
# <a name="reshaping"></a>Remodelagem
Um **conjunto de registros** criado por uma cláusula de uma forma de comando pode ser atribuído uma *alias* nome (normalmente com a palavra-chave). O alias de um moldado **Recordset** pode ser referenciada em um comando completamente diferente. Ou seja, você pode reutilizar, ou *remodelar*, anteriormente moldado **conjunto de registros** em um novo comando de forma. Para dar suporte a esse recurso, o ADO oferece uma propriedade, [remodelar nome](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md).  
  
 Remodelagem tem duas funções principais. A primeira é associar um existente **conjunto de registros** com um novo pai **conjunto de registros**.  
  
## <a name="example"></a>Exemplo  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 A segunda função é permitir o acesso não dividido em capítulos filho existentes **conjunto de registros** objetos, usando a sintaxe "forma \<recordset remodelar nome >".  
  
> [!NOTE]
>  Não é possível acrescentar colunas a um existente **conjunto de registros**, reformatar um parametrizada **conjunto de registros** ou o **Recordset** objetos em qualquer cláusula de computação intermediária ou executar agregar operações em qualquer **conjunto de registros** entre o **conjunto de registros** sendo reformatado. O **conjunto de registros** sendo reformatado e a nova forma de comando devem usar o mesmo [Conexão](../../../ado/reference/ado-api/connection-object-ado.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de data shaping](../../../ado/guide/data/data-shaping-example.md)
