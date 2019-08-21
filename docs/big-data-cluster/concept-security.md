---
title: Conceitos de segurança
titleSuffix: SQL Server big data clusters
description: Este artigo descreve os conceitos de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]segurança para o. Isso inclui a descrição dos pontos de extremidade e da autenticação do cluster.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4e4441f0cc4f19d4784019408bfc5309a5734285
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652251"
---
# <a name="security-concepts-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Conceitos de segurança para[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Um cluster de Big Data seguro implica no suporte uniforme e coerente a cenários de autenticação e autorização, tanto no SQL Server quanto no HDFS/Spark. Autenticação é o processo de verificar a identidade de um usuário ou serviço e de garantir que eles sejam quem alegam ser. Autorização refere-se à concessão ou negação de acesso a recursos específicos com base na identidade do usuário solicitante. Esta etapa é executada após um usuário ser identificado por meio da autenticação.

A autorização no contexto de Big Data geralmente é executada por meio de ACLs (listas de controle de acesso), que associam identidades do usuário a permissões específicas. O HDFS dá suporte à autorização limitando o acesso a APIs de serviço, arquivos HDFS e execução de trabalhos.

Este artigo abordará os principais conceitos relacionados à segurança no cluster de Big Data.

## <a name="cluster-endpoints"></a>Pontos de extremidade do cluster

Há três pontos de entrada para o cluster de Big Data

* Gateway do HDFS/Spark (Knox) – este é um ponto de extremidade baseado em HTTPS. Outros pontos de extremidade são acessados por proxy por meio deste. O gateway do HDFS/Spark é usado para acessar serviços como webHDFS e Livy. Sempre que você vir referências a Knox, este é o ponto de extremidade.

* Ponto de extremidade do controlador – serviço de gerenciamento do cluster de Big Data que expõe APIs REST para gerenciar o cluster. Algumas ferramentas também são acessadas por meio deste ponto de extremidade.

* Instância mestre – ponto de extremidade do TDS para aplicativos e ferramentas de banco de dados se conectarem à instância mestre do SQL Server no cluster.

![Pontos de extremidade do cluster](media/concept-security/cluster_endpoints.png)

Atualmente, não há nenhuma opção de abrir portas adicionais para acessar o cluster de fora.

### <a name="how-endpoints-are-secured"></a>Como pontos de extremidade são protegidos

A proteção de pontos de extremidade no cluster de Big Data é feita usando senhas que podem ser definidas/atualizadas usando variáveis de ambiente ou comandos da CLI. Todas as senhas internas do cluster são armazenadas como segredos do Kubernetes.  

## <a name="authentication"></a>Autenticação

Após o provisionamento do cluster, vários logons são criados.

Alguns desses logons são usados para que os serviços se comuniquem entre si e outros para que os usuários finais acessem o cluster.

### <a name="end-user-authentication"></a>Autenticação do usuário final
Após o provisionamento do cluster, várias senhas do usuário final precisam ser definidas usando variáveis de ambiente. Essas são senhas que os administradores do SQL e do cluster usam para acessar os serviços:

Nome de usuário do controlador:
 + CONTROLLER_USERNAME=<controller_username>

Senha do controlador:  
 + CONTROLLER_PASSWORD=<senha_do_controlador>

Senha SA mestre do SQL: 
 + MSSQL_SA_PASSWORD=<controller_sa_password>

Senha para acessar o ponto de extremidade do HDFS/Spark:
 + KNOX_PASSWORD=<senha_do_knox>

### <a name="intra-cluster-authentication"></a>Autenticação dentro do cluster

Após a implantação do cluster, vários logons do SQL são criados:

* É criado um logon especial do SQL na instância de SQL do Controlador que é gerenciada pelo sistema, com a função sysadmin. A senha para esse logon é capturada como um segredo K8s.

* Um logon sysadmin é criado em todas as instâncias do SQL no cluster que são de propriedade e gerenciadas por esse Controlador. Ele é necessário para que o Controlador execute tarefas administrativas, como a configuração ou atualização da HA, nessas instâncias. Esses logons também são usados para a comunicação dentro do cluster entre instâncias do SQL, como a instância mestre do SQL que se comunica com um pool de dados.

> [!NOTE]
> Na versão atual, há suporte apenas para a autenticação Básica. O controle de acesso refinado para objetos do HDFS e pools de dados e de computação de cluster de Big Data do SQL ainda não estão disponíveis.

## <a name="intra-cluster-communication"></a>Comunicação dentro do cluster

A comunicação com serviços não SQL no cluster de Big Data, como do Livy com o Spark ou do Spark com o pool de armazenamento, é protegida usando certificados. Toda a comunicação do SQL Server com o SQL Server é protegida usando logons do SQL.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], consulte os seguintes recursos:

- [O que [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]são?](big-data-cluster-overview.md)
- [Workshop: Arquitetura [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
