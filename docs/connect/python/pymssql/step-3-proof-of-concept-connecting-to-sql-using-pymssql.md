---
title: 'Etapa 3: Prova de conceito da conexão ao SQL usando pymssql | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27b56a20a0456bef04553c614432bde270d8e98d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935770"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>Etapa 3: prova de conceito conectando-se ao SQL usando pymssql
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

Este exemplo deve ser considerado apenas uma prova de conceito.  O código de exemplo é simplificado para fins de clareza e não necessariamente representa as práticas recomendadas recomendadas pela Microsoft.  
  
## <a name="step-1--connect"></a>Etapa 1: conectar-se  
  
A função [pymssql. Connect](https://pymssql.org/en/latest/ref/pymssql.html) é usada para se conectar ao banco de dados SQL.  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>Etapa 2: executar a consulta  
  
A função [cursor. Execute](https://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.execute) pode ser usada para recuperar um conjunto de resultados de uma consulta no banco de dados SQL. Essa função aceita, essencialmente, qualquer consulta e retorna um conjunto de resultados que pode ser iterado com o uso de [cursor. fetchone ()](https://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.fetchone).  
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute('SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC;')  
    row = cursor.fetchone()  
    while row:  
        print str(row[0]) + " " + str(row[1]) + " " + str(row[2])     
        row = cursor.fetchone()  
```  
  
## <a name="step-3--insert-a-row"></a>Etapa 3: inserir uma linha  
  
Neste exemplo, você verá como executar uma instrução [Insert](../../../t-sql/statements/insert-transact-sql.md) com segurança, passar parâmetros que protegem seu aplicativo do valor de [injeção de SQL](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) .    
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express', 'SQLEXPRESS', 0, 0, CURRENT_TIMESTAMP)")  
    row = cursor.fetchone()  
    while row:  
        print "Inserted Product ID : " +str(row[0])  
        row = cursor.fetchone()  
    conn.commit()
    conn.close()
```  
  
## <a name="step-4--rollback-a-transaction"></a>Etapa 4: reverter uma transação  
  
Este exemplo de código demonstra o uso de transações nas quais você:  
  
* Iniciar uma transação  
* Inserir uma linha de dados  
* Reverter a transação para desfazer a inserção  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("BEGIN TRANSACTION")  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, CURRENT_TIMESTAMP)")  
    conn.rollback()  
    conn.close()
```  
    
  ## <a name="next-steps"></a>Próximas etapas  
  
Para obter mais informações, consulte o [centro de desenvolvedores do Python](https://azure.microsoft.com/develop/python/).
