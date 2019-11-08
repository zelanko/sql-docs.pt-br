---
title: Notas sobre a versão de Clusters de Big Data do SQL Server
titleSuffix: SQL Server big data clusters
description: Este artigo descreve as atualizações mais recentes e os problemas conhecidos para [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (versão prévia).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e868d5db99c3f0be141d28a881d8d8bc6f9c241e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531639"
---
# <a name="sql-server-big-data-clusters-release-notes"></a>Notas sobre a versão de Clusters de Big Data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Obter informações quase em tempo real de todos os seus dados com [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], que fornecem um ambiente completo para trabalhar com grandes conjuntos de dados, incluindo funcionalidades de aprendizado de máquina e IA.

Este artigo lista as atualizações e os problemas conhecidos para as versões mais recentes do BDC ([!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]).

## <a id="rtm"></a> SQL Server 2019

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] apresenta os Clusters de Big Data do SQL Server.

Use Clusters de Big Data do SQL Server para:

- [Implantar clusters escalonáveis](../big-data-cluster/deploy-get-started.md) de contêineres do SQL Server, do Spark e do HDFS em execução no Kubernetes. 
- Ler, gravar e processar Big Data do Transact-SQL ou do Spark.
- Combine e analise facilmente dados relacionais de valor elevado com Big Data de volume grande.
- Consultar fontes de dados externas.
- Armazenar Big Data no HDFS gerenciado por SQL Server.
- Consultar dados de várias fontes de dados externas por meio do cluster.
- Usar os dados para IA, aprendizado de máquina e outras tarefas de análise.
- [Implantar e executar aplicativos](../big-data-cluster/concept-application-deployment.md) em [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)].
- Virtualizar dados com o [PolyBase](../relational-databases/polybase/polybase-guide.md). Consulte dados de SQL Server externos, Oracle, Teradata, MongoDB e fontes de dados ODBC com tabelas externas.
- Forneça alta disponibilidade para a instância mestra do SQL Server e todos os bancos de dados usando a tecnologia de grupo de disponibilidade Always On.

## <a name="sql-server-version"></a>Versão do SQL Server

A versão atual do SQL Server é `15.0.2070.34`.

## <a name="image-tags"></a>Marcas de imagem

A tag de imagem desta versão é `2019-GDR1-ubuntu-16.04`.

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="supportability"></a>Suporte

Esta seção explica as plataformas compatíveis com o BDC ([!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]).

### <a name="kubernetes-platforms"></a>Plataformas do Kubernetes

|Plataforma|Versões com suporte|
|---------|---------|
|Kubernetes|O BDC requer a versão mínima do Kubernetes 1.13. Confira a [política de suporte a distorção de versão e kubernetes do Kubernetes](https://kubernetes.io/docs/setup/release/version-skew-policy/) para a política de suporte à versão do Kubernetes.|
|AKS (Serviço de Kubernetes do Azure)|O BDC requer a versão mínima do AKS 1.13.<br/>Confira [Versões do Kubernetes com suporte no AKS](/azure/aks/supported-kubernetes-versions) para obter a política de suporte de versão.|

### <a name="host-os-for-kubernetes"></a>SO host para Kubernetes

|Plataforma|Versões com suporte|
|---------|---------|
|Red Hat Enterprise Linux|7.3, 7.4, 7.5, 7.6|
|Ubuntu|16.04|

### <a name="tools"></a>Ferramentas

|Plataforma|Versões com suporte|
|---------|---------|
|`azdata`|Deve ser a mesma versão secundária que a do servidor (a mesma instância mestra do SQL Server).<br/>Execute `azdata –-version` para validar a versão. Atualmente, esta versão é `15.0.2070`.|
|Azure Data Studio|Obtenha o build mais recente do [Azure Data Studio](https://aka.ms/getazuredatastudio).|

### <a name="sql-server-editions"></a>Edições do SQL Server

|Edition|Observações|
|---------|---------|
|Enterprise<br/>Standard<br/>Desenvolvedor| A edição de cluster de Big Data é determinada pela edição da instância mestra do SQL Server. No momento da implantação, a Developer Edition é implantada por padrão. Você pode alterar a edição após a implantação. Confira [Configurar a instância mestra do SQL Server](../big-data-cluster/configure-sql-server-master-instance.md). |

## <a name="known-issues"></a>Problemas conhecidos

### <a name="livy-job-submission-from-azure-data-studio-ads-or-curl-fail-with-500-error"></a>O envio de trabalho do Livy do ADS (Azure Data Studio) ou da ondulação falha com o erro 500

**Problema e impacto sobre o cliente**: Em uma configuração de HA, os recursos compartilhados do Spark (sparkhead) são configurados com várias réplicas. Nesse caso, você pode encontrar falhas com o envio de trabalho do Livy do ADS (Azure Data Studio) ou `curl`. Para verificar, `curl` para qualquer pod do sparkhead resulta em uma conexão recusada. Por exemplo, `curl https://sparkhead-0:8998/` ou `curl https://sparkhead-1:8998` retorna um erro 500.

Isso acontece dos seguintes cenários:

- Os pods ou processo do ZooKeeper para cada instância do ZooKeeper são reiniciados algumas vezes.
- Quando a conectividade de rede não é confiável entre o pod do Sparkhead e os pods do ZooKeeper.

**Solução alternativa**: Reiniciar ambos os servidores Livy.

```bash
kubectl -n <clustername> exec sparkhead-0 -c hadoop-livy-sparkhistory supervisorctl restart livy
```

```bash
kubectl -n <clustername> exec sparkhead-1 -c hadoop-livy-sparkhistory supervisorctl restart livy
```

### <a name="create-memory-optimized-table-when-master-instance-in-an-availability-group"></a>Criar uma tabela otimizada para memória quando a instância mestra em um grupo de disponibilidade

- **Problema e impacto sobre o cliente**: Você não pode usar o ponto de extremidade primário exposto para conectar-se a bancos de dados do grupo de disponibilidade (ouvinte) para criar tabelas otimizadas para memória.

- **Solução alternativa**: Para criar tabelas otimizadas para memória quando a instância mestra do SQL Server for uma configuração de grupo de disponibilidade, [conecte-se à instância do SQL Server](deployment-high-availability.md#instance-connect), exponha um ponto de extremidade, conecte-se ao banco de dados do SQL Server e crie as tabelas otimizadas para memória na sessão criada com a nova conexão.

### <a name="insert-to-external-tables-active-directory-authentication-mode"></a>Inserir no modo de autenticação do Active Directory de tabelas externas

- **Problema e impacto sobre o cliente**: Quando a instância mestra do SQL Server está no modo de autenticação do Active Directory, uma consulta que seleciona somente de tabelas externas, em que pelo menos uma das tabelas externas está em um pool de armazenamento e insere em outra tabela externa, a consulta retorna:

   ```
   Msg 7320, Level 16, State 102, Line 1
   Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "SQLNCLI11". Only domain logins can be used to query Kerberized storage pool.
   ```

- **Solução alternativa**: Modifique a consulta de uma das maneiras a seguir. Ingresse a tabela do pool de armazenamento em uma tabela local ou insira-a primeiro na tabela local e depois leia da tabela local para inseri-la no pool de dados.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
