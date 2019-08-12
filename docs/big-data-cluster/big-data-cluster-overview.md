---
title: O que são clusters de Big Data?
titleSuffix: SQL Server big data clusters
description: Saiba mais sobre os clusters de Big Data do SQL Server 2019 (versão prévia) que são executados no Kubernetes e fornecem opções de expansão para dados relacionais e do HDFS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0beb4ea57ba6c2591e5b2c06a7775fc2d7e8b26c
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68419501"
---
# <a name="what-are-sql-server-big-data-clusters"></a>O que são os clusters de Big Data do SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Começando no [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)], os clusters de Big Data do SQL Server permitem implantar clusters escalonáveis de contêineres do SQL Server, do Spark e do HDFS em execução no Kubernetes. Esses componentes são executados lado a lado para permitir que você leia, grave e processe Big Data do Transact-SQL ou do Spark, permitindo combinar e analisar facilmente seus dados relacionais de alto valor com Big Data de alto volume.

Para obter mais informações sobre os novos recursos e problemas conhecidos da versão mais recente, confira as [notas sobre a versão](release-notes-big-data-cluster.md).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>Cenários

Clusters de Big Data do SQL Server fornecem flexibilidade na maneira como você interage com seu Big Data. Você pode consultar fontes de dados externas, armazenar Big Data no HDFS gerenciado pelo SQL Server ou consultar dados de várias fontes de dados externas por meio do cluster. Depois, você pode usar os dados para IA, aprendizado de máquina e outras tarefas de análise. As seções a seguir fornecem mais informações sobre estes cenários.

### <a name="data-virtualization"></a>Virtualização de dados

Utilizando o [SQL Server PolyBase](../relational-databases/polybase/polybase-guide.md), os clusters de Big Data do SQL Server podem consultar fontes de dados externas sem mover ou copiar os dados. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] apresenta novos conectores para fontes de dados.

![Virtualização de dados](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Data Lake

Um cluster de Big Data do SQL Server inclui um *pool de armazenamento* do HDFS escalonável. Ele pode ser usado para armazenar Big Data, potencialmente ingerido de várias fontes externas. Após o Big Data ser armazenado no HDFS no cluster de Big Data, você poderá analisar e consultar os dados e combiná-los com os dados relacionais.

![Data Lake](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>Data mart de expansão

Clusters de Big Data do SQL Server fornecem computação de expansão e armazenamento para melhorar o desempenho da análise de qualquer dado. Dados de diversas origens podem ser ingeridos e distribuídos entre nós do *pool de dados* como um cache para análise posterior.

![Data mart](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>IA e aprendizado de máquina integrados

Clusters de Big Data do SQL Server habilitam tarefas de IA e de aprendizado de máquina nos dados armazenados em pools de armazenamento do HDFS e nos pools de dados. Você pode usar o Spark, bem como ferramentas internas de IA no SQL Server, usando R, Python, Scala ou Java.

![IA e ML](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>Gerenciamento e monitoramento

O gerenciamento e o monitoramento são fornecidos por meio de uma combinação de ferramentas de linha de comando, APIs, portais e exibições de gerenciamento dinâmico.

Você pode usar o Azure Data Studio para executar uma variedade de tarefas no cluster de Big Data. Isso é habilitado pela nova **Extensão do SQL Server 2019 (versão prévia)** . Essa extensão fornece:

- Snippets internos para tarefas comuns de gerenciamento.
- Capacidade de navegar no HDFS, carregar arquivos, visualizar arquivos e criar diretórios.
- Capacidade de criar, abrir e executar notebooks compatíveis com Jupyter.
- Assistente de virtualização de dados para simplificar a criação de fontes de dados externas.

## <a id="architecture"></a> Arquitetura

Um cluster de Big Data do SQL Server é um cluster de contêineres Linux orquestrados pelo [Kubernetes](https://kubernetes.io/docs/concepts/).

### <a name="kubernetes-concepts"></a>Conceitos do Kubernetes

O Kubernetes é um orquestrador de contêineres de software livre que pode dimensionar implantações de contêiner de acordo com a necessidade. A tabela a seguir define algumas terminologias importantes do Kubernetes:

|||
|:--|:--|
| **Cluster** | Um cluster do Kubernetes é um conjunto de computadores, conhecidos como nós. Um nó controla o cluster e é designado como nó mestre; os nós restantes são nós de trabalho. O mestre do Kubernetes é responsável por distribuir o trabalho entre os trabalhadores e por monitorar a integridade do cluster. |
| **Nó** | Um nó executa aplicativos em contêineres. Ele pode ser um computador físico ou uma máquina virtual. Um cluster do Kubernetes pode conter uma combinação de nós de computadores físicos e de máquinas virtuais. |
| **Pod** | Um pod é a unidade de implantação atômica do Kubernetes. Um pod é um grupo lógico de um ou mais contêineres – e recursos associados – necessários para executar um aplicativo. Cada pod é executado em um nó; um nó pode executar um ou mais pods. O mestre do Kubernetes atribui pods automaticamente aos nós no cluster. |
| &nbsp; ||

Em clusters de Big Data do SQL Server, o Kubernetes é responsável pelo estado dos clusters de Big Data do SQL Server. O Kubernetes compila e configura os nós do cluster, atribui pods a nós e monitora a integridade do cluster.

### <a name="big-data-clusters-architecture"></a>Arquitetura de clusters de Big Data

O diagrama a seguir mostra os componentes de um cluster de Big Data para o SQL Server.

![Visão geral de arquitetura](media/big-data-cluster-overview/architecture-diagram-overview.png)

### <a id="controlplane"></a> Controlador

O controlador fornece gerenciamento e segurança para o cluster. Ele contém o serviço de controle, o repositório de configurações e outros serviços no nível do cluster, como Kibana, Grafana e Pesquisa elástica.

### <a id="computeplane"></a> Pool de computação

O pool de computação fornece recursos computacionais para o cluster. Ele contém nós que executam pods do SQL Server em Linux. Os pods no pool de computação são divididos em *instâncias de computação do SQL* para tarefas de processamento específicas. 

### <a id="dataplane"></a> Pool de dados

O pool de dados é usado para persistência e cache de dados. O pool de dados é composto por um ou mais pods em execução no SQL Server em Linux. Ele é usado para ingerir dados de consultas SQL ou de trabalhos do Spark. Data marts do cluster de Big Data do SQL Server são persistidos no pool de dados. 

### <a name="storage-pool"></a>Pool de armazenamento

O pool de armazenamento é composto por pods do pool de armazenamento compostos pelo SQL Server em Linux, pelo Spark e pelo HDFS. Todos os nós de armazenamento em um cluster de Big Data do SQL Server são membros de um cluster do HDFS.

> [!TIP]
> Para obter uma análise detalhada da arquitetura e da instalação do cluster de Big Data, confira [Workshop: Arquitetura de clusters de Big Data do Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters).

## <a name="next-steps"></a>Próximas etapas

Os clusters de Big Data do SQL Server estão disponíveis primeiro como uma versão prévia pública limitada por meio do Programa de adoção antecipada do SQL Server 2019. Para solicitar acesso, registre-se [aqui](https://aka.ms/eapsignup) e especifique seu interesse de experimentar os clusters de Big Data. A Microsoft fará a triagem de todas as solicitações e responderá assim que possível.
