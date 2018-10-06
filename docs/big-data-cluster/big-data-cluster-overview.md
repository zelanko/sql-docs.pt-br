---
title: O que é o SQL Server 2019 clusters de big data? | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: overview
ms.prod: sql
ms.openlocfilehash: cf13ea198a5a40a5d67d41fea2f8f9b9b3b5434d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795794"
---
# <a name="what-is-sql-server-2019-big-data-clusters"></a>O que é o SQL Server 2019 clusters de big data?

Começando com [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)], clusters de grandes dados do SQL Server permitem que você implante clusters escalonáveis de contêineres do Docker do HDFS, Spark e do SQL Server em execução no Kubernetes. Esses componentes são executados lado a lado para que você possa ler, gravar e processar big data do Transact-SQL ou Spark. Clusters de grandes dados do SQL Server permitem que você combine e analisar seus dados relacionais de alto valor com alto volume de big data com facilidade.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>Cenários

Clusters de grandes dados do SQL Server fornecem flexibilidade em como você interage com seu big data. Você pode consultar fontes de dados externas, armazenar big data no HDFS gerenciadas pelo SQL Server, ou efetuar pull de dados de várias fontes de dados no cluster. Em seguida, você pode usar os dados de inteligência Artificial, aprendizado de máquina e outras tarefas de análise. As seções a seguir fornecem mais informações sobre esses cenários.

### <a name="data-virtualization"></a>Virtualização de dados

Aproveitando [PolyBase do SQL Server](../relational-databases/polybase/polybase-guide.md), clusters de grandes dados do SQL Server podem consultar fontes de dados externos sem importá-los. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] introduz novos conectores de fontes de dados.

![Virtualização de dados](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Lago de dados

Um cluster de big data do SQL Server inclui um HDFS escalonável *pool de armazenamento*. Isso pode ser usado para armazenar diretamente dados grandes, potencialmente ingeridos de várias fontes externas. Uma vez no cluster de big data, você pode analisar e consultar os dados e combiná-lo com seus dados relacionais de alto valor.

![Lago de dados](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>Armazém de dados de expansão

Clusters de grandes dados do SQL Server fornecem computação de expansão e armazenamento para melhorar o desempenho de todos os dados de análise. Dados de uma variedade de fontes podem ser ingeridos e distribuídos entre *pool de dados* nós para análise posterior.

![armazém de dados](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>Inteligência Artificial integrada e aprendizado de máquina

Clusters de grandes dados do SQL Server habilitar tarefas nos dados armazenados em dados de pools de armazenamento do HDFS e os pools de dados de aprendizado de máquina e IA. Você pode usar o Spark, bem como ferramentas de inteligência Artificial internas no SQL Server, usando o R, Python ou Java.

![ML e AI](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>Gerenciamento e monitoramento

Gerenciamento e monitoramento são fornecidos por meio de uma combinação de componentes de código-fonte aberto, ferramentas do SQL Server e exibições de gerenciamento dinâmico.

O [Portal de administração de Cluster](cluster-admin-portal.md) é uma interface da web que exibe o status e a integridade dos pods no cluster. Ele também fornece links para outros painéis fornecidos pelo Grafana e Kibana.

Você pode usar o Studio de dados do Azure para executar uma variedade de tarefas no cluster de big data. Isso é habilitado pelo novo **extensão de 2019 (visualização) do SQL Server**. Essa extensão oferece:

- Trechos de código internos para tarefas comuns de gerenciamento.
- Relatórios sobre o número de pools de computação e o status de trabalhos em execução.
- Relatórios sobre o status dos trabalhos de Spark e HDFS.
- Capacidade de procurar HDFS, carregar arquivos, visualizar arquivos e criar diretórios.
- Capacidade de criar, abrir e executar compatível com o Jupyter notebooks.
- Assistente de virtualização de dados para simplificar a criação de fontes de dados externas.

## <a id="architecture"></a> Arquitetura

Um cluster de big data do SQL Server é um cluster de nós do Linux orquestrada pelo [Kubernetes](https://kubernetes.io/docs/concepts/).

### <a name="kubernetes-concepts"></a>Conceitos de Kubernetes

O Kubernetes é um orquestrador de contêiner do código-fonte aberto, que pode dimensionar as implantações de contêiner conforme a necessidade. A tabela a seguir define a terminologia importante Kubernetes:

|||
|--|--|
| **Cluster** | Um cluster Kubernetes é um conjunto de computadores, conhecidos como nós. Um nó controla o cluster e é designado o nó mestre; os nós restantes são nós de trabalho. O mestre de Kubernetes é responsável por distribuir o trabalho entre os trabalhadores e para monitorar a integridade do cluster. |
| **Nó** | Um nó executa aplicativos em contêineres. Ele pode ser um computador físico ou uma máquina virtual. Um cluster Kubernetes pode conter uma mistura de nós físicos de máquina e máquina virtual. |
| **pod** | Um pod é a unidade atômica de Kubernetes. Um pod é um grupo lógico de um ou mais contêineres — e recursos associados — necessários para executar um aplicativo. Cada pod é executado em um nó; um nó pode executar um ou mais pods. O mestre de Kubernetes atribui automaticamente os pods para nós no cluster. |

Em clusters de grandes dados do SQL Server, o Kubernetes é responsável pelo estado dos clusters grandes dados do SQL Server; Kubernetes cria e configura os nós de cluster, atribui pods para nós e monitora a integridade do cluster.

### <a name="big-data-clusters-architecture"></a>arquitetura de clusters de big data

Nós no cluster são organizados em três planos lógicos: o plano de controle, o painel de computação e o plano de dados. Cada plano tem responsabilidades diferentes no cluster. Todos os nós Kubernetes em um cluster de big data do SQL Server é membro de pelo menos um plano.

![Visão geral de arquitetura](media/big-data-cluster-overview/architecture-diagram-planes.png)

### <a id="controlplane"></a> Plano de controle

O plano de controle fornece gerenciamento e segurança para o cluster. Ele contém o mestre de Kubernetes, o *instância mestre do SQL Server*e outros serviços de nível de cluster, como o Metastore do Hive e o Driver do Spark.

### <a id="computeplane"></a> Plano de computação

O plano de computação fornece recursos computacionais para o cluster. Ele contém nós executando o SQL Server no Linux pods. Os pods no plano de computação estão divididos *pools de computação* para determinado processamento de tarefas. Um pool de computação pode agir como um [PolyBase](../relational-databases/polybase/polybase-guide.md) grupo de escala horizontal para consultas distribuídas ao longo de diferentes fontes de dados — como o HDFS, Oracle, MongoDB ou Teradata.

### <a id="dataplane"></a> Plano de dados

O plano de dados é usado para persistência de dados e armazenamento em cache. Ele contém o conjunto de dados SQL e nós de armazenamento.  O pool de dados SQL consiste em um ou mais nós executando o SQL Server no Linux. Ele é usado para a ingestão de dados de consultas SQL ou trabalhos do Spark. Grandes de dados do SQL Server data marts são mantidas no pool de dados do cluster. O pool de armazenamento consiste em armazenamento compostos de nós do SQL Server no Linux, Spark e HDFS. Todos os nós de armazenamento em um cluster de big data do SQL Server são membros de um cluster do HDFS.

## <a name="next-steps"></a>Próximas etapas

Clusters de grandes dados do SQL Server está disponível como visualização pública limitada por meio do programa de adoção antecipada do SQL Server de 2019. Para solicitar acesso, registre [aqui](https://aka.ms/eapsignup)e especifique seu interesse para experimentar os clusters de big data. A Microsoft todas as solicitações de triagem e responder assim que possível.