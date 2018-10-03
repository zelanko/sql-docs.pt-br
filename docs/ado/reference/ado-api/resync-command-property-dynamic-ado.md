---
title: Ressincronizar propriedade dinâmica do comando (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5567bf3cc460aac6abfc2979a14e124bfd9d4cac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789284"
---
# <a name="resync-command-property-dynamic-ado"></a>Ressincronizar propriedade dinâmica do comando (ADO)
Especifica um comando fornecido pelo usuário de cadeia de caracteres que o [ressincronizar](../../../ado/reference/ado-api/resync-method.md) problemas para atualizar os dados na tabela chamada no método da [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) propriedade dinâmica.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor que é uma cadeia de caracteres de comando.  
  
## <a name="remarks"></a>Comentários  
 O [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto é o resultado de uma operação de junção executado em várias tabelas base. As linhas afetadas dependem de *AffectRecords* parâmetro do [ressincronizar](../../../ado/reference/ado-api/resync-method.md) método. O padrão **ressincronizar** método é executado se o [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) e **comando ressincronizar** propriedades não estão definidas.  
  
 A cadeia de caracteres de comando de **comando ressincronizar** propriedade é um comando com parâmetros ou um procedimento armazenado que identifica exclusivamente a linha que está sendo atualizada e retorna uma única linha que contém o mesmo número e a ordem das colunas, como a linha seja atualizado. A cadeia de caracteres de comando contém um parâmetro para cada coluna de chave primária a **tabela exclusiva**; caso contrário, será retornado um erro de tempo de execução. Os parâmetros são preenchidos automaticamente com valores de chave primária da linha a ser atualizado.  
  
 Aqui estão dois exemplos com base em SQL:  
  
 1\) as **Recordset** é definido por um comando:  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 O **comando ressincronizar** estiver definida como:  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 O **tabela exclusiva** é *pedidos* e sua chave primária, *OrderID*, com parâmetros. A Subseleção fornece uma maneira simples de forma programática, certifique-se de que o mesmo número e a ordem das colunas são retornadas como pelo comando original.  
  
 2\) as **Recordset** é definido por um procedimento armazenado:  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 O **ressincronizar** método deve executar o procedimento armazenado a seguir:  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 O **comando ressincronizar** estiver definida como:  
  
```  
"{call CustordersResync (?)}"  
```  
  
 Mais uma vez, o **tabela exclusiva** é *pedidos* e sua chave primária, *OrderID*, com parâmetros.  
  
 **Ressincronização de comando** uma propriedade dinâmica que é acrescentada à **conjunto de registros** objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção quando o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) estiver definida como **adUseClient**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
