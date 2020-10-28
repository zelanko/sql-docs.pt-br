---
title: Conceitos de segurança
titleSuffix: SQL Server big data clusters
description: Este artigo descreve os conceitos de segurança dos Clusters de Big Data do SQL Server. Esse conteúdo inclui a descrição dos pontos de extremidade e da autenticação do cluster.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7e3be3a3ea0d3f3b3d452bfea058ff85dd8a9141
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257242"
---
# <a name="security-concepts-for-big-data-clusters-2019"></a>Conceitos de segurança do [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo abordará os principais conceitos relacionados à segurança no cluster de Big Data

Os [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] fornecem autenticação e autorização coerentes e consistentes. Um cluster de Big Data pode ser integrado ao AD (Active Directory) por meio de uma implantação totalmente automatizada que configura a integração do AD em um domínio existente. Depois que um cluster de Big Data for configurado com a integração do AD, aproveite as identidades e os grupos de usuários existentes para acesso unificado em todos os pontos de extremidade. Além disso, depois de criar tabelas externas no SQL Server, você pode controlar o acesso às fontes de dados permitindo acesso a tabelas externas aos usuários e grupos do AD, centralizando as políticas de acesso a dados em uma só localização.

Neste vídeo de 14 minutos, você obterá uma visão geral da segurança do cluster de Big Data:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Overview-Big-Data-Cluster-Security/player?WT.mc_id=dataexposed-c9-niner]


## <a name="authentication"></a>Autenticação

Os pontos de extremidade do cluster externo dão suporte à autenticação do AD. Use sua identidade do AD para autenticação no cluster de Big Data.

### <a name="cluster-endpoints"></a>Pontos de extremidade do cluster

Há cinco pontos de entrada para o cluster de Big Data

* Instância mestra – ponto de extremidade TDS para acessar a instância mestra do SQL Server no cluster, usando ferramentas de banco de dados e aplicativos como o SSMS ou o Azure Data Studio. Ao usar comandos do HDFS ou do SQL Server na [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)], a ferramenta se conectará aos outros pontos de extremidade, dependendo da operação.

* Gateway para acessar arquivos HDFS, Spark (Knox) – ponto de extremidade HTTPS para acessar serviços como o webHDFS e o Spark.

* Ponto de extremidade do Serviço de Gerenciamento do Cluster (Controlador) – serviço de gerenciamento de cluster de Big Data que expõe APIs REST para gerenciar o cluster. A ferramenta azdata exige conexão com esse ponto de extremidade.

* Proxy de Gerenciamento – para acessar o painel Pesquisa de logs e o painel Métricas.

* Proxy de aplicativo – ponto de extremidade para gerenciar aplicativos implantados dentro do cluster de Big Data.

![Pontos de extremidade do cluster](media/concept-security/cluster_endpoints.png)

Atualmente, não há nenhuma opção de abrir portas adicionais para acessar o cluster de fora.

## <a name="authorization"></a>Autorização

Em todo o cluster, a segurança integrada entre diferentes componentes permite que a identidade do usuário original seja passada, durante a emissão de consultas do Spark e do SQL Server, até o HDFS. Conforme mencionado acima, os vários pontos de extremidade de cluster externo dão suporte à autenticação do AD.

Há dois níveis de verificações de autorização no cluster para gerenciar o acesso a dados. A autorização no contexto de Big Data é feita no SQL Server, usando as permissões tradicionais do SQL Server em objetos e no HDFS com ACLs (listas de controle), que associam as identidades de usuário a permissões específicas.

Um cluster de Big Data seguro implica no suporte uniforme e coerente a cenários de autenticação e autorização, tanto no SQL Server quanto no HDFS/Spark. Autenticação é o processo de verificar a identidade de um usuário ou serviço e de garantir que eles sejam quem alegam ser. Autorização refere-se à concessão ou negação de acesso a recursos específicos com base na identidade do usuário solicitante. Esta etapa é executada após um usuário ser identificado por meio da autenticação.

A autorização no contexto de Big Data é executada por meio de ACLs (listas de controle de acesso), que associam identidades de usuário a permissões específicas. O HDFS dá suporte à autorização limitando o acesso a APIs de serviço, arquivos HDFS e execução de trabalhos.

## <a name="encryption-in-flight-and-other-security-mechanisms"></a>Criptografia em trânsito e outros mecanismos de segurança

A criptografia da comunicação entre clientes com os pontos de extremidade externos, bem como entre componentes dentro do cluster, é protegida com o TLS/SSL, usando certificados.

Toda a comunicação do SQL Server com o SQL Server, como a instância mestra do SQL que se comunica com um pool de dados, é protegida usando logons do SQL.

> [!IMPORTANT]
>  Os Clusters de Big Data usam `etcd` para armazenar as credenciais. Como prática recomendada, é necessário garantir que o cluster do Kubernetes esteja configurado para usar a criptografia `etcd` em repouso. Por padrão, os segredos armazenados em `etcd` serão descriptografados. A documentação do Kubernetes fornece detalhes sobre esta tarefa administrativa: https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/ e https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/.

## <a name="data-encryption-at-rest"></a>Criptografia de dados em repouso

A capacidade de criptografia em repouso de Clusters de Big Data do SQL Server dá suporte ao cenário principal de criptografia de nível de aplicativo para os componentes do SQL Server e do HDFS. Siga o artigo [Guia de configuração e conceitos de criptografia em repouso](encryption-at-rest-concepts-and-configuration.md) para obter um guia abrangente de uso dos recursos.

> [!IMPORTANT]
> A criptografia de volume é recomendada para todas as implantações de Cluster de Big Data do SQL Server. Os volumes de armazenamento fornecidos pelo cliente configurados em clusters do Kubernetes também devem ser criptografados, como uma abordagem abrangente da criptografia de dados em repouso. A capacidade de criptografia em repouso do Cluster de Big Data do SQL Server é uma camada de segurança adicional, fornecendo criptografia em nível de aplicativo aos arquivos de log e dados do SQL Server e suporte à zona de criptografia do HDFS.


## <a name="basic-administrator-login"></a>Logon de administrador básico

Você pode optar por implantar o cluster no modo do AD ou usando somente o logon de administrador básico. Somente usar o logon de administrador básico não é um modo de segurança com suporte em produção e destina-se à avaliação do produto.

Mesmo que você escolha o modo do Active Directory, os logons básicos serão criados para o administrador do cluster. Esse recurso fornece acesso alternativo, caso a conectividade do AD esteja inoperante.

Após a implantação, esse logon básico receberá permissões de administrador no cluster. O usuário do logon será o administrador do sistema na instância mestra do SQL Server e um administrador no controlador de cluster.
Os componentes do Hadoop não dão suporte à autenticação de modo misto, o que significa que um logon de administrador básico não pode ser usado para autenticação no gateway (Knox).

As credenciais de logon que você precisa definir na implantação incluem:

Nome de usuário administrador do cluster:

 + `AZDATA_USERNAME=<username>`

Senha de administrador do cluster:  
 + `AZDATA_PASSWORD=<password>`

> [!NOTE]
> Observe que, no modo não AD, o nome de usuário deve ser usado em combinação com a senha acima, para autenticação no gateway (KNOX) para acesso ao HDFS/Spark. Antes do SQL Server 2019 CU5, o nome de usuário era `root`.
> 
> [!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

## <a name="next-steps"></a>Próximas etapas

[O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)

[Workshop: Arquitetura dos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)

[RBAC de Kubernetes](kubernetes-rbac.md)
