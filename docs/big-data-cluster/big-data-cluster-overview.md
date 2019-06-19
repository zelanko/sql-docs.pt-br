---
title: Quais são os clusters de big data?
titleSuffix: SQL Server big data clusters
description: Saiba mais sobre clusters de big data de 2019 do SQL Server (visualização) que são executados no Kubernetes e fornecem opções de escalabilidade horizontal para relacionais e dados do HDFS.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 12/07/2018
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: fed82f9bda8f72d92157de726eb6ae3c6ed1c0c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801885"
---
# <a name="what-are-sql-server-big-data-clusters"></a>O que são os clusters de Big Data do SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Começando com [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)], clusters de grandes dados do SQL Server permitem que você implante clusters escalonáveis de contêineres do HDFS, Spark e do SQL Server em execução no Kubernetes. Esses componentes são executados lado a lado para que você possa ler, gravar e processar big data do Transact-SQL ou o Spark, permitindo que você facilmente combinar e analisar seus dados relacionais de alto valor com grandes volumes de dados grandes.

Para obter mais informações sobre novos recursos e problemas conhecidos para a versão mais recente, consulte o [notas de versão](release-notes-big-data-cluster.md).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>Cenários

Clusters de grandes dados do SQL Server fornecem flexibilidade em como você interage com seu big data. Você pode consultar fontes de dados externas, armazenar big data no HDFS gerenciadas pelo SQL Server, ou consultar dados de várias fontes de dados externos por meio do cluster. Em seguida, você pode usar os dados de inteligência Artificial, aprendizado de máquina e outras tarefas de análise. As seções a seguir fornecem mais informações sobre esses cenários.

### <a name="data-virtualization"></a>Virtualização de dados

Aproveitando [PolyBase do SQL Server](../relational-databases/polybase/polybase-guide.md), clusters de grandes dados do SQL Server podem consultar fontes de dados externas sem mover ou copiar os dados. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] introduz novos conectores de fontes de dados.

![Virtualização de dados](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Lago de dados

Um cluster de big data do SQL Server inclui um HDFS escalonável *pool de armazenamento*. Isso pode ser usado para armazenar dados grandes, potencialmente ingeridos de várias fontes externas. Depois que o big data é armazenado no HDFS no cluster de big data, você pode analisar e consultar os dados e combiná-lo com seus dados relacionais.

![Lago de dados](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>Armazém de dados de expansão

Clusters de grandes dados do SQL Server fornecem computação de expansão e armazenamento para melhorar o desempenho de todos os dados de análise. Dados de uma variedade de fontes podem ser ingeridos e distribuídos entre *pool de dados* nós como um cache para análise posterior.

![armazém de dados](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>Inteligência Artificial integrada e aprendizado de máquina

Clusters de grandes dados do SQL Server habilitar tarefas nos dados armazenados em pools de armazenamento do HDFS e os pools de dados de aprendizado de máquina e IA. Você pode usar o Spark, bem como ferramentas de inteligência Artificial internas no SQL Server, usando o Java, Python, Scala ou R.

![ML e AI](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>Gerenciamento e monitoramento

Gerenciamento e monitoramento são fornecidos por meio de uma combinação de ferramentas de linha de comando, APIs, um portal do administrador e exibições de gerenciamento dinâmico.

O [portal do administrador de cluster](cluster-admin-portal.md) é uma interface da web que exibe o status e a integridade dos pods no cluster. Ele também fornece links para outros painéis para o log analytics e painéis de monitoramento.

Você pode usar o Studio de dados do Azure para executar uma variedade de tarefas no cluster de big data. Isso é habilitado pelo novo **extensão de 2019 (visualização) do SQL Server**. Essa extensão oferece:

- Trechos de código internos para tarefas comuns de gerenciamento.
- Capacidade de procurar HDFS, carregar arquivos, visualizar arquivos e criar diretórios.
- Capacidade de criar, abrir e executar compatível com o Jupyter notebooks.
- Assistente de virtualização de dados para simplificar a criação de fontes de dados externas.

## <a id="architecture"></a> Arquitetura

Um cluster de big data do SQL Server é um cluster de contêineres do Linux orquestrada pelo [Kubernetes](https://kubernetes.io/docs/concepts/).

### <a name="kubernetes-concepts"></a>Conceitos de Kubernetes

O Kubernetes é um orquestrador de contêiner do código-fonte aberto, que pode dimensionar as implantações de contêiner conforme a necessidade. A tabela a seguir define a terminologia importante Kubernetes:

|||
|:--|:--|
| **Cluster** | Um cluster Kubernetes é um conjunto de computadores, conhecidos como nós. Um nó controla o cluster e é designado o nó mestre; os nós restantes são nós de trabalho. O mestre de Kubernetes é responsável por distribuir o trabalho entre os trabalhadores e para monitorar a integridade do cluster. |
| **Nó** | Um nó executa aplicativos em contêineres. Ele pode ser um computador físico ou uma máquina virtual. Um cluster Kubernetes pode conter uma mistura de nós físicos de máquina e máquina virtual. |
| **pod** | Um pod é a unidade atômica de implantação do Kubernetes. Um pod é um grupo lógico de um ou mais contêineres- e associados a recursos necessários para executar um aplicativo. Cada pod é executado em um nó; um nó pode executar um ou mais pods. O mestre de Kubernetes atribui automaticamente os pods para nós no cluster. |
| &nbsp; ||

Em clusters de grandes dados do SQL Server, o Kubernetes é responsável pelo estado dos clusters grandes dados do SQL Server; Kubernetes cria e configura os nós de cluster, atribui pods para nós e monitora a integridade do cluster.

### <a name="big-data-clusters-architecture"></a>arquitetura de clusters de big data

Nós no cluster são organizados em três planos lógicos: o plano de controle, o plano de computação e o plano de dados. Cada plano tem responsabilidades diferentes no cluster. Todos os nós Kubernetes em um cluster de big data do SQL Server está hospedando os pods para componentes de pelo menos um plano.

![Visão geral de arquitetura](media/big-data-cluster-overview/architecture-diagram-planes.png)

### <a id="controlplane"></a> Plano de controle

O plano de controle fornece gerenciamento e segurança para o cluster. Ele contém o mestre de Kubernetes, o *instância mestre do SQL Server*e outros serviços de nível de cluster, como o Metastore do Hive e o Driver do Spark.

### <a id="computeplane"></a> Plano de computação

O plano de computação fornece recursos computacionais para o cluster. Ele contém nós executando o SQL Server no Linux pods. Os pods no plano de computação estão divididos *pools de computação* para determinado processamento de tarefas. Um pool de computação pode agir como um [PolyBase](../relational-databases/polybase/polybase-guide.md) grupo de escala horizontal para consultas distribuídas em dados de diferentes fontes – como como HDFS, Oracle, MongoDB ou Teradata.

### <a id="dataplane"></a> Plano de dados

O plano de dados é usado para persistência de dados e armazenamento em cache. Ele contém o pool de dados SQL e o pool de armazenamento.  O pool de dados SQL consiste em um ou mais pods executando o SQL Server no Linux. Ele é usado para a ingestão de dados de consultas SQL ou trabalhos do Spark. Grandes de dados do SQL Server data marts são mantidas no pool de dados do cluster. O pool de armazenamento consiste em pods de pool de armazenamento compostos do SQL Server no Linux, Spark e HDFS. Todos os nós de armazenamento em um cluster de big data do SQL Server são membros de um cluster do HDFS.

> [!TIP]
> Para obter uma visão mais detalhada em arquitetura de cluster de big data e a instalação, consulte [Workshop: Arquitetura de clusters de grandes dados do Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters).

## <a name="next-steps"></a>Próximas etapas

Clusters de grandes dados do SQL Server está disponível como visualização pública limitada por meio do programa de adoção antecipada do SQL Server de 2019. Para solicitar acesso, registre [aqui](https://aka.ms/eapsignup)e especifique seu interesse para experimentar os clusters de big data. A Microsoft todas as solicitações de triagem e responder assim que possível.
