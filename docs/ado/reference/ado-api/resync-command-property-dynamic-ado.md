---
title: Ressincronizar comando propriedade dinâmica (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Resync Command property [ADO]
ms.assetid: 4e2bb601-0fe8-4d61-b00e-38341d85a6bb
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8b3434c97e9548d5b37326a967f540f5f6d3a073
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="resync-command-property-dynamic-ado"></a>Ressincronizar comando propriedade dinâmica (ADO)
Especifica um comando fornecido pelo usuário de cadeia de caracteres que o [Resync](../../../ado/reference/ado-api/resync-method.md) problemas de método para atualizar os dados na tabela chamada no [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) propriedades dinâmicas.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor que é uma cadeia de caracteres de comando.  
  
## <a name="remarks"></a>Remarks  
 O [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto é o resultado de uma operação de junção executada em várias tabelas base. As linhas afetadas dependem de *AffectRecords* parâmetro do [Resync](../../../ado/reference/ado-api/resync-method.md) método. O padrão **Resync** o método é executado se o [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) e **comando Resync** propriedades não estão definidas.  
  
 A cadeia de caracteres de comando do **comando Resync** propriedade é um comando com parâmetros ou um procedimento armazenado que identifica exclusivamente a linha que está sendo atualizada e retorna uma única linha que contém o mesmo número e ordem das colunas, como a linha a ser atualizado. A cadeia de caracteres de comando contém um parâmetro para cada coluna de chave primária no **tabela exclusiva**; caso contrário, será retornado um erro de tempo de execução. Os parâmetros são preenchidos automaticamente com valores de chave primária da linha a ser atualizado.  
  
 Aqui estão dois exemplos com base em SQL:  
  
 1\) o **registros** é definido por um comando:  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 O **comando Resync** está definida como:  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 O **tabela exclusiva** é *pedidos* e sua chave primária, *OrderID*, é parametrizada. Subseleção fornece uma maneira simples de forma programática, certifique-se de que o mesmo número e ordem das colunas são retornadas como pelo comando original.  
  
 2\) o **registros** é definido por um procedimento armazenado:  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 O **Resync** método deve executar o procedimento armazenado a seguir:  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 O **comando Resync** está definida como:  
  
```  
"{call CustordersResync (?)}"  
```  
  
 Novamente, o **tabela exclusiva** é *pedidos* e sua chave primária, *OrderID*, é parametrizada.  
  
 **Ressincronizar comando** é uma propriedade dinâmica anexada ao **registros** objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção quando o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) está definida como **adUseClient**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
