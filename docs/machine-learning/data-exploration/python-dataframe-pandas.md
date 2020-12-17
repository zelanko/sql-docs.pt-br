---
title: Inserir dados de uma tabela SQL em um dataframe Pandas do Python
titleSuffix: SQL machine learning
description: Saiba como ler dados de uma tabela SQL e inseri-los em um dataframe Pandas usando o Python.
author: dphansen
ms.author: davidph
ms.date: 07/23/2020
ms.topic: how-to
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=azuresqldb-current'
ms.openlocfilehash: d3c051a2c72e911ddbf9d310929fe15628b8b5a2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471317"
---
# <a name="insert-data-from-a-sql-table-into-a-python-pandas-dataframe"></a>Inserir dados de uma tabela SQL em um dataframe Pandas do Python
[!INCLUDE[SQL Server SQL DB SQL MI](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Este artigo descreve como inserir dados SQL em um dataframe [Pandas](https://pandas.pydata.org/) usando o pacote [pyodbc](../../connect/python/pyodbc/python-sql-driver-pyodbc.md) no Python. As linhas e colunas de dados contidos no dataframe podem ser usadas para explorar ainda mais os dados.

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15"
* [SQL Server para Windows](../../database-engine/install-windows/install-sql-server.md) ou [para Linux](../../linux/sql-server-linux-overview.md)
::: moniker-end

::: moniker range="=azuresqldb-current"
* [Banco de Dados SQL do Azure](/azure/sql-database/sql-database-get-started-portal)
::: moniker-end

::: moniker range="=azuresqldb-mi-current"
* [Instância Gerenciada do SQL do Azure](/azure/azure-sql/managed-instance/instance-create-quickstart)

* [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) para restaurar o banco de dados de exemplo na Instância Gerenciada de SQL do Azure.
::: moniker-end

* Azure Data Studio. Para instalá-lo, confira [Azure Data Studio](../../azure-data-studio/what-is.md).

* [Restaure o banco de dados de exemplo](../../samples/adventureworks-install-configure.md) para obter os dados de exemplo usados neste artigo.

## <a name="verify-restored-database"></a>Confirmar o banco de dados restaurado

Confirme se o banco de dados restaurado existe consultando a tabela **Person.CountryRegion**:

```sql
USE AdventureWorks;
SELECT * FROM Person.CountryRegion;
```

## <a name="install-python-packages"></a>Instalar pacotes do Python

[Baixe e instale o Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md).

Instale os seguintes pacotes do Python:
  * pyodbc
  * pandas

  Para instalar esses pacotes:

  1. No notebook do Azure Data Studio, selecione **Gerenciar Pacotes**.
  2. No painel **Gerenciar Pacotes**, selecione a guia **Adicionar Novo**.
  3. Para cada pacote a seguir, insira o nome do pacote, clique em **Pesquisar** e em **Instalar**.

## <a name="insert-data"></a>Inserir dados

Use o script a seguir para selecionar dados da tabela Person.CountryRegion e inserir em um dataframe. Edite as variáveis de cadeia de conexão 'server', 'database', 'username' e 'password' para se conectar ao SQL.

Para criar um notebook:

1. No Azure Data Studio, selecione **Arquivo** e escolha **Novo Notebook**.
2. No notebook, selecione o kernel **Python3** e escolha **+code**.
3. Cole o código no notebook e selecione **Executar Tudo**.

```python
import pyodbc
import pandas as pd
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'servername' 
database = 'AdventureWorks' 
username = 'yourusername' 
password = 'databasename'  
cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
# select 26 rows from SQL table to insert in dataframe.
query = "SELECT [CountryRegionCode], [Name] FROM Person.CountryRegion;"
df = pd.read_sql(query, cnxn)
print(df.head(26))
```

**Saída**

O comando `print` no script anterior exibe as linhas de dados do dataframe `df` do `pandas`.

```text
CountryRegionCode                 Name
0                 AF          Afghanistan
1                 AL              Albania
2                 DZ              Algeria
3                 AS       American Samoa
4                 AD              Andorra
5                 AO               Angola
6                 AI             Anguilla
7                 AQ           Antarctica
8                 AG  Antigua and Barbuda
9                 AR            Argentina
10                AM              Armenia
11                AW                Aruba
12                AU            Australia
13                AT              Austria
14                AZ           Azerbaijan
15                BS         Bahamas, The
16                BH              Bahrain
17                BD           Bangladesh
18                BB             Barbados
19                BY              Belarus
20                BE              Belgium
21                BZ               Belize
22                BJ                Benin
23                BM              Bermuda
24                BT               Bhutan
25                BO              Bolivia
```

## <a name="next-steps"></a>Próximas etapas

+ [Inserir dataframe do Python no SQL](../data-exploration/python-dataframe-sql-server.md)