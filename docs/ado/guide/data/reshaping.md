---
description: Remodelagem
title: Reshaping | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 04c43b9fcca56959aec242f344da6ec81a825030
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979767"
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
  
 A segunda função é habilitar o acesso não-capítulo a objetos conjuntos de **registros** filho existentes, usando a sintaxe "Shape \<recordset reshape name> ".  
  
> [!NOTE]
>  Não é possível acrescentar colunas a um **conjunto de registros**existente, remodelar um **conjunto de registros** com parâmetros ou os objetos **RECORDSET** em qualquer cláusula de computação intermediária ou executar operações de agregação em qualquer descendente de **conjunto** de registros do **conjunto de registros** que está sendo remodelado. O **conjunto de registros** que está sendo remodelado e o comando de nova forma devem usar a mesma [conexão](../../../ado/reference/ado-api/connection-object-ado.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de data shaping](../../../ado/guide/data/data-shaping-example.md)
