---
title: Conceder aos usuários permissão para serviços do SQL Server Machine Learning | Microsoft Docs
description: Como fornecer aos usuários permissão para serviços do SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: ad5c3fa3bf94bb88041c9ec81773b2a26013e517
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100327"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>Conceder aos usuários permissão para serviços do SQL Server Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como você pode dar aos usuários permissão para executar scripts externos em serviços do SQL Server Machine Learning e conceder permissões de DDL (linguagem) para bancos de dados de leitura, gravação ou definição de dados.

Um logon do SQL Server ou a conta de usuário do Windows é necessário para executar scripts externos que usam dados do SQL Server ou que são executados com o SQL Server como o contexto de computação.

A conta de usuário ou logon identifica o *entidade de segurança*, que talvez seja necessário vários níveis de acesso, dependendo dos requisitos de script externo:

+ Permissão para acessar o banco de dados em que os scripts externos estão habilitados.
+ Permissões para ler dados de objetos protegidos, como tabelas.
+ A capacidade de gravar novos dados em uma tabela, como um modelo ou resultados de pontuação.
+ A capacidade de criar novos objetos, como tabelas, procedimentos armazenados que usam o script externo ou funções personalizadas do que usar o R ou o trabalho do Python.
+ O direito de instalar novos pacotes no computador do SQL Server, ou usar os pacotes fornecidos a um grupo de usuários.

Portanto, cada pessoa que executa um script externo usando o SQL Server como o contexto de execução deve ser mapeada para um usuário no banco de dados. Na segurança do SQL Server, é mais fácil de criar funções para gerenciar conjuntos de permissões e atribuir usuários a essas funções, em vez de individualmente, definir permissões de usuário.

Até mesmo usuários que estão usando o R ou Python em uma ferramenta externa devem ser mapeados para um logon ou conta no banco de dados se o usuário precisa para executar um script externo no banco de dados, ou acessar objetos de banco de dados e dados. As mesmas permissões são necessárias se o script externo é enviado de um cliente de ciência de dados remoto ou ao uso de um procedimento armazenado T-SQL.

Por exemplo, suponha que você criou um script externo que é executado no computador local, e você deseja executar esse código em SQL Server. Você deve certificar-se de que as seguintes condições sejam atendidas:

+ O banco de dados permite conexões remotas.
+ O logon SQL ou a conta do Windows que você usou para acesso ao banco de dados foi adicionada para o SQL Server no nível de instância.
+ O logon do SQL ou o usuário do Windows deve ter a permissão para executar scripts externos. Em geral, essa permissão só pode ser adicionada por um administrador de banco de dados.
+ O logon do SQL ou o usuário da janela deve ser adicionado como um usuário, com permissões apropriadas, em cada banco de dados em que o script externo executa qualquer uma dessas operações:
  + Recuperando dados.
  + Gravação ou a atualização de dados.
  + Criando novos objetos, como tabelas ou procedimentos armazenados.

Depois que o logon ou conta de usuário do Windows foi provisionada e recebeu as permissões necessárias, você pode executar um script externo no SQL Server usando um objeto de fonte de dados em R ou o **revoscalepy** biblioteca em Python ou chamando um armazenado procedimento que contém o script externo.

Sempre que um script externo é iniciado a partir do SQL Server, a segurança do mecanismo de banco de dados obtém o contexto de segurança do usuário que iniciou o trabalho e gerencia os mapeamentos do usuário ou logon para objetos protegíveis.

Portanto, todos os scripts externos que são iniciados de um cliente remoto devem especificar as informações de logon ou usuário como parte da cadeia de conexão.

<a name="permissions-external-script"></a> 

## <a name="permission-to-run-scripts"></a>Permissão para executar scripts

Se você instalou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por conta própria e você estiver executando scripts de R ou Python em sua própria instância, você normalmente executa scripts como administrador. Assim, você deve ter permissão implícita em várias operações e todos os dados no banco de dados.

A maioria dos usuários, no entanto, não tem permissões elevadas desse tipo. Por exemplo, os usuários em uma organização que usam logons do SQL Server para acessar o banco de dados geralmente não tem permissões com privilégios elevados. Portanto, para cada usuário que está usando R ou Python, você deve conceder aos usuários dos serviços de aprendizado de máquina a permissão para executar scripts externos em cada banco de dados em que o idioma será usado. Aqui está como:

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> As permissões não são específicas para a linguagem de script com suporte. Em outras palavras, não há níveis de permissão separados para o script de R em comparação com o script Python. Se você precisar manter permissões separadas para esses idiomas, instale o R e Python em instâncias separadas.

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Conceder permissões de bancos de dados

Enquanto um usuário está em execução de scripts, o usuário talvez precise ler dados de outros bancos de dados. O usuário também precisará criar novas tabelas para armazenar os resultados e gravar dados em tabelas.

Para cada conta de usuário do Windows ou logon do SQL que está executando scripts R ou Python, certifique-se de que ele tem as permissões apropriadas no banco de dados específico: `db_datareader` para ler dados, `db_datawriter` para salvar objetos de banco de dados, ou `db_ddladmin` para criar objetos como procedimentos armazenados ou tabelas que contêm treinado e os dados serializados.

Por exemplo, a seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução fornece o logon do SQL *MySQLLogin* os direitos para executar consultas do T-SQL no *ML_Samples* banco de dados. Para executar essa instrução, o logon SQL já deve existir no contexto de segurança do servidor.

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre as permissões incluídas em cada função, consulte [funções de nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md).