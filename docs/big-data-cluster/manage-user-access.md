---
title: Gerenciar o acesso ao cluster de Big Data no modo do Active Directory
description: Gerenciar o acesso ao cluster de Big Data
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/04/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ef2df0bec343d73de90a43e411da92530c3c50c8
ms.sourcegitcommit: 6ab28d954f3a63168463321a8bc6ecced099b247
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87790259"
---
# <a name="manage-big-data-cluster-access-in-active-directory-mode"></a>Gerenciar o acesso ao cluster de Big Data no modo do Active Directory

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo descreve como adicionar novos grupos do Active Directory com funções *bdcUser*, além daqueles fornecidos durante a implantação por meio da definição de configuração *clusterUsers*.

>[!IMPORTANT]
>Não use esse procedimento para adicionar novos grupos do Active Directory com a função *bdcAdmin*. Os componentes do Hadoop, como HDFS e Spark, permitem apenas um grupo do Active Directory como o grupo de superusuários – o equivalente à função *bdcAdmin* no BDC. Para conceder grupos adicionais do Active Directory com permissões de *bdcAdmin* ao cluster de Big Data após a implantação, adicione outros usuários e grupos aos grupos já nomeados durante a implantação. Você pode seguir o mesmo procedimento para atualizar a associação do grupo que tem a função *bdcUsers*.

## <a name="two-overarching-roles-in-the-big-data-cluster"></a>Duas funções abrangentes no cluster de Big Data

Os grupos do Active Directory podem ser fornecidos na seção segurança do perfil de implantação como parte de duas funções abrangentes para autorização dentro do cluster de Big Data:

* `clusterAdmins`: Este parâmetro usa um grupo do Active Directory. Os membros desse grupo têm a função *bdcAdmin*, o que significa que eles obtêm permissões de administrador para todo o cluster. Eles têm permissões de *sysadmin* no SQL Server, permissões de *superusuário* no HDFS (Sistema de Arquivos Distribuído Hadoop) e no Spark e direitos de *administrador* no controlador.

* `clusterUsers`: Esses grupos do Active Directory são mapeados para a função *bdcUsers* no BDC. Eles são usuários regulares, sem permissões de administrador no cluster. Eles têm permissões para fazer logon na instância mestra do SQL Server, mas, por padrão, não têm permissões para objetos ou dados. Eles são usuários regulares do HDFS e Spark, sem permissões de *superusuário*. Ao se conectarem ao ponto de extremidade do controlador, esses usuários podem consultar apenas os pontos de extremidade (usando *azdata bdc endpoints list*).

Para conceder permissões de *bdcUser* a grupos adicionais do Active Directory sem alterar as associações de grupo dentro do Active Directory, conclua os procedimentos nas próximas seções.

## <a name="grant-bdcuser-permissions-to-additional-active-directory-groups"></a>Conceder permissões de *bdcUser* a grupos adicionais do Active Directory

### <a name="create-a-login-for-the-active-directory-user-or-group-in-the-sql-server-master-instance"></a>Criar um logon para o usuário ou grupo do Active Directory na instância mestra do SQL Server

1. Conecte-se ao ponto de extremidade mestre do SQL usando seu cliente SQL favorito. Use qualquer logon de administrador (por exemplo, `AZDATA_USERNAME`, que foi fornecido durante a implantação). Como alternativa, pode ser qualquer conta do Active Directory que pertença ao grupo do Active Directory fornecido como `clusterAdmins` na configuração de segurança.

1. Para criar um logon para o usuário ou grupo do Active Directory, execute o seguinte comando TSQL:

   ```sql
   CREATE LOGIN [<domain>\<principal>] FROM WINDOWS;
   ```

   Conceda as permissões desejadas na instância do SQL Server:

   ```sql
   ALTER SERVER ROLE <server role> ADD MEMBER [<domain>\<principal>];
   GO
   ```

Confira uma lista completa de funções de servidor no tópico de segurança do SQL Server correspondente [aqui](../relational-databases/security/authentication-access/server-level-roles.md).

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

1. Use a conexão anterior para inserir uma nova linha nas tabelas *roles* e *active_directory_principals*. Digite o valor *REALM* em letras maiúsculas.

   ```sql
   USE controller;
   GO

   INSERT INTO [controller].[auth].[roles] VALUES (N'<user or group name>@<REALM>', 'bdcUser')
   GO

   INSERT INTO [controller].[auth].[active_directory_principals] VALUES (N'<user or group name>@<REALM>', N'<SID>')
   GO
   ```

   Para encontrar o SID do usuário ou grupo que está sendo adicionado, você pode usar os comandos do PowerShell [Get-ADUser](/powershell/module/addsadministration/get-aduser/) ou [Get-ADGroup](/powershell/module/addsadministration/get-adgroup/).

2. Verifique se os membros do grupo que você adicionou têm as permissões de *bdcUser* esperadas fazendo login no ponto de extremidade do controlador ou autenticação na instância mestra do SQL Server. Por exemplo:

   ```bash
   azdata login
   azdata bdc endpoints list
   ```

## <a name="next-steps"></a>Próximas etapas

- [Conceitos de segurança para Clusters de Big Data do SQL Server 2019](concept-security.md)
