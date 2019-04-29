---
title: Recebendo vários conjuntos de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving multiple Recordsets [ADO]
- Recordset object [ADO], receiving multiple Recordsets
ms.assetid: 2a7ad7a6-f00d-4355-b0b5-d0ab957b0566
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e70dc047456549b625a1e66250d413009293f4a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62910815"
---
# <a name="receiving-multiple-recordsets"></a>Receber vários conjuntos de registros
O [Microsoft OLE DB Provider para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) dá suporte ao retorno de vários **conjunto de registros** objetos para um único comando que contém várias instruções SQL, um **Recordset**por instrução SQL. A ordem na qual o **Recordset**s serão retornados segue a ordem na qual as instruções SQL são colocadas no texto do comando.  
  
 O Microsoft OLE DB Provider para SQL Server também retorna vários conjuntos de resultados para o ADO quando o comando contém uma cláusula COMPUTE. Por exemplo, um comando que contém a instrução SQL a seguir retornará os resultados em dois **conjunto de registros** objetos: um para o conjunto de linhas de (*ProductID*, *ProductName*, *UnitPrice*) e outro para o preço médio de todos os produtos na tabela.  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 Você pode usar o **Recordset.NextRecordset** método para enumerar os dois objetos.  
  
 Para obter mais informações, consulte [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md).
