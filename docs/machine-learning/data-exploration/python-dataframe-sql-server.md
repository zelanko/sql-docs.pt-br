---
title: Inserir um dataframe do Python em uma tabela SQL
description: Como inserir dados de um dataframe em uma tabela SQL.
author: cawrites
ms.author: chadam
ms.date: 07/23/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=azuresqldb-current||=sqlallproducts-allversions'
ms.openlocfilehash: fe671dd00e844fe4789801a67a7ab4fc1c4be94b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242370"
---
# <a name="insert-python-dataframe-into-sql-table"></a>Inserir um dataframe do Python em uma tabela SQL
[!INCLUDE[sql-asdb-asdbmi-asa](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

Este artigo descreve como inserir um dataframe do [Pandas](https://pandas.pydata.org/) em um Banco de Dados SQL usando o pacote [pyodbc](../../connect/python/pyodbc/python-sql-driver-pyodbc.md) no Python.

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
* SQL Server. Para saber como instalá-lo, confira [SQL Server para Windows](../../database-engine/install-windows/install-sql-server.md) ou [para Linux](../../linux/sql-server-linux-overview.md).
::: moniker-end

::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"
* Banco de Dados SQL do Azure. Para saber como se inscrever, confira [Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
::: moniker-end

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
* Instância Gerenciada de SQL do Azure. Para saber como se inscrever, confira [Instância Gerenciada de SQL do Azure](https://docs.microsoft.com/azure/azure-sql/managed-instance/instance-create-quickstart).

* [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) para restaurar o banco de dados de exemplo na Instância Gerenciada de SQL do Azure.
::: moniker-end

* Azure Data Studio. Para saber como instalá-lo, confira [Azure Data Studio](../../azure-data-studio/what-is.md).

* [Restaure o banco de dados de exemplo](../../samples/adventureworks-install-configure.md) para obter os dados de exemplo usados neste artigo.

## <a name="verify-restored-database"></a>Confirmar o banco de dados restaurado

Confirme se o banco de dados restaurado existe consultando a tabela **HumanResources.Department**:

```sql
USE AdventureWorks;
SELECT * FROM HumanResources.Department;
```

## <a name="install-python-packages"></a>Instalar pacotes do Python

* [Baixar e instalar o Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md)

Instale os seguintes pacotes do Python:
  * pyodbc
  * pandas

  Para instalar esses pacotes:

  1. No notebook do Azure Data Studio, selecione **Gerenciar Pacotes**.
  2. No painel **Gerenciar Pacotes**, selecione a guia **Adicionar Novo**.
  3. Para cada pacote a seguir, insira o nome do pacote, clique em **Pesquisar**e em **Instalar**.

## <a name="connect-to-sql-server-using-azure-data-studio"></a>Conectar ao SQL Server usando o Azure Data Studio

[Conectar-se usando o Azure Data Studio](../../azure-data-studio/quickstart-sql-server.md).

1. Conecte-se ao banco de dados Adventureworks para criar a tabela HumanResources.DepartmentTest. A tabela SQL será usada para a inserção do dataframe.

```sql
CREATE TABLE [HumanResources].[DepartmentTest](
[DepartmentID] [smallint] NOT NULL,
[Name] [dbo].[Name] NOT NULL,
[GroupName] [dbo].[Name] NOT NULL
)
GO
```

## <a name="create-csv-file"></a>Criar um arquivo CSV

Copie o texto e salve o arquivo como department.csv no dataframe.

```text
DepartmentID,Name,GroupName,
1,Engineering,Research and Development,
2,Tool Design,Research and Development,
3,Sales,Sales and Marketing,
4,Marketing,Sales and Marketing,
5,Purchasing,Inventory Management,
6,Research and Development,Research and Development,
7,Production,Manufacturing,
8,Production Control,Manufacturing,
9,Human Resources,Executive General and Administration,
10,Finance,Executive General and Administration,
11,Information Services,Executive General and Administration,
12,Document Control,Quality Assurance,
13,Quality Assurance,Quality Assurance,
14,Facilities and Maintenance,Executive General and Administration,
15,Shipping and Receiving,Inventory Management,
16,Executive,Executive General and Administration
```

## <a name="connect-to-sql-using-python"></a>Conectar-se ao SQL usando o Python

1. Edite as variáveis de cadeia de conexão 'server', 'database', 'username' e 'password' para se conectar ao Banco de Dados SQL.

2. Edite o caminho para o arquivo CSV.

## <a name="load-dataframe-from-csv-file"></a>Carregar o dataframe por meio do arquivo CSV

Use o pacote `pandas` do Python para criar um dataframe e carregar o arquivo CSV. Conecte-se ao SQL para carregar o dataframe na nova tabela SQL, HumanResources.DepartmentTest.

Para criar um notebook:

1. No Azure Data Studio, selecione **Arquivo** e escolha **Novo Notebook**.
2. No notebook, selecione o kernel **Python3** e escolha **+code**.
3. Cole o código no notebook e selecione **Executar Tudo**.

 ```Python
import pyodbc
import pandas as pd
# insert data from csv file into dataframe.
# working directory for csv file: type "pwd" in Azure Data Studio or Linux
# working directory in Windows c:\users\username
df = pd.read_csv("c:\\user\\username\department.csv")
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'yourservername' 
database = 'AdventureWorks' 
username = 'username' 
password = 'yourpassword' 
cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
# Insert Dataframe into SQL Server:
for index, row in df.iterrows():
     cursor.execute("INSERT INTO HumanResources.DepartmentTest (DepartmentID,Name,GroupName) values(?,?,?)", row.DepartmentID, row.Name, row.GroupName)
cnxn.commit()
cursor.close()
```

## <a name="confirm-row-count-in-sql"></a>Confirmar a contagem de linhas no SQL

Execute a instrução SQL para confirmar se a tabela foi carregada com êxito com os dados do dataframe.

```sql
SELECT count(*) from HumanResources.DepartmentTest;
```

Resultados

```bash
(No column name)
16
```

## <a name="next-steps"></a>Próximas etapas

+ [Plotar um histograma para exploração de dados com o Python](../data-exploration/python-plot-histogram.md)
