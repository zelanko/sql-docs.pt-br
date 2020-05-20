---
title: Reshaping | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e0328b7a09f18cde0043cfbcc21d2dceb4893442
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760932"
---
# <a name="reshaping"></a>Remodelagem
Um **conjunto de registros** criado por uma cláusula de um comando Shape pode ser atribuído a um nome de *alias* (normalmente com a palavra-chave as). O alias de um **conjunto de registros** moldado pode ser referenciado em um comando completamente diferente. Ou seja, você pode reutilizar ou *remodelar*um conjunto de **registros** moldado anteriormente em um comando de nova forma. Para dar suporte a esse recurso, o ADO fornece uma propriedade, [reformando o nome](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md).  
  
 A remodelagem tem duas funções principais. A primeira é associar um conjunto de **registros** existente a um novo **conjunto de registros**pai.  
  
## <a name="example"></a>Exemplo  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 A segunda função é habilitar o acesso não-capítulo a objetos existentes do **conjunto de registros** filho, usando a sintaxe " \< nome da forma de remodelação do conjunto de registros da forma>".  
  
> [!NOTE]
>  Não é possível acrescentar colunas a um **conjunto de registros**existente, remodelar um **conjunto de registros** com parâmetros ou os objetos **RECORDSET** em qualquer cláusula de computação intermediária ou executar operações de agregação em qualquer descendente de **conjunto** de registros do **conjunto de registros** que está sendo remodelado. O **conjunto de registros** que está sendo remodelado e o comando de nova forma devem usar a mesma [conexão](../../../ado/reference/ado-api/connection-object-ado.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de data shaping](../../../ado/guide/data/data-shaping-example.md)
