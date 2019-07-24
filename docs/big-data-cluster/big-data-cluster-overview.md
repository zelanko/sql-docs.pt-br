---
title: O que são clusters Big Data?
titleSuffix: SQL Server big data clusters
description: Saiba mais sobre os clusters SQL Server 2019 Big Data (versão prévia) que são executados no kubernetes e fornecem opções de expansão para dados relacionais e de HDFS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0beb4ea57ba6c2591e5b2c06a7775fc2d7e8b26c
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419501"
---
# <a name="what-are-sql-server-big-data-clusters"></a>O que são os clusters de Big Data do SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

A [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]partir do, SQL Server clusters Big data permitem que você implante clusters escalonáveis de contêineres SQL Server, Spark e HDFS em execução no kubernetes. Esses componentes são executados lado a lado para permitir que você leia, grave e processe Big Data do Transact-SQL ou do Spark, permitindo que você combine e analise facilmente seus dados relacionais de alto valor com Big Data de alto volume.

Para obter mais informações sobre os novos recursos e problemas conhecidos para a versão mais recente, consulte as [notas de versão](release-notes-big-data-cluster.md).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>Cenários

SQL Server clusters Big Data fornecem flexibilidade na maneira como você interage com seu Big Data. Você pode consultar fontes de dados externas, armazenar Big Data no HDFS gerenciado pelo SQL Server ou consultar dados de várias fontes de dados externas por meio do cluster. Você pode usar os dados para ia, Machine Learning e outras tarefas de análise. As seções a seguir fornecem mais informações sobre esses cenários.

### <a name="data-virtualization"></a>Virtualização de dados

Ao aproveitar [SQL Server polybase](../relational-databases/polybase/polybase-guide.md), SQL Server Big data clusters podem consultar fontes de dados externas sem mover ou copiar os dados. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]apresenta novos conectores para fontes de dados.

![Virtualização de dados](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Data Lake

Um cluster SQL Server Big Data inclui um pool de *armazenamento*do HDFS escalonável. Isso pode ser usado para armazenar Big Data, potencialmente ingerido de várias fontes externas. Depois que o Big Data for armazenado no HDFS no cluster Big Data, você poderá analisar e consultar os dados e combiná-los com os dados relacionais.

![Data Lake](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>data mart de expansão

SQL Server clusters Big Data fornecem computação e armazenamento de expansão para melhorar o desempenho da análise de todos os dados. Os dados de uma variedade de fontes podem ser ingeridos e distribuídos entre nós do *pool de dados* como um cache para análise posterior.

![Data Mart](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>IA integrado e Machine Learning

SQL Server clusters Big Data habilitam as tarefas de AI e de aprendizado de máquina nos dados armazenados em pools de armazenamento do HDFS e nos pools de dados. Você pode usar o Spark, bem como ferramentas internas de ia no SQL Server, usando R, Python, escala ou Java.

![IA e ML](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>Gerenciamento e monitoramento

O gerenciamento e o monitoramento são fornecidos por meio de uma combinação de ferramentas de linha de comando, APIs, portais e exibições de gerenciamento dinâmico.

Você pode usar Azure Data Studio para executar uma variedade de tarefas no cluster Big Data. Isso é habilitado pela nova **extensão SQL Server 2019 (versão prévia)** . Essa extensão fornece:

- Trechos de código internos para tarefas comuns de gerenciamento.
- Capacidade de navegar no HDFS, carregar arquivos, Visualizar arquivos e criar diretórios.
- Capacidade de criar, abrir e executar notebooks compatíveis com Jupyter.
- Assistente de virtualização de dados para simplificar a criação de fontes de dados externas.

## <a id="architecture"></a>Arquitectura

Um cluster SQL Server Big Data é um cluster de contêineres do Linux orquestrados por [kubernetes](https://kubernetes.io/docs/concepts/).

### <a name="kubernetes-concepts"></a>Conceitos de kubernetes

Kubernetes é um orquestrador de contêiner de código-fonte aberto, que pode dimensionar implantações de contêiner de acordo com a necessidade. A tabela a seguir define algumas terminologias kubernetes importantes:

|||
|:--|:--|
| **Cluster** | Um cluster kubernetes é um conjunto de computadores, conhecidos como nós. Um nó controla o cluster e é designado como o nó mestre; os nós restantes são nós de trabalho. O mestre kubernetes é responsável por distribuir o trabalho entre os trabalhadores e para monitorar a integridade do cluster. |
| **Nó** | Um nó executa aplicativos em contêineres. Pode ser um computador físico ou uma máquina virtual. Um cluster kubernetes pode conter uma combinação de máquinas físicas e nós de máquina virtual. |
| **Pod** | Um pod é a unidade de implantação atômica de kubernetes. Um pod é um grupo lógico de um ou mais contêineres – e recursos associados – necessários para executar um aplicativo. Cada pod é executado em um nó; um nó pode executar um ou mais pods. O mestre kubernetes atribui pods automaticamente aos nós no cluster. |
| &nbsp; ||

Em clusters de Big Data SQL Server, kubernetes é responsável pelo Estado dos clusters de Big Data SQL Server; O kubernetes compila e configura os nós de cluster, atribui pods a nós e monitora a integridade do cluster.

### <a name="big-data-clusters-architecture"></a>Arquitetura de clusters de Big data

O diagrama a seguir mostra os componentes de um cluster Big Data para SQL Server.

![Visão geral de arquitetura](media/big-data-cluster-overview/architecture-diagram-overview.png)

### <a id="controlplane"></a>Controle

O controlador fornece gerenciamento e segurança para o cluster. Ele contém o serviço cntrol, o repositório de configuração e outros serviços de nível de cluster, como Kibana, Grafana e pesquisa elástica.

### <a id="computeplane"></a>Pool de computação

O pool de computação fornece recursos computacionais para o cluster. Ele contém nós que executam SQL Server em Linux pods. Os pods no pool de computação são divididos em *instâncias de computação do SQL* para tarefas de processamento específicas. 

### <a id="dataplane"></a>Pool de dados

O pool de dados é usado para persistência de dados e cache. O pool de dados consiste em um ou mais pods em execução SQL Server em Linux. Ele é usado para ingerir dados de consultas SQL ou de trabalhos do Spark. SQL Server Big Data dados de cluster marts são persistidos no pool de dados. 

### <a name="storage-pool"></a>Pool de armazenamento

O pool de armazenamento consiste no pods do pool de armazenamento composto por SQL Server em Linux, Spark e HDFS. Todos os nós de armazenamento em um cluster SQL Server Big Data são membros de um cluster HDFS.

> [!TIP]
> Para obter uma análise detalhada do Big data a arquitetura e a instalação do cluster [, consulte Workshop: Microsoft SQL Server Big Data arquitetura](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)de clusters.

## <a name="next-steps"></a>Próximas etapas

SQL Server clusters Big Data está disponível pela primeira vez como uma visualização pública limitada por meio do programa de adoção antecipada do SQL Server 2019. Para solicitar acesso, registre-se [aqui](https://aka.ms/eapsignup)e especifique seu interesse para experimentar Big data clusters. A Microsoft fará a triagem de todas as solicitações e responderá assim que possível.
