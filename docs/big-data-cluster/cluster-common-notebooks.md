---
title: Cenário comum ao trabalhar com BDCs (Clusters de Big Data) com Jupyter notebooks e Azure Data Studio
titleSuffix: SQL Server Big Data Clusters
description: Cenário comum ao trabalhar com BDC com Jupyter notebooks e Azure Data Studio no cluster de Big Data do SQL Server 2019.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 99e62be597e4ce08d38db199116f1bd4d5ab33f6
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378340"
---
# <a name="common-notebooks-for-sql-server-big-data-clusters"></a>Notebooks comuns para Clusters de Big Data do SQL Server

Este artigo lista notebooks para Clusters de Big Data do SQL Server. Esses notebooks executáveis (.ipynb) foram criados para o SQL Server 2019 para auxiliar na exibição de cenários comuns envolvendo Clusters de Big Data.

Cada notebook foi criado para conferir suas próprias dependências. Uma opção **Executar todas as células** vai ser concluída com êxito ou gerar uma exceção com uma *dica* de hiperlink para um outro notebook a fim de resolver a dependência ausente. Siga o hiperlink de dica para o notebook subsequente, pressione **Executar todas as células** e, tendo êxito, volte para o notebook original e pressione **Executar todas as células** .

Depois que todas as dependências forem instaladas mas **Executar todas as células** falhar, cada notebook analisará os resultados e, sempre que possível, produzirá um hiperlink de dica para outro notebook a fim de ajudar a resolver o problema.

## <a name="gathering-logs-from-big-data-cluster-bdc"></a>Coletar logs do BDC (cluster de Big Data)

Os notebooks nessa seção são usados como pré-requisitos de outros notebooks, como logon e logoff de um cluster.

|Name |Descrição |
|---|---|
|SOP005 – az login|Use a interface de linha de comando az para fazer logon no Azure. |
|SOP006 – az logout|Use a interface de linha de comando az para fazer logoff do Azure.|
|SOP007 – Informações sobre a versão (azdata, bdc, kubernetes)|Defina as funções auxiliares usadas no notebook sobre informações de controle de versão.|
|SOP011 – Definir contexto de configuração do Kubernetes|Definir a configuração do Kubernetes a ser usada. |
|SOP028 – azdata login|Use a interface de linha de comando azdata para fazer logon no Cluster de Big Data. |
|SOP033 – logoff do azdata|Use a interface de linha de comando do azdata para fazer logoff de um Cluster de Big Data. |
|SOP034 – Aguardar que o BDC fique íntegro|Realiza um bloqueio até que o cluster de Big Data fique íntegro ou que o tempo limite especificado expire. O parâmetro min_pod_count indica que a verificação de integridade não será aprovada até que pelo menos esse número de pods exista no cluster. Se os pods existentes além desse limite não estiverem íntegros, o cluster não estará íntegro.|
|OPR001 – Criar app-deploy|Use esse notebook para criar um aplicativo no cluster de Big Data. |
|OPR002 – Executar app-deploy|Use esse notebook para executar um aplicativo no cluster de Big Data. |
|OPR003 – Criar cronjob|Use esse notebook para criar um cronjob no cluster de Big Data. |
|OPR004 – Suspender cronjob|Use esse notebook para suspender um cronjob no cluster de Big Data. |
|OPR005 – Retomar cronjob|Use esse notebook para retomar um cronjob no cluster de Big Data. |
|OPR006 – Excluir cronjob|Use esse notebook para excluir um cronjob no cluster de Big Data. |
|OPR007 – Excluir app-deploy|Use esse notebook para excluir um aplicativo no cluster de Big Data. |
|OPR100 – Implantar e agendar notebooks|Use esse notebook para implantar uma lista de notebooks em um pod App-Deploy, executar o App-Deploy segundo uma agenda usando um CronJob do Kubernetes e instalar um painel do Grafana para ver os resultados.|
|OPR600 – Monitorar a infraestrutura (Kubernetes)|Use esse notebook para monitorar a infraestrutura.|
|OPR700 – Criar um painel do Grafana para aplicativos App-Deploy|Use esse notebook para criar um painel no Grafana a fim de monitorar os resultados de App-Deploy e gerar alertas se um canário ou aplicativo começar a falhar.|
|OPR900 – Solucionar problemas de execução de app-deploy|Use esse notebook para executar o script app-deploy diretamente no contêiner (usando kubectl exec). Isso pode fornecer mais informações de depuração para solução de problemas, especialmente aqueles relacionados ao estágio de inicialização do script.|
|OPR901 – Solucionar problemas de cronjob|Use esse notebook para executar o script cronjob diretamente no contêiner (usando kubectl exec). Isso pode fornecer mais informações de depuração para solução de problemas.|


## <a name="analyze-logs-from-big-data-clusters-bdc"></a>Analisar logs de BDCs (Clusters de Big Data)

Um conjunto de notebooks de exemplo que demonstram os cenários de Cluster de Big Data do SQL Server.

|Name |Descrição |
|---|---|
|SAM001a – Pool de armazenamento de consulta do Pool Mestre do SQL Server (1 de 3) – Carregar dados de exemplo|Neste tutorial de três partes, carregue dados no pool de armazenamento (HDFS) usando o azdata, converta-os em Parquet (usando o Spark) e, na terceira parte, consulte os dados usando o Pool Mestre (SQL Server). |
|SAM001b – Pool de armazenamento de consulta do Pool Mestre do SQL Server (2 de 3) – Converter dados em Parquet|Nesta segunda parte de um tutorial de três partes, use o Spark para converter um arquivo .csv em um arquivo Parquet.|
|SAM001c – Pool de armazenamento de consulta do Pool Mestre do SQL Server (3 de 3) – Consultar HDFS do SQL Server|Nesta terceira parte do tutorial do pool de armazenamento, você aprenderá a criar uma tabela externa apontando para dados do HDFS em um cluster de Big Data e a uni-los com os dados de valor alto na instância mestra.|
|SAM002 – Pool de Armazenamento (2 de 2) – Consultar HDFS|Nessa segunda parte do tutorial do pool de armazenamento, você aprenderá a criar uma tabela externa apontando para dados do HDFS em um cluster de Big Data e unirá esses dados com outros de alto valor na instância mestra|
|SAM003 – Exemplo de Pool de Dados|Nesse tutorial, você aprenderá a criar uma origem do pool de dados e uma tabela externa no pool de dados, depois inserir dados em tabelas do pool de dados e carregar dados de uma tabela do pool de dados para outra. Una dados na tabela de pool de dados com outras tabelas de pool de dados, realizando também o truncamento de tabelas e a limpeza. |
|SAM004 – Virtualizar dados do MongoDB|Para consultar os dados de uma fonte de dados externa do MongoDB, você precisa criar tabelas externas para referenciar os dados externos. Esta seção fornece código de exemplo para criar essas tabelas externas.|
|SAM005 – Virtualizar dados do Oracle|Para consultar os dados de uma fonte de dados externa do Oracle, você precisa criar tabelas externas para referenciar os dados externos. Esta seção fornece código de exemplo para criar essas tabelas externas.|
|SAM006 – Virtualizar dados do SQL Server|Para consultar dados virtualmente de outra fonte de dados do SQL Server, você deve criar tabelas externas para referenciar esses dados externos. Esta seção fornece código de exemplo para criar essas tabelas externas.|
|SAM007 – Virtualizar dados do Teradata|Para consultar os dados de uma fonte de dados externa do Teradata, você precisa criar tabelas externas para referenciar os dados externos. Esta seção fornece código de exemplo para criar essas tabelas externas.|
|SAM008 – Spark usando azdata|Comandos azdata e kubectl para trabalhar com sessões do Spark.|
|SAM009 – HDFS usando azdata|Comandos azdata e kubectl para trabalhar com o HDFS.|
|SAM010 – Aplicativo usando azdata|Comandos azdata e kubectl para trabalhar com o App-Deploy. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
