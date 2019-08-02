---
title: Conceder permissões de banco de dados para a execução de script R e Python
description: Como conceder permissões de usuário de banco de dados para a execução de script R e Python no SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 97e1fb6e2415e30f595d61dffa8a4952cfdc42d0
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715560"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>Conceder aos usuários permissão para SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve como você pode conceder aos usuários permissão para executar scripts externos no SQL Server Serviços de Machine Learning e conceder permissões de leitura, gravação ou linguagem de definição de dados (DDL) aos bancos de dado.

Para obter mais informações, consulte a seção permissões em [visão geral de segurança para a estrutura de extensibilidade](../../advanced-analytics/concepts/security.md#permissions).

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>Permissão para executar scripts

Se você tiver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se instalado e estiver executando scripts de R ou Python em sua própria instância, normalmente executará scripts como administrador. Portanto, você tem permissão implícita em várias operações e todos os dados no banco de dado.

No entanto, a maioria dos usuários não tem essas permissões elevadas. Por exemplo, os usuários em uma organização que usam logons do SQL para acessar o banco de dados geralmente não têm permissões elevadas. Portanto, para cada usuário que está usando R ou Python, você deve conceder aos usuários Serviços de Machine Learning a permissão para executar scripts externos em cada banco de dados em que o idioma é usado. Veja como:

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> As permissões não são específicas para a linguagem de script com suporte. Em outras palavras, não há níveis de permissão separados para script R versus script Python. Se você precisar manter permissões separadas para esses idiomas, instale R e Python em instâncias separadas.

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Permissões de conceder bancos de dados

Enquanto um usuário estiver executando scripts, talvez o usuário precise ler os dados de outros bancos. O usuário também pode precisar criar novas tabelas para armazenar os resultados e gravar dados em tabelas.

Para cada conta de usuário do Windows ou logon do SQL que esteja executando scripts de R ou Python, verifique se ele tem as permissões apropriadas no `db_datareader` banco de dados específico `db_datawriter` : para ler e salvar objetos no banco `db_ddladmin` de dado, ou para criar objetos como procedimentos armazenados ou tabelas que contêm dados treinados e serializados.

Por exemplo, a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir fornece ao logon do SQL *MySQLLogin* os direitos para executar consultas T-SQL no banco de dados *ML_Samples* . Para executar essa instrução, o logon SQL já deve existir no contexto de segurança do servidor.

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre as permissões incluídas em cada função, consulte [funções de nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md).