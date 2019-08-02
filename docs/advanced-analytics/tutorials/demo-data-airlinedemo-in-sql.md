---
title: Conjunto de dados de demonstração de vôo aérea para SQL Server tutoriais de Python e R
Description: Crie um banco de dados que contenha o DataSet de companhia aérea de R e Python. Esse conjunto de DataSet é usado em exercícios que mostram como encapsular a linguagem R ou o código Python em um procedimento armazenado SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b7f28dd4b3e7e6990e037dbd9afe164d8d0e4bec
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714810"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>Dados de demonstração da chegada da voo aérea para SQL Server tutoriais de Python e R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste exercício, crie um banco de dados de SQL Server para armazenar dados importados de conjuntos internos do R ou Python demonstração de linhas aéreas. As distribuições do R e do Python fornecem dados equivalentes, que podem ser importados para um banco de dado SQL Server usando Management Studio.

Para concluir este exercício, você deve ter [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) ou outra ferramenta que possa executar consultas T-SQL.

Os tutoriais e os guias de início rápido usando esse conjunto de dados incluem o seguinte:

+  [Criar um modelo Python usando o revoscalepy](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>Criar o banco de dados

1. Inicie o SQL Server Management Studio, conecte-se a uma instância do mecanismo de banco de dados que tenha integração de R ou Python.  

2. No Pesquisador de objetos, clique com o botão direito do mouse em **bancos** de dados e crie um novo, chamado **flightdata**.

3. Clique com o botão direito do mouse em **flightdata**, clique em **tarefas**e em **Importar arquivo simples**.

4. Abra o arquivo AirlineDemoData. csv fornecido na distribuição do R ou do Python, dependendo de qual idioma você instalou.

   Para R, procure **AirlineDemoSmall. csv** em C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData
   
   Para Python, procure **AirlineDemoSmall. csv** em C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\data\sample_data
  
Quando você seleciona o arquivo, os valores padrão são preenchidos para o nome e o esquema da tabela.

  ![Assistente de importação de arquivo simples mostrando padrões de demonstração da companhia aérea](media/import-airlinedemosmall.png)

Clique nas páginas restantes, aceitando os padrões, para importar os dados.


## <a name="query-the-data"></a>Consultar os dados

Como uma etapa de validação, execute uma consulta para confirmar se os dados foram carregados.

1. No Pesquisador de objetos, em bancos de dados, clique com o botão direito do mouse em **flightdata** e inicie uma nova consulta.

2. Execute algumas consultas simples:

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>Próximas etapas

Na lição a seguir, você criará um modelo de regressão linear com base nesses dados.

+ [Criar um modelo Python usando o revoscalepy](use-python-revoscalepy-to-create-model.md)
