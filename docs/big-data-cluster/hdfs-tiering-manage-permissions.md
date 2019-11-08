---
title: Permissões de camadas do HDFS para Clusters de Big Data do SQL Server
titleSuffix: Manage HDFS tiering permissions for SQL Server Big Data Clusters
description: Gerenciar a segurança para a camada do HDFS em Clusters de Big Data do SQL Server, como permissões em outros sistemas baseados em Linux.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 758338618a312d8efe92503581ae82d49d353e51
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531969"
---
# <a name="manage-hdfs-permissions-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Gerenciar permissões do HDFS para [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O HDFS como um sistema de arquivos é semelhante aos sistemas de arquivos baseados em Linux que usam POSIX para permissões de arquivo. Além do modelo de permissões POSIX tradicional, o HDFS também dá suporte a ACLs (listas de controle de acesso) do POSIX. Para obter mais informações, confira o artigo [Apache Hadoop sobre ACLs](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_.28Access_Control_Lists.29).

As seções a seguir apresentam exemplos de como usar a CLI do `azdata` para gerenciar permissões de arquivo e diretório do HDFS.

## <a name="prerequisites"></a>Prerequisites

- [Cluster de Big Data implantado](deployment-guidance.md)
- [Ferramentas de Big Data](deploy-big-data-tools.md)
  
## <a name="hdfs-shell"></a>Shell do HDFS

A funcionalidade de shell do `hdfs` no `azdata` permite emitir comandos diretamente em um shell para gerenciar permissões de HDFS em arquivos e diretórios. O mecanismo subjacente usa chamadas WebHdfs para emitir os comandos

O comando a seguir abrirá o shell.

```bash
azdata bdc hdfs shell
```

Para acessar a ajuda para o shell `hdfs` e entender como emitir comandos, execute o comando a seguir quando o shell estiver ativo.

```bash
[hdfs] ?
```

O exemplo a seguir mostra como criar um diretório, listar diretórios e modificar permissões em um diretório e atribuir a um usuário nomeado `bob` acesso de leitura, gravação e execução ao diretório `sales`.

```bash
[hdfs] mkdir sales
[hdfs] ls
rwxr-xr-x  hdfs bdcadmins        0 Oct 09 18:02 system/
rwxrwxr-x admin bdcadmins        0 Oct 10 16:47 sales/
--xrwxrwxrwx  hdfs bdcadmins        0 Oct 09 18:03 tmp/
rwxrwxrwx  hdfs bdcadmins        0 Oct 09 17:59 user/

[hdfs] acl modify  '/sales/' 'user:bob:rwx'
acl modify: Change completed.
[hdfs] acl status  '/sales/'
{
  `AclStatus`: {
    `entries`: [
      `user:bob:rwx`,
      `group::r-x`
    ],
    `group`: `bdcadmins`,
    `owner`: `admin`,
    `permission`: `775`,
    `stickyBit`: false
  }
}
```

## <a name="create-a-directory-in-hdfs-using-azdata"></a>Criar um diretório no HDFS usando `azdata`

Crie um diretório chamado `data` no caminho `/sales`.

```bash
azdata bdc hdfs mkdir --path '/sales/data'
```

## <a name="change-owner-of-a-directory-or-file"></a>Alterar o proprietário de um diretório ou arquivo

Altere o usuário proprietário do diretório `data` no HDFS e torne *`alice`* o usuário proprietário e *`salesgroup`* , o grupo proprietário. Para alterar o proprietário, você precisa ser um proprietário.

```bash
azdata bdc hdfs chown --owner alice --group 'salesgroup' --path '/sales/data'
```

## <a name="change-permissions-of-a-file-or-directory-with-chmod"></a>Alterar as permissões de um arquivo ou diretório com `chmod`

Use `chmod` para alterar permissões em arquivos e diretórios (para proprietário, grupo proprietário e outros). Para obter mais informações, confira [como alterar permissões em um sistema de arquivos do Linux](https://www.lifewire.com/uses-of-command-chmod-2201064). No hdfs, o padrão é o mesmo. Por exemplo:

```bash
azdata bdc hdfs chmod --permission 750 --path /sales/data
```

```bash
azdata bdc hdfs chmod --permission 775 --path /sales/data/file.txt
```

## <a name="set-sticky-bit-on-directories"></a>Definir bit persistente em diretórios

Definir o recipiente de bit persistente nos diretórios para impedir a exclusão ou a relocação não intencional de arquivos. O bit persistente limita a permissão para excluir ou mover um arquivo para o superusuário, o proprietário do diretório ou o proprietário do arquivo. Esta configuração não afeta o arquivo. O exemplo abaixo define um bit persistente no diretório `users` prefixando as permissões com um `1`.

```bash
azdata bdc hdfs chmod --path /sales/users --permission 1750
```

## <a name="setting-acls-on-files-and-directories"></a>Como configurar ACLs em arquivos e diretórios

Para definir ACLs em arquivos e diretórios no HDFS, use os comandos `azdata`.

Definir ACLs em um diretório e fornecer ao usuário nomeado *`tom`* acesso para ler, gravar e executar ao diretório *`data`* . 

> [!NOTE]
> Ao usar o comando `set`, verifique se você está fornecendo a especificação da ACL completa, incluindo a especificação da ACL para o usuário proprietário, o grupo proprietário e outros.

```bash
azdata bdc hdfs acl set --path '/sales' --aclspec  'user::rw-,user:tom:rwx,group::rw-,other::rw-'
```

## <a name="default-acl-on-directories"></a>ACL padrão em diretórios

A ACL padrão permite que os subdiretórios herdem as permissões do diretório pai. Somente diretórios podem ter uma ACL padrão. Quando um novo arquivo ou subdiretório é criado, ele herda automaticamente a ACL padrão de seu pai para a própria ACL de acesso. Dessa forma, a ACL padrão será herdada por níveis de diretório arbitrariamente profundo à medida que novos subdiretórios forem criados.

Veja abaixo um exemplo de como definir a ACL padrão usando azdata.

```bash
azdata bdc hdfs acl set --path '/sale' --aclspec  'user::rw-,user:tom:rwx,group::rw-,other::rw-,default:group::rw-,default:user::rw-,default:other::rw-'
```

## <a name="next-steps"></a>Próximas etapas

- [Referência de `azdata`](reference-azdata.md)

- [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
