---
description: Ressincronizar propriedade dinâmica do comando (ADO)
title: Propriedade de comando de ressincronização-dinâmica (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Resync Command property [ADO]
ms.assetid: 4e2bb601-0fe8-4d61-b00e-38341d85a6bb
author: rothja
ms.author: jroth
ms.openlocfilehash: a7a350540d94ea0379f7829fa004d98ce691f1e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442298"
---
# <a name="resync-command-property-dynamic-ado"></a>Ressincronizar propriedade dinâmica do comando (ADO)
Especifica uma cadeia de caracteres de comando fornecida pelo usuário que o método de [ressincronização](../../../ado/reference/ado-api/resync-method.md) emite para atualizar os dados na tabela nomeada na propriedade dinâmica da [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **cadeia** de caracteres que é uma cadeia de caracteres de comando.  
  
## <a name="remarks"></a>Comentários  
 O objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) é o resultado de uma operação JOIN executada em várias tabelas base. As linhas afetadas dependem do parâmetro *AffectRecords* do método [Ressync](../../../ado/reference/ado-api/resync-method.md) . O método de **ressincronização** padrão é executado se a [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) e as propriedades de **comando de ressincronização** não estiverem definidas.  
  
 A cadeia de caracteres de comando da propriedade de **comando Ressync** é um comando com parâmetros ou um procedimento armazenado que identifica exclusivamente a linha que está sendo atualizada e retorna uma única linha contendo o mesmo número e a mesma ordem das colunas que a linha a ser atualizada. A cadeia de caracteres de comando contém um parâmetro para cada coluna de chave primária na **tabela exclusiva**; caso contrário, um erro de tempo de execução será retornado. Os parâmetros são preenchidos automaticamente com valores de chave primária da linha a ser atualizada.  
  
 Aqui estão dois exemplos com base no SQL:  
  
 1 \) o **conjunto de registros** é definido por um comando:  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 A propriedade de **comando Ressync** é definida como:  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 A **tabela exclusiva** é *pedidos* e sua chave primária, *OrderID*, é parametrizada. A Subseleção fornece uma maneira simples de garantir programaticamente que o mesmo número e a ordem das colunas sejam retornados como pelo comando original.  
  
 2 \) o **conjunto de registros** é definido por um procedimento armazenado:  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 O método de **ressincronização** deve executar o seguinte procedimento armazenado:  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 A propriedade de **comando Ressync** é definida como:  
  
```  
"{call CustordersResync (?)}"  
```  
  
 Mais uma vez, a **tabela exclusiva** é *pedidos* e sua chave primária, *OrderID*, é parametrizada.  
  
 O **comando Ressync** é uma propriedade dinâmica acrescentada à coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) do objeto **Recordset** quando a propriedade [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) é definida como **adUseClient**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
