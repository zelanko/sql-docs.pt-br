---
description: sp_execute_remote (Banco de Dados SQL do Azure)
title: sp_execute_remote (banco de dados SQL do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sp_execute_remote
- sp_execute_remote_TSQL
helpviewer_keywords:
- remote execution
- queries, remote execution
ms.assetid: ca89aa4c-c4c1-4c46-8515-a6754667b3e5
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1fbd97400ced46a70026b832ad4721d9f33cf690
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543429"
---
# <a name="sp_execute_remote-azure-sql-database"></a>sp_execute_remote (Banco de Dados SQL do Azure)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Executa uma [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução em um único banco de dados SQL do Azure remoto ou em um conjunto de bancos de dados que serve como fragmentos em um esquema de particionamento horizontal.  
  
 O procedimento armazenado faz parte do recurso de consulta elástica.  Consulte Visão geral de consulta de banco de dados [elástico do banco de dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/) e [consultas de banco de dados elástico para fragmentação (particionamento horizontal)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-horizontal-partitioning/).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_execute_remote [ @data_source_name = ] datasourcename  
[ , @stmt = ] statement  
[   
  { , [ @params = ] N'@parameter_name data_type [,...n ]' }   
     { , [ @param1 = ] 'value1' [ ,...n ] }  
]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ \@ data_source_name =] *DataSourceName*  
 Identifica a fonte de dados externa em que a instrução é executada. Consulte [criar fonte de dados externa &#40;&#41;Transact-SQL ](../../t-sql/statements/create-external-data-source-transact-sql.md). A fonte de dados externa pode ser do tipo "RDBMS" ou "SHARD_MAP_MANAGER".  
  
 \@ *instrução* [stmt =]  
 É uma cadeia de caracteres Unicode que contém uma [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução ou um lote. \@stmt deve ser uma constante Unicode ou uma variável Unicode. Mais expressões Unicode complexas, como concatenar duas cadeias de caracteres com o operador +, não são permitidas. Constantes de caracteres não são permitidas. Se uma constante Unicode for especificada, ela deverá ser prefixada com um **N**. Por exemplo, a constante Unicode **N ' sp_who '** é válida, mas a constante de caractere **' sp_who '** não é. O tamanho da cadeia de caracteres é limitado apenas pela memória disponível do servidor de banco de dados. Em servidores de 64 bits, o tamanho da cadeia de caracteres é limitado a 2 GB, o tamanho máximo de **nvarchar (max)**.  
  
> [!NOTE]  
>  \@stmt pode conter parâmetros com a mesma forma que um nome de variável, por exemplo: `N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 Cada parâmetro incluído em \@ stmt deve ter uma entrada correspondente na lista de \@ definições de parâmetro params e na lista de valores de parâmetro.  
  
 [ \@ params =] N ' \@ *parameter_name * * data_type* [,... *n* ] '  
 É uma cadeia de caracteres que contém as definições de todos os parâmetros que foram inseridos em \@ stmt. A cadeia de caracteres deve ser uma constante Unicode ou uma variável Unicode. Cada definição de parâmetro consiste em um nome de parâmetro e um tipo de dados. *n* é um espaço reservado que indica definições de parâmetros adicionais. Cada parâmetro especificado em \@ stmtmust ser definido em \@ params. Se a [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução ou o lote em \@ stmt não contiver parâmetros, \@ params não será necessário. O valor padrão para este parâmetro é NULL.  
  
 [ \@ param1 =] '*value1*'  
 É um valor para o primeiro parâmetro definido na cadeia de caracteres de parâmetro. O valor pode ser uma constante Unicode ou uma variável Unicode. Deve haver um valor de parâmetro fornecido para cada parâmetro incluído em \@ stmt. Os valores não são necessários quando a [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução ou o lote em \@ stmt não tem parâmetros.  
  
 *n*  
 É um espaço reservado aos valores de parâmetros adicionais. Os valores só podem ser constantes ou variáveis. Os valores não podem ser expressões mais complexas, como funções ou expressões construídas usando os operadores.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou não zero (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna o conjunto de resultados da primeira instrução SQL.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `ALTER ANY EXTERNAL DATA SOURCE`.  
  
## <a name="remarks"></a>Comentários  
 `sp_execute_remote` os parâmetros devem ser inseridos na ordem específica, conforme descrito na seção sintaxe acima. Se os parâmetros forem inseridos na ordem incorreta, uma mensagem de erro será exibida.  
  
 `sp_execute_remote` tem o mesmo comportamento que [executar &#40;&#41;Transact-SQL ](../../t-sql/language-elements/execute-transact-sql.md) com relação a lotes e o escopo de nomes. A instrução Transact-SQL ou o lote no parâmetro sp_execute_remote * \@ stmt* não é compilado até que a instrução sp_execute_remote seja executada.  
  
 `sp_execute_remote` Adiciona uma coluna adicional ao conjunto de resultados denominado ' $ShardName ' que contém o nome do banco de dados remoto que produziu a linha.  
  
 `sp_execute_remote` pode ser usado como [sp_executesql &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
### <a name="simple-example"></a>Exemplo simples  
 O exemplo a seguir cria e executa uma instrução SELECT simples em um banco de dados remoto.  
  
```sql  
EXEC sp_execute_remote  
    N'MyExtSrc',  
    N'SELECT COUNT(w_id) AS Count_id FROM warehouse'   
```  
  
### <a name="example-with-multiple-parameters"></a>Exemplo com vários parâmetros  
Crie uma credencial no escopo do banco de dados em um banco de dados de usuário, especificando credenciais de administrador para o banco de dados mestre. Crie uma fonte de dados externa apontando para o banco de dados mestre e especificando a credencial no escopo do banco de dado. Em seguida, o exemplo a seguir, no banco de dados do usuário, executa o `sp_set_firewall_rule` procedimento no banco de dados mestre. O `sp_set_firewall_rule` procedimento requer 3 parâmetros e requer que o `@name` parâmetro seja Unicode.

```
EXEC sp_execute_remote @data_source_name  = N'PointToMaster', 
@stmt = N'sp_set_firewall_rule @name, @start_ip_address, @end_ip_address', 
@params = N'@name nvarchar(128), @start_ip_address varchar(50), @end_ip_address varchar(50)',
@name = N'TempFWRule', @start_ip_address = '0.0.0.2', @end_ip_address = '0.0.0.2';
```

## <a name="see-also"></a>Consulte Também:

[CRIAR UMA CREDENCIAL NO ESCOPO DO BANCO DE DADOS](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
[CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
    
