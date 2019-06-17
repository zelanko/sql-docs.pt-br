---
title: 'Etapa 3: Prova de conceito da conexão ao SQL usando pyodbc | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e8f4c34c1b6b945c28193a549a06546ec952a5d9
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66780364"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>Etapa 3: Prova de conceito da conexão ao SQL usando pyodbc

Este exemplo deve ser considerado uma prova de conceito apenas.  O código de exemplo é simplificado por motivos de clareza e não representa necessariamente as melhores práticas recomendadas pela Microsoft.  

**Execute o script de exemplo abaixo** crie um arquivo chamado test.py e adicione cada trecho de código conforme você avança. 

```
> python test.py
```
  
## <a name="step-1--connect"></a>Etapa 1: conectar-se  
  
```python

import pyodbc 
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'tcp:myserver.database.windows.net' 
database = 'mydb' 
username = 'myusername' 
password = 'mypassword' 
cnxn = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()

```  
  
  
## <a name="step-2--execute-query"></a>Etapa 2: Executar consulta  
  
O cursor.executefunction pode ser usado para recuperar um conjunto de resultados de uma consulta no banco de dados SQL. Essencialmente, essa função aceita qualquer consulta e retorna um conjunto de resultados que pode ser iterado com o uso de fetchone)
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print row[0] 
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>Etapa 3: Inserir uma linha  
  
Neste exemplo, você verá como executar uma [inserir](../../../t-sql/statements/insert-transact-sql.md) instrução com segurança, passar parâmetros que protegem seu aplicativo contra [injeção de SQL](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) valor.    
  
  
```python

#Sample insert query
cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP )") 
row = cursor.fetchone()

while row: 
    print 'Inserted Product key is ' + str(row[0]) 
    row = cursor.fetchone()
```  
  `      
  ## <a name="next-steps"></a>Próximas etapas  
  
Para obter mais informações, consulte o [Central de desenvolvedores do Python](https://azure.microsoft.com/develop/python/).
