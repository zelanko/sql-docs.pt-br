---
title: "Lição 2: Importar dados para o SQL Server usando o PowerShell | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 3c5b5145-fa57-455a-b153-0400fc062dc0
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2f88b31305c9c648192d48d071972a787903136d
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="lesson-2-import-data-to-sql-server-using-powershell"></a>Lição 2: Importar dados para o SQL Server usando o PowerShell

Este artigo faz parte de um tutorial para desenvolvedores em SQL sobre como usar o R no SQL Server.

Nesta etapa, você vai executar um dos scripts baixados, para criar os objetos de banco de dados necessários para o passo a passo. O script também cria a maioria dos procedimentos armazenados que serão usados e carrega os dados de exemplo em uma tabela no banco de dados especificado.

## <a name="run-the-scripts-to-create-sql-objects"></a>Executar os scripts para criar objetos do SQL

Entre os arquivos baixados, você deverá ver um script do PowerShell que você pode executar para preparar o ambiente para o passo a passo. As ações executadas pelo script incluem:

- Instalando o SQL Native Client e utilitários de linha de comando do SQL, se ainda não estiverem instalados. Esses utilitários são necessários para o carregamento em massa dos dados no banco de dados com o **bcp**.

- Criando um banco de dados e uma tabela na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e inserindo em massa os dados na tabela.

- Criando vários procedimentos armazenados e funções do SQL.

### <a name="run-the-script"></a>Execute o script

1.  Abra um prompt de comando do PowerShell como administrador e execute o comando a seguir.
  
    ```ps
    .\RunSQL_SQL_Walkthrough.ps1
    ```
  
    Será solicitado que você insira as seguintes informações:
  
    - O nome ou endereço de uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em que o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] foi instalado
  
    - O nome de usuário e a senha de uma conta na instância. A conta deve ter permissões para criar bancos de dados, criar tabelas e procedimentos armazenados e carregar dados para tabelas. Se você não fornecer o nome de usuário e senha, a identidade do Windows é usada para entrar no SQL Server.
  
    - O caminho e o nome do arquivo de dados de exemplo que você acabou de baixar. Por exemplo:
  
        `C:\tempRSQL\nyctaxi1pct.csv`
  
2.  Como parte dessa etapa, todos os scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] também são modificados para substituir os espaços reservados pelos nomes do banco de dados e de usuário fornecidos como entradas de script.
  
    Reserve um minuto para examinar os procedimentos armazenados e as funções criadas pelo script.
  
    |**Nome do arquivo de script SQL**|**Função**|
    |-|-|
    |create-db-tb-upload-data.sql|Cria um banco de dados e duas tabelas:<br /><br />nyctaxi_sample: contém o conjunto de dados principal Táxi de Nova York. Um índice columnstore clusterizado é adicionado à tabela para melhorar o desempenho de armazenamento e consulta. A amostra de 1% do conjunto de dados Táxi de Nova York será inserida nesta tabela.<br /><br />nyc_taxi_models: usado para persistir o modelo treinado de análise avançada.|
    |fnCalculateDistance.sql|Cria uma função de valor escalar que calcula a distância direta entre os locais de embarque e desembarque de passageiros|
    |fnEngineerFeatures.sql|Cria uma função com valor de tabela que cria novos recursos de dados para treinamento do modelo|
    |PersistModel.sql|Cria um procedimento armazenado que pode ser chamado para salvar um modelo. O procedimento armazenado usa um modelo que foi serializado em um tipo de dados varbinary e grava-o na tabela especificada.|
    |PredictTipBatchMode.sql|Cria um procedimento armazenado que chama o modelo treinado para criar previsões usando o modelo. O procedimento armazenado aceita uma consulta como seu parâmetro de entrada e retorna uma coluna de valores numéricos que contêm as pontuações para as linhas de entrada.|
    |PredictTipSingleMode.sql|Cria um procedimento armazenado que chama o modelo treinado para criar previsões usando o modelo. Esse procedimento armazenado aceita uma nova observação como entrada, com valores de recursos individuais passados como parâmetros na linha, e retorna um valor que prevê o resultado da nova observação.|
  
    Você criará alguns procedimentos armazenados adicionais na última parte deste passo a passo:
  
    |**Nome do arquivo de script SQL**|**Função**|
    |------|------|
    |PlotHistogram.sql|Cria um procedimento armazenado para exploração de dados. Esse procedimento armazenado chama uma função do R para plotar o histograma de uma variável e retorna a plotagem como um objeto binário.|
    |PlotInOutputFiles.sql|Cria um procedimento armazenado para exploração de dados. Esse procedimento armazenado cria um gráfico usando uma função do R e salva a saída como um arquivo PDF local.|
    |TrainTipPredictionModel.sql|Cria um procedimento armazenado que treina um modelo de regressão logística chamando um pacote do R. O modelo prevê o valor da coluna tipped e é treinado usando uma seleção aleatória de 70% dos dados. A saída do procedimento armazenado é o modelo treinado, que é salvo na tabela nyc_taxi_models.|
  
3.  Faça logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e o logon especificado para verificar se você pode ver o banco de dados, as tabelas, as funções e os procedimentos armazenados criados.
  
    ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")
  
    > [!NOTE]
    > Se os objetos de banco de dados já existirem, não será possível criá-los novamente.
    >   
    > Se a tabela já existir, os dados serão acrescentados, não substituídos. Portanto, lembre-se de remover todos os objetos existentes antes de executar o script.

## <a name="next-lesson"></a>Próxima lição

[Lição 3: Explorar e visualizar os dados](../tutorials/sqldev-explore-and-visualize-the-data.md)

## <a name="previous-lesson"></a>Lição anterior

[Lição 1: Baixar os dados de exemplo](../tutorials/sqldev-download-the-sample-data.md)
