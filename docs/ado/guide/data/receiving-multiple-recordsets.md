---
title: "Receber vários conjuntos de registros | Microsoft Docs"
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
- receiving multiple Recordsets [ADO]
- Recordset object [ADO], receiving multiple Recordsets
ms.assetid: 2a7ad7a6-f00d-4355-b0b5-d0ab957b0566
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ab72906b1f36e22bba58b58ca7917b3399ebc458
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="receiving-multiple-recordsets"></a>Receber vários conjuntos de registros
O [Microsoft OLE DB Provider para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) dá suporte a retorno de vários **registros** objetos de um único comando que contém várias instruções SQL, um **registros**por instrução SQL. A ordem na qual o **registros**s serão retornados segue a ordem na qual as instruções SQL são colocadas no texto do comando.  
  
 O Microsoft OLE DB Provider para SQL Server também retorna vários conjuntos de resultados para o ADO quando o comando contém uma cláusula COMPUTE. Por exemplo, um comando que contém a instrução SQL a seguir retornará os resultados em duas **registros** objetos: uma para o conjunto de linhas (*ProductID*, *ProductName*, *UnitPrice*) e outro para o preço médio de todos os produtos na tabela.  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 Você pode usar o **Recordset.NextRecordset** método para enumerar os dois objetos.  
  
 Para obter mais informações, consulte [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md).

