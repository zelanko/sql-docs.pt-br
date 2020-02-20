---
title: 'Etapa 3: Prova de conceito da conexão ao SQL usando pyodbc | Microsoft Docs'
ms.custom: ''
ms.date: 10/09/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e241d84ebc60acceafe09b1a9240711a72d2067
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "72798321"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>Etapa 3: Prova de conceito da conexão ao SQL usando pyodbc

Este exemplo deve ser considerado apenas uma prova de conceito.  O código de exemplo está simplificado para fins de clareza e não necessariamente representa as melhores práticas recomendadas pela Microsoft.  

**Execute o script de exemplo abaixo** Crie um arquivo chamado test.py e adicione cada snippet de código conforme prosseguir. 

```
> python test.py
```
  
## <a name="step-1--connect"></a>Etapa 1:  Conectar  
  
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
  
  
## <a name="step-2--execute-query"></a>Etapa 2:  Executar consulta  
  
A função cursor.execute pode ser usada para recuperar um conjunto de resultados de uma consulta no Banco de Dados SQL. Essencialmente, essa função aceita qualquer consulta e retorna um conjunto de resultados que pode ser iterado com o uso de cursor.fetchone()
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print(row[0])
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>Etapa 3:  Inserir uma linha  
  
Neste exemplo, você verá como executar uma instrução [INSERT](../../../t-sql/statements/insert-transact-sql.md) com segurança e passar parâmetros que protegem seu aplicativo contra o valor [injeção de SQL](../../../relational-databases/tables/primary-and-foreign-key-constraints.md).    
  
  
```python

#Sample insert query
cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP )") 
cnxn.commit()
row = cursor.fetchone()

while row: 
    print 'Inserted Product key is ' + str(row[0]) 
    row = cursor.fetchone()
```  

## <a name="azure-active-directory-aad-and-the-connection-string"></a>AAD (Azure Active Directory) e a cadeia de conexão

O pyODBC usa o driver ODBC da Microsoft para SQL Server.
Se a versão do driver ODBC for 17.1 ou posterior, você poderá usar o modo interativo do AAD do driver ODBC por meio de pyODBC.
Essa opção interativa do AAD funcionará se o Python e o pyODBC permitirem que o driver ODBC faça com que a caixa de diálogo apareça.
Esta opção só está disponível no sistema operacional Windows.

### <a name="example-connection-string-for-aad-interactive-authentication"></a>Exemplo de cadeia de conexão para a autenticação interativa do AAD

Aqui está um exemplo de cadeia de conexão ODBC que especifica a autenticação interativa do AAD:

- `server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

Para obter detalhes sobre as opções de autenticação do AAD do driver ODBC, confira o seguinte artigo:

- [Usando o Azure Active Directory com o Driver ODBC](../../odbc/using-azure-active-directory.md#new-andor-modified-dsn-and-connection-string-keywords)

## <a name="next-steps"></a>Próximas etapas
  
Para saber mais, confira o [Centro de Desenvolvedores do Python](https://azure.microsoft.com/develop/python/).
