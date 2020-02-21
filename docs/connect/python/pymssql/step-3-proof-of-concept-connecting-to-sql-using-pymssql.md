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
ms.openlocfilehash: c1dfce515eeadbdbaf1fd96e6dcf1a08cd536ab5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74200454"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>Etapa 3: Prova de conceito da conexão ao SQL usando pymssql
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

Este exemplo deve ser considerado apenas uma prova de conceito.  O código de exemplo está simplificado para fins de clareza e não necessariamente representa as melhores práticas recomendadas pela Microsoft.  
  
## <a name="step-1--connect"></a>Etapa 1:  Conectar  
  
A função [pymssql.connect](https://pypi.org/project/pymssql/) é usada para se conectar ao Banco de Dados SQL.  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>Etapa 2:  Executar consulta  
  
A função [cursor.execute](https://pypi.org/project/pymssql/) pode ser usada para recuperar um conjunto de resultados de uma consulta no Banco de Dados SQL. Essencialmente, essa função aceita qualquer consulta e retorna um conjunto de resultados que pode ser iterado com o uso de [cursor.fetchone()](https://pypi.org/project/pymssql/).  
  
  
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
  
## <a name="step-3--insert-a-row"></a>Etapa 3:  Inserir uma linha  
  
Neste exemplo, você verá como executar uma instrução [INSERT](../../../t-sql/statements/insert-transact-sql.md) com segurança e passar parâmetros que protegem seu aplicativo contra o valor [injeção de SQL](../../../relational-databases/tables/primary-and-foreign-key-constraints.md).    
  
  
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
  
## <a name="step-4--rollback-a-transaction"></a>Etapa 4:  Reverter uma transação  
  
Este exemplo de código demonstra o uso de transações nas quais você:  
  
* Inicia uma transação  
* Insere uma linha de dados  
* Reverte a transação para desfazer a inserção  
  
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
  
Para saber mais, confira o [Centro de Desenvolvedores do Python](https://azure.microsoft.com/develop/python/).
