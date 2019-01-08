---
title: Conceitos de segurança
titleSuffix: SQL Server 2019 big data clusters
description: Este artigo descreve conceitos de segurança para o cluster de big data de 2019 do SQL Server (versão prévia). Isso inclui descrevendo os pontos de extremidade do cluster e autenticação do cluster.
author: nelgson
ms.author: negust
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: d4da38df828b2859de07a7676fc5070bcecf6329
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030570"
---
# <a name="security-concepts-for-sql-server-big-data-clusters"></a>Conceitos de segurança para clusters de grandes dados do SQL Server

Um cluster de big data seguro implica suporte consistente e coerente para cenários de autenticação e autorização, entre o SQL Server e o HDFS/Spark. A autenticação é o processo de verificação da identidade de um usuário ou serviço e garantir que eles são quem eles são afirmando ser. Autorização refere-se para conceder ou negar o acesso a recursos específicos com base na identidade do usuário solicitante. Esta etapa é executada depois que um usuário é identificado por meio da autenticação.

Autorização no contexto de Big Data geralmente é feita por meio de listas de controle de acesso (ACLs) que associam identidades de usuário com permissões específicas. HDFS dá suporte a autorização, limitando o acesso a APIs do serviço, arquivos HDFS e execução do trabalho.

Este artigo abordará os principais conceitos relacionados à segurança no cluster de big data.

## <a name="cluster-endpoints"></a>Pontos de extremidade do cluster

Há três pontos de entrada para o cluster de big data

* Gateway HDFS/Spark (Knox) – isso é um ponto de extremidade com base em HTTPS. Outros pontos de extremidade são transmitidas por proxy por meio deste. Gateway HDFS/Spark é usado para acessar serviços como o webHDFS e Livy. Sempre que você veja referências a Knox, esse é o ponto de extremidade.

* Ponto de extremidade controlador - serviço de gerenciamento de cluster de big data que expõe as APIs REST para gerenciar o cluster. Algumas ferramentas, como o portal de administração, também são acessadas por meio desse ponto de extremidade.

* Instância mestre - ponto de extremidade TDS para ferramentas de banco de dados e aplicativos para se conectar à instância mestre do SQL Server no cluster.

![Pontos de extremidade do cluster](media/concept-security/cluster_endpoints.png)

Atualmente, não há nenhuma opção de abrir portas adicionais para acessar o cluster de fora.

### <a name="how-endpoints-are-secured"></a>Como os pontos de extremidade são protegidos

Proteger os pontos de extremidade no cluster de big data é feito utilizando senhas que podem ser conjunto/atualizada usando variáveis de ambiente ou comandos da CLI. Todas as senhas interno do cluster são armazenadas como segredos do Kubernetes.  

## <a name="authentication"></a>Autenticação

Após o provisionamento do cluster, um número de logons é criado.

Alguns desses logons são para os serviços se comunicam entre si e outros são para os usuários finais acessem o cluster.

### <a name="end-user-authentication"></a>Autenticação do usuário final
Após o provisionamento do cluster, um número de senhas do usuário final precisa ser definido usando variáveis de ambiente. Estas são as senhas que os administradores do SQL e os administradores de cluster usam para acessar serviços:

Nome de usuário do controlador:
 + CONTROLLER_USERNAME = < controller_username >

Senha do controlador:  
 + CONTROLLER_PASSWORD = < controller_password >

Senha de SA do SQL Master: 
 + MSSQL_SA_PASSWORD = < controller_sa_password >

Senha para acessar o ponto de extremidade HDFS/Spark:
 + KNOX_PASSWORD = < knox_password >

### <a name="intra-cluster-authentication"></a>Autenticação de dentro do cluster

Após a implantação do cluster, um número de logons do SQL Server é criado:

* Um logon SQL especial é criado na instância do SQL do controlador que é gerenciado, com a função sysadmin do sistema. A senha para esse logon é capturada como um segredo K8s.

* Um logon de sysadmin é criado em todas as instâncias do SQL no cluster, que o controlador possui e gerencia. Ele é necessário para o controlador executar tarefas administrativas, como instalação de alta disponibilidade ou atualização, nessas instâncias. Esses logons também são usados para comunicação dentro do cluster entre instâncias do SQL, como a instância mestre do SQL se comunicando com um pool de dados.

> [!NOTE]
> Na versão atual, há suporte para somente a autenticação básica. Controle de acesso refinado para objetos do HDFS e SQL grande cluster computação e dados de pools de dados, ainda não está disponível.

## <a name="intra-cluster-communication"></a>Comunicação interna do cluster

Comunicação com os serviços não-SQL dentro do cluster de big data, como o Livy Spark ou do Spark ao pool de armazenamento, é protegida usando certificados. Todos os SQL Server para comunicação do SQL Server é protegida usando logons do SQL Server.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de grandes dados do SQL Server, consulte os seguintes artigos:

- [Quais são os clusters do SQL Server 2019 grandes dados?](big-data-cluster-overview.md)
- [Guia de início rápido: Implantar um cluster de big data do SQL Server no Kubernetes](quickstart-big-data-cluster-deploy.md)
