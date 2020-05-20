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
author: rothja
ms.author: jroth
ms.openlocfilehash: 12aa80b918d11dad07119a26da3da8f27ef82cdb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759102"
---
# <a name="receiving-multiple-recordsets"></a>Receber vários conjuntos de registros
O [provedor de OLE DB da Microsoft para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) dá suporte ao retorno de vários objetos de **conjunto de registros** para um único comando que contém várias instruções SQL, um **conjunto de registros** por instrução SQL. A ordem na qual os s do **conjunto de registros**são retornados segue a ordem na qual as instruções SQL são colocadas no texto do comando.  
  
 O provedor de OLE DB da Microsoft para SQL Server também retorna vários conjuntos de resultados ao ADO quando o comando contém uma cláusula COMPUTE. Por exemplo, um comando que contém a seguinte instrução SQL retornará os resultados em dois objetos **Recordset** : um para o conjunto de linhas de (*ProductID*, *ProductName*, *PreçoUnitário*) e outro para o preço médio de todos os produtos na tabela.  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 Você pode usar o método **Recordset. NextRecordset** para enumerar os dois objetos.  
  
 Para obter mais informações, consulte [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md).
