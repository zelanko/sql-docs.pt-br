---
title: Conjunto de dados de demonstração de voo de companhia aérea para tutoriais do SQL Server Python e R - aprendizagem de máquina do SQL Server
Description: Crie um banco de dados que contém o conjunto de dados de companhia aérea do R e Python. Esse conjunto de dados é usado em exercícios que mostra como encapsular a linguagem R ou o código do Python em um procedimento armazenado do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 69f95876a880684ee09b83ad32341a781bc4f5cf
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510183"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>Dados de demonstração de chegada de voo de companhia aérea para tutoriais do SQL Server Python e R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste exercício, crie um banco de dados do SQL Server para armazenar os dados importados de R ou Python internos Airline demo conjuntos de dados. Distribuições do R e Python fornecem dados equivalentes, que você pode importar um banco de dados do SQL Server usando o Management Studio.

Para concluir este exercício, você deve ter [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) ou outra ferramenta que pode executar consultas do T-SQL.

Tutoriais e guias de início rápido usando esse conjunto de dados incluem o seguinte:

+  [Criar um modelo de Python usando revoscalepy](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>Criar o banco de dados

1. Inicie o SQL Server Management Studio, conecte-se para uma instância do mecanismo de banco de dados que tem integração de R ou Python.  

2. No Pesquisador de objetos, clique com botão direito **bancos de dados** e crie um novo banco de dados chamado **flightdata**.

3. Clique com botão direito **flightdata**, clique em **tarefas**, clique em **importar arquivo simples**.

4. Abra o arquivo AirlineDemoData.csv fornecido na distribuição de R ou Python, dependendo do idioma que você instalou.

   Para R, procure **AirlineDemoSmall.csv** em C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData
   
   Para o Python, procure **AirlineDemoSmall.csv** em C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Lib\site packages\revoscalepy\data\sample_data
  
Quando você seleciona o arquivo, valores padrão são preenchidos para o esquema e o nome da tabela.

  ![Assistente Importar arquivo simples que mostra os padrões de demonstração de companhia aérea](media/import-airlinedemosmall.png)

Clique nas páginas restantes, aceitando os padrões, para importar os dados.


## <a name="query-the-data"></a>Consultar os dados

Como uma etapa de validação, execute uma consulta para confirmar se que os dados foram carregados.

1. No Pesquisador de objetos em bancos de dados, clique com botão direito do **flightdata** de banco de dados e iniciar uma nova consulta.

2. Execute algumas consultas simples:

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>Próximas etapas

Na próxima lição, você criará um modelo de regressão linear com base nesses dados.

+ [Criar um modelo de Python usando revoscalepy](use-python-revoscalepy-to-create-model.md)
