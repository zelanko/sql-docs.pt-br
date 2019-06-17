---
title: Restrições de recursos | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: vainolo
ms.author: arib
manager: tomerw
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 99a0a768334ab5335591fae69e4f18060fba9866
ms.sourcegitcommit: 561cee96844b82ade6cf543a228028ad5c310768
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66506914"
---
# <a name="feature-restrictions"></a>Restrições de recursos

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Uma fonte comum de ataques de SQL Server são aplicativos Web que acessam o banco de dados em que as várias formas de ataques de injeção de SQL são usadas para reunir informações sobre o banco de dados.  O ideal é que o código do aplicativo seja desenvolvido de modo a não permitir injeção de SQL.  No entanto, em grandes-bases de código que incluem código herdado e externo, nunca podemos ter certeza de que todos os casos foram resolvidos, portanto, injeções de SQL são um fato da vida contra o qual precisamos nos proteger.  A meta das restrições de recursos é prevenir que algumas formas de injeção de SQL vazem informações sobre o banco de dados, mesmo quando a injeção de SQL é bem-sucedida.

## <a name="enabling-feature-restrictions"></a>Habilitar restrições de recursos

A habilitação de restrições de recursos é feita usando o procedimento armazenado `sp_add_feature_restriction` da seguinte maneira:

```sql
EXEC sp_add_feature_restriction <feature>, <object_class>, <object_name>
```

Os recursos a seguir podem ser restritos:

| Recurso          | Descrição |
|------------------|-------------|
| N'ErrorMessages' | Quando restrito, qualquer dado de usuário dentro da mensagem de erro será mascarado. Veja [Restrição de recursos de mensagens de erro](#error-messages-feature-restriction) |
| N'Waitfor'       | Quando a restrito, o comando retornará imediatamente sem nenhum atraso. Veja [Restrição de recurso WAITFOR](#waitfor-feature-restriction) |

O valor de `object_class` pode ser `N'User'` ou `N'Role'` para indicar se `object_name` é um nome de Usuário ou um nome de Função no banco de dados.

O exemplo a seguir fará com que todas as mensagens de erro para o usuário `MyUser` sejam mascaradas:

```sql
EXEC sp_add_feature_restriction N'ErrorMessages', N'User', N'MyUser'
```

## <a name="disabling-feature-restrictions"></a>Desabilitar restrições de recursos

A desabilitação de restrições de recursos é feita usando o procedimento armazenado `sp_drop_feature_restriction` da seguinte maneira:

```sql
EXEC sp_drop_feature_restriction <feature>, <object_class>, <object_name>
```

O exemplo a seguir desabilita o mascaramento de mensagem de erro para o usuário `MyUser`:

```sql
EXEC sp_drop_feature_restriction N'ErrorMessages', N'User', N'MyUser'
```

## <a name="viewing-feature-restrictions"></a>Exibir restrições de recursos

A exibição `sys.sql_feature_restrictions` apresenta todas as restrições de recurso definidas no momento no banco de dados. Veja [sys.sql_feature_restrictions](../system-catalog-views/sys-sql-feature-restrictions.md) para informações sobre o modo.

## <a name="feature-restrictions"></a>Restrições de recursos

### <a name="error-messages-feature-restriction"></a>Restrição de recursos de mensagens de erro

Um método comum de ataque de injeção de SQL é injetar o código que causa um erro.  Ao examinar a mensagem de erro, um invasor pode obter informações sobre o sistema, permitindo ataques adicionais mais direcionados.  Esse ataque pode ser especialmente útil quando o aplicativo não exibe os resultados de uma consulta, mas exibe mensagens de erro.

Considere um aplicativo Web que tenha uma solicitação na forma de:

```html
http://www.contoso.com/employee.php?id=1
```

Que executa a consulta de banco de dados a seguir:

```sql
SELECT Name FROM EMPLOYEES WHERE Id=$EmpId
```

Se o valor passado como o parâmetro `Id` para a solicitação de aplicativo Web for copiado para substituir $EmpId na consulta de banco de dados, um invasor poderá fazer a solicitação a seguir:

```html
http://www.contoso.com/employee.php?id=1 AND CAST(DB_NAME() AS INT)=0
```

E o seguinte erro será retornado, permitindo que o invasor saber o nome do banco de dados:

```sql
Conversion failed when converting the nvarchar value 'HR_Data' to data type int.
```

Depois de habilitar restrição de recurso de mensagens de erro para o usuário do aplicativo no banco de dados, a mensagem de erro retornada é mascarada, de modo que nenhuma informação interna sobre o banco de dados vaze:

```sql
Conversion failed when converting the ****** value '******' to data type ******.
```

De modo similar, o invasor poderia fazer a solicitação a seguir:

```html
http://www.contoso.com/employee.php?id=1 AND CAST(Salary AS TINYINT)=0
```

E o seguinte erro será retornado, permitindo que o invasor saber o salário do funcionário:

```sql
Arithmetic overflow error for data type tinyint, value = 140000.
```

Usando a restrição de recurso de mensagens de erro, o banco de dados retornaria:

```sql
Arithmetic overflow error for data type ******, value = ******.
```

### <a name="waitfor-feature-restriction"></a>Restrição de recurso WAITFOR

Uma injeção de SQL cega é quando um aplicativo não fornece ao invasor os resultados do SQL injetado ou uma mensagem de erro, mas o invasor pode deduzir as informações do banco de dados criando uma consulta condicional na qual duas ramificações condicionais levam uma quantidade diferente de tempo para serem executadas. Comparando o tempo de resposta, o invasor pode saber qual branch foi executado e, portanto, obter informações sobre o sistema. A variante mais simples desse ataque é usar a instrução `WAITFOR` para introduzir o atraso.

Considere um aplicativo Web que tenha uma solicitação na forma de:

```html
http://www.contoso.com/employee.php?id=1
```

que executa a consulta de banco de dados a seguir:

```sql
SELECT Name FROM EMPLOYEES WHERE Id=$EmpId
```

Se o valor passado como o parâmetro `Id` para as solicitações de aplicativo Web for copiado para substituir $EmpId na consulta de banco de dados, um invasor poderá fazer a solicitação a seguir:

```html
http://www.contoso.com/employee.php?id=1; IF SYSTEM_USER='sa' WAITFOR DELAY '00:00:05'
```

E a consulta levaria 5 segundos adicionais se a conta `sa` estivesse sendo usada. Se a restrição de recurso `WAITFOR` estiver desabilitada no banco de dados, a instrução `WAITFOR` será ignorada e nenhuma informação será vazada usando esse ataque.
