---
title: Monitorar cluster com Jupyter notebooks e Azure Data Studio
titleSuffix: SQL Server Big Data Clusters
description: Monitorar cluster com Jupyter notebooks e Azure Data Studio no cluster de Big Data do SQL Server 2019.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 10/01/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 516b1bb461e5927ff52f0cee79e48d9945e6da21
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378356"
---
# <a name="monitoring-cluster-with-notebooks"></a>Monitorar o cluster com notebooks

Esta página é um índice de notebooks para Clusters de Big Data do SQL Server. Esses notebooks executáveis (.ipynb) foram criados para o SQL Server 2019 para auxiliar no monitoramento de Clusters de Big Data.

Cada notebook foi criado para conferir suas próprias dependências. Um **Executar todas as células** vai ser concluído com êxito ou gerar uma exceção com uma dica de hiperlink para um outro notebook resolver a dependência ausente. Siga o hiperlink de dica para o notebook subsequente, pressione **Executar todas as células** e, tendo êxito, volte para o notebook original e pressione **Executar todas as células** .

Depois que todas as dependências forem instaladas mas **Executar todas as células** falhar, cada notebook analisará os resultados e, sempre que possível, produzirá um hiperlink de dica para outro notebook a fim de ajudar a resolver o problema.


## <a name="monitoring-kubernetes"></a>Como monitorar o Kubernetes

Esta seção contém um conjunto de notebooks úteis para obter informações e status sobre um cluster de Big Data do SQL Server que usa a CLI (interface de linha de comando) do `azdata`.

|Name |Descrição |
|---|---|---|---|
|TSG006 – Obter o status do pod do sistema|Exiba o status de todos os pods do sistema. |
|TSG007 – Obter o status do pod do BDC|Exiba o status dos pods do cluster de Big Data.|
|TSG008 – Obter informações de versão (Kubernetes)|Obtenha as informações de cluster do Kubernetes.|
|TSG009 – Obter nós (Kubernetes)|Obtenha os contextos do Kubernetes. |
|TSG010 – Obter contextos de configuração|Como usar a consulta DMV para obter mais informações sobre o erro interno do processador de consultas|
|TSG015 – Ver serviços BDC (Kubernetes)|Obtenha o status dos serviços do cluster BDC implantado no cluster do Kubernetes. |
|TSG016 – Descrever os pods do BDC|Obtenha o status dos pods do BDC implantado no cluster do Kubernetes. |
|TSG020 – Descrever nós (Kubernetes)|Obtenha as informações de nó do cluster BDC. Use a interface de linha de comando kubectl. |
|TSG021 – Obter informações do cluster (Kubernetes)|Obtenha as informações de cluster do Kubernetes. |
|TSG022 – Obter o endereço IP externo do host kubeadm|Obtenha o endereço IP externo do host de kubeadm. |
|TSG023 – Obter todos os objetos BDC (Kubernetes)|Obtenha um resumo de todos os recursos do Kubernetes para o namespace do sistema e o namespace do cluster de Big Data. |
|TSG042 – Obter o nome do nó e as montagens externas para PVCs de dados e de logs|Obtenha o pod de hospedagem do nome do nó juntamente com as montagens externas de dados e de logs. |
|TSG063 – Obter classes de armazenamento (Kubernetes)|Use este notebook para obter classes de armazenamento do Kubernetes. |
|TSG064 – Obter declarações de volume persistente do BDC|Mostre as PVCs (Declarações de Volume Persistente) para o cluster de Big Data. |
|TSG065 – Obter segredos do BDC (Kubernetes)|Veja os segredos do cluster de Big Data. |
|TSG066 – Obter o evento do BDC (Kubernetes)|Veja os eventos do cluster de Big Data.|
|TSG072 – Obter volumes persistentes (Kubernetes)|Mostre os PVs (volumes persistentes) para o cluster do Kubernetes. Os Volumes Persistentes são objetos que não são namespaces. |
|TSG081 – Obter namespaces (Kubernetes)|Obtenha os namespaces do Kubernetes. |
|TSG089 – Descrever pods não em execução do BDC|Mostre pods do BDC não em execução para o cluster do Kubernetes. |
|TSG097 – Obter conjuntos com estado de BDC (Kubernetes)|Mostre conjuntos com estado do BDC para o cluster do Kubernetes. |
|TSG098 – Obter conjuntos de réplica do BDC (Kubernetes)|Mostre conjuntos de réplica do BDC para o cluster do Kubernetes. |
|TSG099 – Obter daemonsets do BDC (Kubernetes)|Mostre daemonsets do BDC para o cluster do Kubernetes. |


## <a name="monitor-big-data-cluster-bdc"></a>Monitorar o BDC (cluster de Big Data)

Esta seção contém um conjunto de notebooks úteis para obter informações e status sobre o cluster do Kubernetes que hospeda o BDC (Cluster de Big Data) do SQL Server.

|Name |Descrição |
|---|---|---|---|
|TSG003 – Mostrar as sessões do BDC Spark|Veja sessões do Spark do BDC. |
|TSG004 – Mostrar aplicativos do BDC|Veja os aplicativos em funcionamento no cluster BDC.|
|TSG012 – Mostrar status do BDC|Obtenha o status atual de diferentes componentes do cluster BDC.|
|TSG013 – Mostrar lista de arquivos no pool de armazenamento (HDFS)|Obtenha a lista de arquivos no pool de armazenamento (HDFS). |
|TSG014 – Mostrar pontos de extremidade do BDC|Obtenha todos os pontos de extremidade disponíveis para o cluster BDC.|
|TSG017 – Mostrar a configuração do BDC|Obtenha a configuração do BDC. |
|TSG033 – Mostrar status do SQL do BDC|Obtenha o status do SQL Server do BDC implantado no cluster do Kubernetes. |
|TSG049 – Mostrar o status do controlador do BDC|Obtenha o status do controlador do BDC implantado no cluster do Kubernetes. |
|TSG068 – Mostrar o status do HDFS do BDC|Obtenha o status do HDFS do BDC implantado no cluster do Kubernetes. |
|TSG069 – Mostrar o status do gateway do Cluster de Big Data|Obtenha o status do gateway do BDC implantado no cluster do Kubernetes. |
|TSG070 – Consultar o pool mestre do SQL| Execute uma consulta SQL na instância mestra. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
