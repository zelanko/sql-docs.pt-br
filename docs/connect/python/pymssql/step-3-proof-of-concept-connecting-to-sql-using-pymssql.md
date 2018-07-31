---
title: 'Etapa 3: Prova de conceito da conexão ao SQL usando pymssql | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ea4fa2527fa39700647832bdd1a194389cb36e4
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982228"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>Etapa 3: Prova de conceito da conexão ao SQL usando pymssql
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

Este exemplo deve ser considerado uma prova de conceito apenas.  O código de exemplo é simplificado por motivos de clareza e não representa necessariamente as melhores práticas recomendadas pela Microsoft.  
  
## <a name="step-1--connect"></a>Etapa 1: conectar-se  
  
O [pymssql](http://pymssql.org/en/latest/ref/pymssql.html) função é usada para se conectar ao banco de dados SQL.  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>Etapa 2: Executar consulta  
  
O [cursor](http://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.execute) função pode ser usada para recuperar um conjunto de resultados de uma consulta no banco de dados SQL. Essencialmente, essa função aceita qualquer consulta e retorna um conjunto de resultados que pode ser iterado com o uso de [fetchone ()](http://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.fetchone).  
  
  
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
  
## <a name="step-3--insert-a-row"></a>Etapa 3: Inserir uma linha  
  
Neste exemplo, você verá como executar uma [inserir](../../../t-sql/statements/insert-transact-sql.md) instrução com segurança, passar parâmetros que protegem seu aplicativo contra [injeção de SQL](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) valor.    
  
  
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
  
## <a name="step-4--rollback-a-transaction"></a>Etapa 4: Reverter uma transação  
  
Este exemplo de código demonstra o uso de transações em que você:  
  
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
  
Para obter mais informações, consulte o [Central de desenvolvedores do Python](https://azure.microsoft.com/develop/python/).
