---
title: "Reformatação | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reshaping previously shaped Recordset [ADO]
- data shaping [ADO], reshaping
ms.assetid: b1c965b7-3dad-4de6-9e0e-502ca8785be3
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d5264de973e4ed36cc24eb5c535576bdfa0a7228
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="reshaping"></a>Reformatação
Um **registros** criado por uma cláusula de uma forma de comando pode ser atribuído um *alias* nome (normalmente com a palavra-chave). O alias de uma forma **registros** podem ser referenciados em um comando completamente diferente. Ou seja, você pode reutilizar, ou *remodelar*, anteriormente com um formato **registros** em um novo comando de forma. Para dar suporte a esse recurso, o ADO fornece uma propriedade, [nome remodelar](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md).  
  
 Reformatação tem duas funções principais. A primeira é para associar um existente **registros** com um novo pai **registros**.  
  
## <a name="example"></a>Exemplo  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 A segunda função é permitir o acesso não tem capítulos filho existente **registros** objetos, usando a sintaxe "forma \<recordset remodelar nome >".  
  
> [!NOTE]
>  Não é possível acrescentar colunas a uma **Recordset**, reformatar um parametrizadas **Recordset** ou o **Recordset** objetos em qualquer cláusula COMPUTE intermediária ou executar agregar operações em qualquer **registros** descendente do **registros** sendo reformatado. O **registros** sendo reformatado e a nova forma de comando devem usar o mesmo [Conexão](../../../ado/reference/ado-api/connection-object-ado.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de data shaping](../../../ado/guide/data/data-shaping-example.md)

