---
title: Coletar e analisar logs com Jupyter notebooks e Azure Data Studio
titleSuffix: SQL Server Big Data Clusters
description: Registrar cluster em log com Jupyter notebooks e Azure Data Studio no cluster de Big Data do SQL Server 2019.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5efb20db2b0f5e3d3509715a8711ce32414fa9ee
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378336"
---
# <a name="gathering-and-analyzing-logs-in-the-cluster-with-notebooks"></a>Coletar e analisar logs no cluster com notebooks

Esta página é um índice de notebooks para Clusters de Big Data do SQL Server. Esses notebooks executáveis (.ipynb) foram criados para o SQL Server 2019 para auxiliar no registro de Clusters de Big Data.

Cada notebook foi criado para conferir suas próprias dependências. Um **Executar todas as células** vai ser concluído com êxito ou gerar uma exceção com uma dica de hiperlink para um outro notebook resolver a dependência ausente. Siga o hiperlink de dica para o notebook subsequente, pressione **Executar todas as células** e, tendo êxito, volte para o notebook original e pressione **Executar todas as células** .

Depois que todas as dependências forem instaladas mas **Executar todas as células** falhar, cada notebook analisará os resultados e, sempre que possível, produzirá um hiperlink de dica para outro notebook a fim de ajudar a resolver o problema.

## <a name="gathering-logs-from-big-data-cluster-bdc"></a>Coletar logs do BDC (cluster de Big Data)

Essa seção contém um conjunto de notebooks úteis para obter logs de um BDC (cluster de Big Data) do SQL Server.

| Name | Descrição |
|--|--|
| TSG001 – Executar azdata copy-logs | Use a interface de linha de comando azdata para copiar dados para clusters BDC. |
| TSG061 – Obter a parte final de todos os logs de contêiner para os pods no namespace do BDC | Obtenha todos os logs de contêiner para pods do cluster BDC no namespace. |
| TSG062 – Obter a parte final de todos os logs de contêiner anteriores para os pods no namespace do BDC | Obtenha todos os logs de contêiner anteriores para pods do cluster BDC no namespace. |
| TSG083 – Executar kubectl cluster-info dump | Use a interface de linha de comando do kubetl para despejar informações relacionadas ao cluster BDC. |
| TSG084 – Erro interno do processador de consultas | Use a consulta DMV para obter mais informações sobre o erro interno do processador de consultas. |
| TSG091 – Obter os logs da CLI do azdata | Obtenha os logs do azdata do computador local. |



## <a name="analyse-logs-from-big-data-clusters-bdc"></a>Analisar logs de BDCs (Clusters de Big Data)

Um conjunto de notebooks para coletar e analisar logs de um Cluster de Big Data do SQL Server.  O processo de análise sugerirá notebooks subsequentes a serem executados para um problema conhecido encontrado nos logs.

|Name|Descrição |
|---|---|
|TSG030 – Arquivos de log de erros do SQL Server|Obtenha os arquivos de log de erros do SQL Server, analise as entradas de log e sugira guias de solução de problemas adicionais relevantes. |
|TSG031 – Logs do PolyBase do SQL Server|Obtenha os logs do PolyBase do SQL Server, analise as entradas de log e sugira guias de solução de problemas adicionais relevantes.|
|TSG034 – Logs do Livy|Obtenha os logs do Livy, analise as entradas de log e sugira guias de solução de problemas adicionais relevantes.|
|TSG035 – Logs do Histórico do Spark|Obtenha os logs de histórico do Spark, analise as entradas de log e sugira guias de solução de problemas adicionais relevantes.|
|TSG036 – Logs do controlador|Obtenha os logs do controlador das últimas "N" horas, analise as entradas de log e sugira guias de solução de problemas adicionais relevantes.|
|TSG046 – Logs de gateway do Knox|O Knox apresenta um erro 500 ao cliente e remove os detalhes (a pilha) que apontam para a causa do problema subjacente. Portanto, use este notebook para obter os logs do Knox do cluster. Obtenha os logs de gateway do Knox, analise as entradas de log e sugira guias de solução de problemas adicionais relevantes.|
|TSG073 – Logs do InfluxDB|Obtenha os logs do InfluxDB, analise as entradas de log e sugira guias de solução de problemas adicionais relevantes.|
|TSG076 – Logs da Pesquisa Elástica|Obtenha os logs da Pesquisa Elástica, analise as entradas de log e sugira guias de solução de problemas adicionais relevantes.|
|TSG077 – logs do Kibana|Obter os logs do Kibana, analisar as entradas de log e sugerir guias de solução de problemas adicionais relevantes.|
|TSG088 – Logs de datanode do Hadoop|Obtenha os logs de datanode do Hadoop, analise as entradas de log e sugira guias de solução de problemas adicionais relevantes.|
|TSG090 – Logs do nodemanager do YARN|Obtenha os logs de nodemanager do Yarn, analise as entradas de log e sugira guias de solução de problemas adicionais relevantes.|
|TSG092 – Parte final do log do Supervisord para todos os contêineres no BDC|Obtenha a parte final do log do Supervisord para todos os contêineres no BDC, analise as entradas de log e sugira guias de solução de problemas adicionais relevantes.|
|TSG093 – Parte final do log do Agente para todos os contêineres no BDC|Obtenha a parte final do log do Agente para todos os contêineres no BDC, analise as entradas de log e sugira guias de solução de problemas adicionais relevantes.|
|TSG094 – Logs do Grafana|Obtenha os logs do Grafana, analise as entradas de log e sugira guias de solução de problemas adicionais relevantes.|
|TSG095 – Logs de namenode do Hadoop|Obtenha os logs de datanode do namenode, analise as entradas de log e sugira guias de solução de problemas adicionais relevantes.|
|TSG096 – Logs do Zookeeper|Obtenha os logs do ZooKeeper, analise as entradas de log e sugira guias de solução de problemas adicionais relevantes.|

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
