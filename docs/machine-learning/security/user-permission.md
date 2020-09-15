---
title: Conceder permissões para executar scripts do Python e do R
description: Saiba como conceder aos usuários permissão para executar scripts do Python e do R externos nos Serviços de Machine Learning do SQL Server e conceder permissões de leitura, gravação ou DDL (linguagem de definição de dados) em bancos de dados.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/03/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019, contperfq4
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5c961c2c4df15fdff7b1e2f3d5b1815c50d69771
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180393"
---
# <a name="grant-users-permission-to-execute-python-and-r-scripts-with-sql-server-machine-learning-services"></a>Conceder permissão aos usuários para executar scripts do Python e do R com os Serviços de Machine Learning do SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Saiba como conceder aos usuários permissão para executar scripts do Python e do R externos nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) e conceder permissões de leitura, gravação ou DDL (linguagem de definição de dados) em bancos de dados.

Para obter mais informações, confira a seção de permissões em [Visão geral de segurança da estrutura de extensibilidade](../../machine-learning/concepts/security.md#permissions).

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>Permissão para executar scripts

Você precisará conceder permissão, a cada usuário que executa scripts do R ou do Python com os Serviços de Machine Learning do SQL Server e que não tem status de administrador, para executar scripts externos em cada banco de dados em que a linguagem é usada.

Para conceder permissão para executar o script externo, execute o seguinte script:

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> As permissões não são específicas da linguagem de script compatível. Em outras palavras, não há níveis de permissão separados para o script R versus o script Python.

<a name="permissions-db"></a>

## <a name="grant-databases-permissions"></a>Conceder permissões de banco de dados

Enquanto um usuário está executando scripts, talvez ele precise ler dados de outros bancos de dados. O usuário também pode precisar criar tabelas para armazenar os resultados e gravar dados nas tabelas.

Para cada conta de usuário do Windows ou logon do SQL que esteja executando scripts de R ou Python, verifique se as permissões apropriadas estão presentes no banco de dados específico: 

+ `db_datareader` para ler dados.
+ `db_datawriter` para salvar objetos no banco de dados.
+ `db_ddladmin` para criar objetos como procedimentos armazenados ou tabelas que contêm dados treinados e serializados.

Por exemplo, a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir concede ao logon SQL *MySQLLogin* os direitos para executar consultas T-SQL no banco de dados *ML_Samples*. Para executar essa instrução, o logon SQL já deve existir no contexto de segurança do servidor.

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre as permissões incluídas em cada função, confira [Funções em nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md).
