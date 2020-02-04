---
title: Conceder permissões para scripts
description: Como conceder permissões de usuário de banco de dados para a execução de script R e Python nos Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9b8d3ea5c52c5c18f09097322fdc1e1b2321494e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727311"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>Conceder aos usuários permissão nos Serviços de Machine Learning do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve como conceder aos usuários permissão para executar scripts externos nos Serviços de Machine Learning do SQL Server e conceder permissões de leitura, gravação ou DDL (linguagem de definição de dados) em bancos de dados.

Para obter mais informações, confira a seção de permissões em [Visão geral de segurança da estrutura de extensibilidade](../../advanced-analytics/concepts/security.md#permissions).

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>Permissão para executar scripts

Se você instalou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por conta própria e está executando scripts R ou Python em sua própria instância, normalmente, você executa scripts como administrador. Portanto, você tem permissão implícita em várias operações e todos os dados no banco de dados.

No entanto, a maioria dos usuários não tem essas permissões elevadas. Por exemplo, os usuários de uma organização que usam logons do SQL para acessar o banco de dados geralmente não têm permissões elevadas. Portanto, para cada usuário que está usando o R ou o Python, você deve conceder aos usuários dos Serviços de Machine Learning a permissão para executar scripts externos em cada banco de dados em que a linguagem é usada. Veja como:

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> As permissões não são específicas da linguagem de script compatível. Em outras palavras, não há níveis de permissão separados para o script R versus o script Python. Caso você precise manter permissões separadas para essas linguagens, instale o R e o Python em instâncias separadas.

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Conceder permissões de banco de dados

Enquanto um usuário está executando scripts, talvez ele precise ler dados de outros bancos de dados. O usuário também pode precisar criar tabelas para armazenar os resultados e gravar dados nas tabelas.

Para cada conta de usuário do Windows ou logon do SQL que está executando scripts R ou Python, verifique se ele tem as permissões apropriadas no banco de dados específico: `db_datareader` para ler dados, `db_datawriter` para salvar objetos no banco de dados ou `db_ddladmin` para criar objetos como procedimentos armazenados ou tabelas que contêm dados treinados e serializados.

Por exemplo, a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir concede ao logon SQL *MySQLLogin* os direitos para executar consultas T-SQL no banco de dados *ML_Samples*. Para executar essa instrução, o logon SQL já deve existir no contexto de segurança do servidor.

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre as permissões incluídas em cada função, confira [Funções em nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md).