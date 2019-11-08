---
title: Conceitos de segurança
titleSuffix: SQL Server big data clusters
description: Este artigo descreve os conceitos de segurança dos Clusters de Big Data do SQL Server. Isso inclui a descrição dos pontos de extremidade e da autenticação do cluster.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 35eb5e0a3236d8f016ed5ca99b769d628a4d81ed
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532373"
---
# <a name="security-concepts-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Conceitos de segurança do [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo abordará os principais conceitos relacionados à segurança no cluster de Big Data

Os [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] fornecem autenticação e autorização coerentes e consistentes. Um cluster de Big Data pode ser integrado ao Active Directory por meio de uma implantação totalmente automatizada que configura a integração do Active Directory em um domínio existente. Depois que um cluster de Big Data for configurado com a integração do Active Directory, aproveite as identidades e os grupos de usuários existentes para acesso unificado em todos os pontos de extremidade. Além disso, depois de criar tabelas externas no SQL Server, você pode controlar o acesso às fontes de dados permitindo acesso a tabelas externas aos usuários e grupos do Active Directory, centralizando as políticas de acesso a dados em uma só localização.

## <a name="authentication"></a>Autenticação

Os pontos de extremidade do cluster externo dão suporte à autenticação do Active Directory. Isso significa que você pode usar sua identidade do AD para autenticação no cluster de Big Data.

### <a name="cluster-endpoints"></a>Pontos de extremidade do cluster

Há cinco pontos de entrada para o cluster de Big Data

* Instância mestra – ponto de extremidade TDS para acessar a instância mestra do SQL Server no cluster, usando ferramentas de banco de dados e aplicativos como o SSMS ou o Azure Data Studio. Ao usar comandos do HDFS ou do SQL Server no azdata, a ferramenta se conectará aos outros pontos de extremidade, dependendo da operação.

* Gateway para acessar arquivos HDFS, Spark (KNOX) – esse é um ponto de extremidade baseado em HTTPS. O ponto de extremidade é usado para acessar serviços como o WebHDFS e o Spark.

* Ponto de extremidade do Serviço de Gerenciamento do Cluster (Controlador) – serviço de gerenciamento de cluster de Big Data que expõe APIs REST para gerenciar o cluster. A ferramenta azdata exige conexão com esse ponto de extremidade.

* Proxy de Gerenciamento – para acessar o painel Pesquisa de logs e o painel Métricas.

* Proxy de aplicativo – ponto de extremidade para gerenciar aplicativos implantados dentro do cluster de Big Data.

![Pontos de extremidade do cluster](media/concept-security/cluster_endpoints.png)

Atualmente, não há nenhuma opção de abrir portas adicionais para acessar o cluster de fora.

## <a name="authorization"></a>Autorização

Em todo o cluster, a segurança integrada entre diferentes componentes permite que a identidade do usuário original seja passada, durante a emissão de consultas do Spark e do SQL Server, até o HDFS. Conforme mencionado acima, os vários pontos de extremidade de cluster externo dão suporte à autenticação do AD.

Há dois níveis de verificações de autorização no cluster para gerenciar o acesso a dados. A autorização no contexto de Big Data é feita no SQL Server, usando as permissões tradicionais do SQL Server em objetos e no HDFS com ACLs (listas de controle), que associam as identidades de usuário a permissões específicas.

Um cluster de Big Data seguro implica no suporte uniforme e coerente a cenários de autenticação e autorização, tanto no SQL Server quanto no HDFS/Spark. Autenticação é o processo de verificar a identidade de um usuário ou serviço e de garantir que eles sejam quem alegam ser. Autorização refere-se à concessão ou negação de acesso a recursos específicos com base na identidade do usuário solicitante. Esta etapa é executada após um usuário ser identificado por meio da autenticação.

A autorização no contexto de Big Data geralmente é executada por meio de ACLs (listas de controle de acesso), que associam identidades do usuário a permissões específicas. O HDFS dá suporte à autorização limitando o acesso a APIs de serviço, arquivos HDFS e execução de trabalhos.

## <a name="encryption-and-other-security-mechanisms"></a>Criptografia e outros mecanismos de segurança

A criptografia da comunicação entre clientes com os pontos de extremidade externos, bem como entre componentes dentro do cluster, é protegida com o TLS/SSL, usando certificados.

Toda a comunicação do SQL Server com o SQL Server, como a instância mestra do SQL que se comunica com um pool de dados, é protegida usando logons do SQL.

## <a name="basic-administrator-login"></a>Logon de administrador básico

Você pode optar por implantar o cluster no modo do Active Directory ou usando somente o logon de administrador básico. Somente usar o logon de administrador básico não é um modo de segurança com suporte em produção e destina-se principalmente à avaliação do produto.

Mesmo que você escolha o modo do Active Directory, os logons básicos serão criados para o administrador do cluster. Isso fornece uma "porta dos fundos", caso a conectividade do AD esteja inoperante.

Após a implantação, esse logon básico receberá permissões de administrador no cluster. Isso significa que o usuário será o administrador do sistema na instância mestra do SQL Server e um administrador no controlador de cluster.
Os componentes do Hadoop não dão suporte à autenticação de modo misto, o que significa que um logon de administrador básico não pode ser usado para autenticação no gateway (KNOX).


Estas são as credenciais de logon que precisam ser definidas na implantação.

Nome de usuário administrador do cluster:
 + `AZDATA_USERNAME=<username>`

Senha de administrador do cluster:  
 + `AZDATA_PASSWORD=<password>`

> [!NOTE]
> Observe que, no modo não AD, o nome de usuário "raiz" deve ser usado em combinação com a senha acima, para autenticação no gateway (KNOX) para acesso ao HDFS/ao Spark.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira os seguintes recursos:

- [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
- [Workshop: Arquitetura dos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
