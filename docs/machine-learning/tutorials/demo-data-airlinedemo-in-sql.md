---
description: Dados de demonstração de chegadas de voos de companhias aéreas para tutoriais de Python e R do SQL Server
title: Dados de demonstração de voo de companhia aérea para tutoriais
Description: Crie um banco de dados que contenha um conjunto de dados de companhia aérea em R e Python. Esse conjunto de dados é usado em tutoriais de R e Python para os Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/22/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 3b19e905d68d53764a496ab5ee7745e3529484cf
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489896"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>Dados de demonstração de chegadas de voos de companhias aéreas para tutoriais de Python e R do SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Neste exercício, crie um banco de dados do SQL Server para armazenar dados importados de conjuntos internos de demonstração de linhas aéreas em R ou Python. As distribuições do R e Python fornecem dados equivalentes, que podem ser importados para um banco de dados do SQL Server usando o Management Studio.

Para concluir este exercício, você deve ter o [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) ou outra ferramenta que possa executar consultas T-SQL.

Os tutoriais e guias de início rápido que usam esse conjunto de dados incluem o seguinte:

+  [Criar um modelo Python usando revoscalepy](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>Criar o banco de dados

1. Inicie o SQL Server Management Studio, conecte-se a uma instância do mecanismo de banco de dados que tenha integração com R ou Python.  

2. No Pesquisador de Objetos, clique com o botão direito do mouse em **Bancos de Dados** e crie um novo banco de dados chamado **flightdata**.

3. Clique com o botão direito do mouse em **flightdata**, clique em **Tarefas** e clique em **Importar Arquivo Simples**.

4. Abra o arquivo AirlineDemoData.csv fornecido na distribuição do R ou do Python, dependendo da linguagem que você instalou.

   Para R, procure **AirlineDemoSmall.csv** em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL14. MSSQLSERVER \ R_SERVICES \library\RevoScaleR\SampleData
   
   Para Python, procure **AirlineDemoSmall.csv** em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\data\sample_data
  
Quando você seleciona o arquivo, os valores padrão do nome e esquema da tabela são preenchidos.

  ![Assistente de importação de arquivo simples mostrando padrões de demonstração de companhia aérea](media/import-airlinedemosmall.png)

Clique nas páginas restantes, aceitando os padrões, para importar os dados.


## <a name="query-the-data"></a>Consultar os dados

Como uma etapa de validação, execute uma consulta para confirmar se os dados foram carregados.

1. No Pesquisador de Objetos, em Bancos de Dados, clique com o botão direito do mouse no banco de dados **flightdata** e inicie uma nova consulta.

2. Execute algumas consultas simples:

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>Próximas etapas

Na lição a seguir, você criará um modelo de regressão linear com base nesses dados.

+ [Criar um modelo Python usando revoscalepy](use-python-revoscalepy-to-create-model.md)
