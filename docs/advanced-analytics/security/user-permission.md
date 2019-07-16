---
title: Conceda permissões de banco de dados para execução do script R e Python - serviços do SQL Server Machine Learning
description: Como conceder permissões de usuário de banco de dados para execução de scripts de R e Python em serviços do SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: e24095b7ec5aafd3439a3d344123c0a7f9dae86d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962322"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>Conceder aos usuários permissão para serviços do SQL Server Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como você pode dar aos usuários permissão para executar scripts externos em serviços do SQL Server Machine Learning e conceder permissões de DDL (linguagem) para bancos de dados de leitura, gravação ou definição de dados.

Para obter mais informações, consulte a seção permissões nos [visão geral de segurança para a estrutura de extensibilidade](../../advanced-analytics/concepts/security.md#permissions).

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>Permissão para executar scripts

Se você instalou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por conta própria e você estiver executando scripts de R ou Python em sua própria instância, você normalmente executa scripts como administrador. Assim, você deve ter permissão implícita em várias operações e todos os dados no banco de dados.

A maioria dos usuários, no entanto, não tem permissões elevadas desse tipo. Por exemplo, os usuários em uma organização que usam logons do SQL Server para acessar o banco de dados geralmente não tem permissões com privilégios elevados. Portanto, para cada usuário que está usando R ou Python, você deve conceder aos usuários dos serviços de aprendizado de máquina a permissão para executar scripts externos em cada banco de dados em que o idioma será usado. Veja como:

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> As permissões não são específicas para a linguagem de script com suporte. Em outras palavras, não há níveis de permissão separados para o script de R em comparação com o script Python. Se você precisar manter permissões separadas para esses idiomas, instale o R e Python em instâncias separadas.

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Conceder permissões de bancos de dados

Enquanto um usuário está em execução de scripts, o usuário talvez precise ler dados de outros bancos de dados. O usuário também precisará criar novas tabelas para armazenar os resultados e gravar dados em tabelas.

Para cada conta de usuário do Windows ou logon do SQL que está executando scripts R ou Python, certifique-se de que ele tem as permissões apropriadas no banco de dados específico: `db_datareader` para ler dados, `db_datawriter` para salvar objetos de banco de dados, ou `db_ddladmin` para criar objetos como procedimentos armazenados ou tabelas que contêm treinado e os dados serializados.

Por exemplo, a seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução fornece o logon do SQL *MySQLLogin* os direitos para executar consultas do T-SQL no *ML_Samples* banco de dados. Para executar essa instrução, o logon SQL já deve existir no contexto de segurança do servidor.

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre as permissões incluídas em cada função, consulte [funções de nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md).