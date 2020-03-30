---
title: Gerenciar o acesso ao cluster de Big Data no modo do Active Directory
description: Gerenciar o acesso ao cluster de Big Data
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 12/06/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9f9cca7e761b8f8ec3f5b87e9a195a0eb8b5da6d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76259454"
---
# <a name="manage-big-data-cluster-access-in-active-directory-mode"></a>Gerenciar o acesso ao cluster de Big Data no modo do Active Directory

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como atualizar os grupos do Active Directory que são fornecidos durante a implantação para clusterAdmins e clusterUsers.

## <a name="two-overarching-roles-in-the-big-data-cluster"></a>Duas funções abrangentes no cluster de Big Data

Os grupos do Active Directory podem ser fornecidos na seção segurança do perfil de implantação como parte de duas funções abrangentes para autorização dentro do cluster de Big Data:

* `clusterAdmins`: Este parâmetro usa um grupo do Active Directory. Os membros desse grupo recebem permissões de administrador no cluster inteiro. Eles têm permissões de *sysadmin* no SQL Server, permissões de *superusuário* no HDFS (Sistema de Arquivos Distribuído Hadoop) e no Spark e direitos de *administrador* no controlador.

* `clusterUsers`: Estes grupos do Active Directory são usuários comuns sem permissões de administrador no cluster. Eles têm permissões para fazer logon na instância mestra do SQL Server, mas, por padrão, não têm permissões para objetos ou dados.

Uma maneira de conceder permissões adicionais a grupos do Active Directory ao cluster de Big Data após a implantação é acrescentar usuários e grupos adicionais aos grupos já nomeados durante a implantação. 

No entanto, talvez nem sempre seja viável para os administradores alterar as associações de grupo dentro do Active Directory. Para conceder permissões adicionais a grupos do Active Directory sem alterar as associações de grupo dentro do Active Directory, conclua os procedimentos nas próximas seções.

## <a name="grant-administrator-permissions-to-additional-active-directory-groups"></a>Conceder permissões de administrador para grupos adicionais do Active Directory

>[!IMPORTANT]
>Este procedimento não concede acesso adicional de administrador de grupos do Active Directory aos componentes do Hadoop, como HDFS e Spark, no cluster de Big Data. Esses componentes permitem apenas um grupo do Active Directory como o grupo de superusuários. Essa restrição significa que o grupo especificado em `clusterAdmins` durante a implantação permanece como grupo de superusuários mesmo após essa etapa.

Ao seguir os procedimentos nesta seção, você pode conceder acesso de administrador ao controlador e à instância mestra do SQL Server.

### <a name="create-a-login-for-the-active-directory-user-or-group-in-the-sql-server-master-instance"></a>Criar um logon para o usuário ou grupo do Active Directory na instância mestra do SQL Server 

1. Conecte-se ao ponto de extremidade mestre do SQL usando seu cliente SQL favorito. Use qualquer logon de administrador (por exemplo, `AZDATA_USERNAME`, que foi fornecido durante a implantação). Como alternativa, pode ser qualquer conta do Active Directory que pertença ao grupo do Active Directory fornecido como `clusterAdmins` na configuração de segurança.

1. Para criar um logon para o usuário ou grupo do Active Directory, execute o seguinte comando TSQL:

   ```sql
   CREATE LOGIN [<domain>\<principal>] FROM WINDOWS;
   ```

   Se você estiver concedendo permissões de administrador na instância do SQL Server, conceda também a seguinte permissão:

   ```sql
   ALTER SERVER ROLE sysadmin ADD MEMBER [<domain>\<principal>];
   GO
   ```

### <a name="add-the-active-directory-user-or-group-to-the-roles-table-in-the-controller-database"></a>Adicionar o usuário ou grupo do Active Directory à tabela de funções no banco de dados do controlador 

1. Obtenha as credenciais do SQL Server do controlador executando os seguintes comandos:

   a. Execute este comando como um administrador do Kubernetes:

   ```bash
   kubectl get secret controller-sa-secret -n <cluster name> -o yaml | grep password
   ```

   b. Decodifique o segredo em Base64:

   ```bash
   echo <password from kubectl command>  | base64 --decode && echo
   ```

1. Em uma janela de comando separada, exponha a porta do servidor de banco de dados do controlador:

   ```bash
   kubectl port-forward controldb-0 1433:1433 --address 0.0.0.0 -n <cluster name>
   ```

1. Use a conexão anterior para inserir uma linha na tabela de funções. Digite o valor *REALM* em letras maiúsculas.

   Se você estiver concedendo permissões de administrador, use a função *bdcAdmin* no *\<nome da função>* . Para usuários que não são administradores, use a função *bdcUser*.

   ```sql
   USE controller;
   GO

   INSERT INTO [controller].[auth].[roles] VALUES (N'<user or group name>@<REALM>', N'<role name>')
   GO
   ```

1. Verifique se os membros do grupo que você adicionou têm permissões de administrador de cluster de Big Data, efetuando logon no ponto de extremidade do controlador e executando o seguinte comando:

   ```bash
   azdata bdc config show
   ```

1. Para usuários que não são administradores, você pode verificar o acesso autenticando-se na instância mestra do SQL ou no controlador usando `azdata login`.

## <a name="next-steps"></a>Próximas etapas

- [Conceitos de segurança para Clusters de Big Data do SQL Server 2019](concept-security.md)
