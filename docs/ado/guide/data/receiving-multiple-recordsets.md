---
description: Receber vários conjuntos de registros
title: Recebendo vários conjuntos de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: abac183f348553f30bf0cf5ed91725ef421afb3e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979967"
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
