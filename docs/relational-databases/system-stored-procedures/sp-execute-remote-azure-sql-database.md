---
title: sp_execute_remote (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sp_execute_remote
- sp_execute_remote_TSQL
helpviewer_keywords:
- remote execution
- queries, remote execution
ms.assetid: ca89aa4c-c4c1-4c46-8515-a6754667b3e5
caps.latest.revision: 17
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: d681bdeafa6fc39a01a41f067bf9cec7a809add6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spexecuteremote-azure-sql-database"></a>sp_execute_remote (banco de dados do SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Executa um [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução em um único remoto Azure SQL Database ou um conjunto de bancos de dados que serve como fragmentos em um esquema de particionamento horizontal.  
  
 O procedimento armazenado é parte do recurso de consulta Elástico.  Consulte [visão geral de consulta de banco de dados Elástico de banco de dados do Azure SQL](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/) e [consultas de banco de dados Elástico de fragmentação (particionamento horizontal)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-horizontal-partitioning/).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ @data_source_name =] *datasourcename*  
 Identifica a fonte de dados externa em que a instrução é executada. Consulte [criar fonte de dados externa &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md). Fonte de dados externa pode ser do tipo "RDBMS" ou "SHARD_MAP_MANAGER".  
  
 [ @stmt=] *instrução*  
 É uma cadeia de caracteres Unicode que contém um [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução ou lote. @stmt deve ser uma constante Unicode ou uma variável Unicode. Mais expressões Unicode complexas, como concatenar duas cadeias de caracteres com o operador +, não são permitidas. Constantes de caracteres não são permitidas. Se uma constante Unicode for especificada, ele deve ser prefixado com um **N**. Por exemplo, a constante Unicode **n' sp_who'** é válido, mas a constante de caractere **'sp_who'** não é. O tamanho da cadeia de caracteres é limitado apenas pela memória disponível do servidor de banco de dados. Em servidores de 64 bits, o tamanho da cadeia de caracteres é limitado a 2 GB, o tamanho máximo de **nvarchar (max)**.  
  
> [!NOTE]  
>  @stmt pode conter parâmetros com a mesma forma que um nome de variável, por exemplo: `N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 Cada parâmetro incluído em @stmt deve ter uma entrada correspondente na lista de definições de parâmetro @params e na lista de valores de parâmetro.  
  
 [ @params=] N'@*parameter_name * * data_type* [,... *n* ] '  
 É uma cadeia de caracteres que contém as definições de todos os parâmetros inseridos em @stmt. A cadeia de caracteres deve ser uma constante Unicode ou uma variável Unicode. Cada definição de parâmetro consiste em um nome de parâmetro e um tipo de dados. *n* é um espaço reservado que indica definições de parâmetro adicionais. Todo parâmetro especificado em @stmtmust ser definido em @params. Se a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] ou lote em @stmt não contiverem parâmetros, @params não será necessário. O valor padrão para este parâmetro é NULL.  
  
 [ @param1=] '*value1*'  
 É um valor para o primeiro parâmetro definido na cadeia de caracteres de parâmetro. O valor pode ser uma constante Unicode ou uma variável Unicode. Deve haver um valor de parâmetro fornecido para cada parâmetro incluído em @stmt. Os valores não são necessários quando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] ou lote em @stmt não tiver nenhum parâmetro.  
  
 *n*  
 É um espaço reservado aos valores de parâmetros adicionais. Os valores só podem ser constantes ou variáveis. Os valores não podem ser expressões mais complexas, como funções ou expressões construídas usando os operadores.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou não zero (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna o conjunto de resultados da primeira instrução SQL.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `ALTER ANY EXTERNAL DATA SOURCE`.  
  
## <a name="remarks"></a>Remarks  
 `sp_execute_remote` parâmetros devem ser inseridos na ordem específica, conforme descrito na seção de sintaxe acima. Se os parâmetros forem inseridos na ordem incorreta, uma mensagem de erro será exibida.  
  
 `sp_execute_remote` tem o mesmo comportamento que [EXECUTE &#40;Transact-SQL&#41; ](../../t-sql/language-elements/execute-transact-sql.md) em relação a lotes e o escopo de nomes. A instrução Transact-SQL ou lote no sp_execute_remote *@stmt* parâmetro não é compilado até que a instrução sp_execute_remote seja executada.  
  
 `sp_execute_remote` Adiciona uma coluna adicional para o conjunto de resultados chamado '$ShardName' que contém o nome do banco de dados remoto que gerou a linha.  
  
 `sp_execute_remote` pode ser usado como [sp_executesql &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
### <a name="simple-example"></a>Exemplo simples  
 O exemplo a seguir cria e executa uma instrução SELECT simples no banco de dados remoto.  
  
```sql  
EXEC sp_execute_remote  
    N'MyExtSrc',  
    N'SELECT COUNT(w_id) AS Count_id FROM warehouse'   
```  
  
### <a name="example-with-multiple-parameters"></a>Exemplo com vários parâmetros  
Crie uma credencial no escopo do banco de dados em um banco de dados de usuário, especificando as credenciais de administrador para o banco de dados mestre. Crie uma fonte de dados externa apontando para o banco de dados mestre e especificar a credencial no escopo do banco de dados. Em seguida, executa a seguir, o exemplo no banco de dados de usuário, o `sp_set_firewall_rule` procedimento no banco de dados mestre. O `sp_set_firewall_rule` procedimento requer 3 parâmetros e requer o `@name` parâmetro como Unicode.

```
EXEC sp_execute_remote @data_source_name  = N'PointToMaster', 
@stmt = N'sp_set_firewall_rule @name, @start_ip_address, @end_ip_address', 
@params = N'@name nvarchar(128), @start_ip_address varchar(50), @end_ip_address varchar(50)',
@name = N'TempFWRule', @start_ip_address = '0.0.0.2', @end_ip_address = '0.0.0.2';
```

## <a name="see-also"></a>Consulte Também:

[CRIAR BANCO DE DADOS NO ESCOPO CREDENCIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
[CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
    
