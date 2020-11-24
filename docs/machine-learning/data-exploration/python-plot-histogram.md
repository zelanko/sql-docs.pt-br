---
title: Plotar um histograma para exploração de dados com o Python
titleSuffix: SQL machine learning
description: Saiba como criar um histograma para visualizar dados usando o Python.
author: dphansen
ms.author: davidph
ms.date: 07/14/2020
ms.topic: how-to
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=azuresqldb-current||=sqlallproducts-allversions'
ms.openlocfilehash: ee708d473e29cd36fe02e18e95eb71c0505dfdd7
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870128"
---
# <a name="plot-histograms-in-python"></a>Plotar histogramas no Python 
[!INCLUDE[SQL Server SQL DB SQL MI](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Este artigo descreve como plotar os dados usando o pacote [pandas'.hist()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.hist.html) do Python. Um Banco de Dados SQL é a origem usada para visualizar os intervalos de dados de histograma que têm valores consecutivos e não sobrepostos.

## <a name="prerequisites"></a>Pré-requisitos:

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
* [SQL Server para Windows](../../database-engine/install-windows/install-sql-server.md) ou [para Linux](../../linux/sql-server-linux-overview.md)
::: moniker-end

::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"
* [Banco de Dados SQL do Azure](/azure/sql-database/sql-database-get-started-portal)
::: moniker-end

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
* [Instância Gerenciada do SQL do Azure](/azure/azure-sql/managed-instance/instance-create-quickstart)

* [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) para restaurar o banco de dados de exemplo na Instância Gerenciada de SQL do Azure.
::: moniker-end

* Azure Data Studio. Para instalá-lo, confira [Azure Data Studio](../../azure-data-studio/what-is.md).

* [Restaure o banco de dados DW de exemplo](../../samples/adventureworks-install-configure.md) para obter os dados de exemplo usados neste artigo.

## <a name="verify-restored-database"></a>Confirmar o banco de dados restaurado

Confirme se o banco de dados restaurado existe consultando a tabela **Person.CountryRegion**:
```sql
USE AdventureWorksDW;
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

## <a name="plot-histogram"></a>Plotar um histograma

Os dados distribuídos exibidos no histograma baseiam-se em uma consulta SQL do AdventureWorksDW. O histograma visualiza os dados e a frequência dos valores de dados. Edite as variáveis de cadeia de conexão: 'server', 'database', 'username' e 'password' para se conectar ao Banco de Dados SQL.

Para criar um notebook:

1. No Azure Data Studio, selecione **Arquivo** e escolha **Novo Notebook**.
2. No notebook, selecione o kernel **Python3** e escolha **+code**.
3. Cole o código no notebook e selecione **Executar Tudo**.

```python
import pyodbc 
import pandas as plt
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'servername' 
database = 'AdventureWorksDW' 
username = 'yourusername' 
password = 'databasename'  
cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
sql = "SELECT DATEDIFF(year, c.BirthDate, GETDATE()) AS Age FROM [dbo].[FactInternetSales] s INNER JOIN dbo.DimCustomer c ON s.CustomerKey = c.CustomerKey"
df = pd.read_sql(sql, cnxn)
df.hist(bins=10)
```

A exibição mostra a distribuição etária de clientes na tabela FactInternetSales.

![Histograma do Pandas](./media/python-histogram.png)