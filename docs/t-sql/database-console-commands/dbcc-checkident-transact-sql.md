---
description: DBCC CHECKIDENT (Transact-SQL)
title: DBCC CHECKIDENT (Transact-SQL)
ms.custom: ''
ms.date: 03/07/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKIDENT
- DBCC CHECKIDENT
- CHECKIDENT_TSQL
- DBCC_CHECKIDENT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- checking identity values
- reseeding identity values
- resetting identity values
- identity values [SQL Server]
- identity values [SQL Server], checking
- modifying identity values
- current identity values
- DBCC CHECKIDENT statement
- identity values [SQL Server], reseeding
- reporting current identity values
ms.assetid: 2c00ee51-2062-4e47-8b19-d90f524c6427
author: pmasl
ms.author: umajay
monikerRange: = azuresqldb-current || >= sql-server-2016 || >= sql-server-linux-2017 || = azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: b7fd8592ed2643d25736539c91b3e3bedfdd75ea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479853"
---
# <a name="dbcc-checkident-transact-sql"></a>DBCC CHECKIDENT (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Verifica o valor de identidade atual da tabela especificada no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e, se necessário, altera o valor da identidade. Você também pode usar DBCC CHECKIDENT para definir manualmente um novo valor de identidade atual para a coluna de identidade.  
  
 ![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do artigo") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql

-- Syntax for SQL Server and Azure SQL Database  

DBCC CHECKIDENT
 (
    table_name  
        [, { NORESEED | { RESEED [, new_reseed_value ] } } ]  
)  
[ WITH NO_INFOMSGS ]  
```  

```console
-- Syntax for Azure SQL Data Warehouse
DBCC CHECKIDENT   
 (   
    table_name  
        [RESEED, new_reseed_value ]   
)  
[ WITH NO_INFOMSGS ]  

```
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

 *table_name*  
 É o nome da tabela sobre a qual verificar o valor de identidade atual. A tabela especificada deve conter uma coluna de identidade. Os nomes de tabela precisam seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md). Dois ou três nomes de parte devem ser delimitados, como 'Person.AddressType' ou [Person.AddressType].
  
 NORESEED  
 Especifica que o valor de identidade atual não deve ser alterado.  
  
 RESEED  
 Especifica que o valor de identidade atual deve ser alterado.  
  
 *new_reseed_value*  
 O novo valor a ser usado como o valor atual da coluna de identidade.  
  
 WITH NO_INFOMSGS  
 Suprime todas as mensagens informativas.  
  
## <a name="remarks"></a>Comentários

 As correções específicas feitas no valor de identidade atual dependem das especificações de parâmetro.  
  
|Comando DBCC CHECKIDENT|Correção de Identidade ou correções feitas|  
|-----------------------------|---------------------------------------------|  
|DBCC CHECKIDENT ( *table_name*, NORESEED )|Valor de identidade atual não é redefinido. DBCC CHECKIDENT retorna o valor de identidade atual e o valor máximo atual da coluna de identidade. Se os dois valores não coincidirem, redefina o valor de identidade para evitar erros em potencial ou intervalos na sequência de valores.|  
|DBCC CHECKIDENT ( *table_name* )<br /><br /> ou<br /><br /> DBCC CHECKIDENT ( *table_name*, RESEED )|Se o valor de identidade atual de uma tabela for menor que o valor de identidade máximo armazenado na coluna de identidade, ele será redefinido por meio do valor máximo na coluna de identidade. Consulte a seção de 'Exceções' a seguir.|  
|DBCC CHECKIDENT ( *table_name*, RESEED, *new_reseed_value* )|O valor atual da identidade é definido como o *new_reseed_value*. Se nenhuma linha for inserida na tabela desde sua criação, ou se todas as linhas forem removidas usando a instrução TRUNCATE TABLE, a primeira linha inserida após a execução de DBCC CHECKIDENT usará *new_reseed_value* como a identidade. Se houver linhas na tabela ou se todas as linhas foram removidas usando a instrução DELETE, a próxima linha inserida usará *new_reseed_value* + o valor do [incremento atual](../../t-sql/functions/ident-incr-transact-sql.md). Se uma transação inserir uma linha e depois for revertida, a próxima linha inserida usará *new_reseed_value* + o valor do [incremento atual](../../t-sql/functions/ident-incr-transact-sql.md) como se a linha tivesse sido excluída. Se a tabela não estiver vazia, definir o valor de identidade em um número menor que o valor máximo na coluna de identidade poderá resultar em uma das seguintes condições:<br /><br /> Caso exista uma restrição PRIMARY KEY ou UNIQUE na coluna de identidade, a mensagem de erro 2627 será gerada em operações de inserção posteriores na tabela, porque o valor de identidade gerado estará em conflito com os valores existentes.<br /><br /> –Caso não exista uma restrição PRIMARY KEY ou UNIQUE, operações de inserção posteriores resultarão em valores de identidade duplicados.|  
  
## <a name="exceptions"></a>Exceções

 A tabela a seguir lista condições quando DBCC CHECKIDENT não redefine o valor de identidade atual automaticamente e oferece métodos para redefini-lo.  
  
|Condição|Métodos de redefinição|  
|---------------|-------------------|  
|O valor de identidade atual é maior do que o valor máximo na tabela.|Execute DBCC CHECKIDENT (*table_name*, NORESEED) para determinar o valor máximo atual na coluna. Em seguida, especifique esse valor como o *new_reseed_value* em um comando DBCC CHECKIDENT (*table_name*, RESEED, *new_reseed_value*).<br /><br /> -OU-<br /><br /> Execute DBCC CHECKIDENT (*table_name*, RESEED,*new_reseed_value*) com *new_reseed_value* definido como um valor muito baixo e, em seguida, execute (*table_name*, RESEED) para corrigir o valor.|  
|Todas as linhas são excluídas da tabela.|Execute DBCC CHECKIDENT (*table_name*, RESEED,*new_reseed_value*) com *new_reseed_value* definido como o valor inicial desejado.|  
  
## <a name="changing-the-seed-value"></a>Alterando o valor de semente

 O valor de semente é o valor inserido em uma coluna de identidade na primeira linha carregada na tabela. Todas as linhas subsequentes contêm o valor de identidade atual além do valor de incremento, em que o valor de identidade atual é o último valor de identidade gerado para a tabela ou exibição.  
  
 Não é possível usar DBCC CHECKIDENT para executar as seguintes tarefas:  
  
- Alterar o valor de semente original que foi especificado para uma coluna de identidade quando a tabela ou exibição foram criadas.  
  
- Propagar novamente linhas existentes em uma tabela ou exibição.  
  
 Para alterar o valor de semente original e propagar novamente as linhas existentes, é necessário remover a coluna de identidade e recriá-la especificando o novo valor de semente. Quando a tabela contém dados, os números de identidade são adicionados às linhas existentes com os valores de semente e de incremento especificados. A ordem em que as linhas são atualizadas não é garantida.  
  
## <a name="result-sets"></a>Conjuntos de resultados

 Quer uma das opções seja especificada ou não para uma tabela que contém uma coluna de identidade, DBCC CHECKIDENT retorna a mensagem a seguir para todas as operações, exceto durante a especificação de um novo valor de semente. Essa operação está especificando um novo valor de semente.  
  
`Checking identity information: current identity value '\<current identity value>', current column value '\<current column value>'. DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
 Quando DBCC CHECKIDENT é usado para especificar um novo valor de semente usando RESEED *new_reseed_value*, é retornada a mensagem a seguir.  
  
`Checking identity information: current identity value '\<current identity value>'. DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
## <a name="permissions"></a>Permissões

 O chamador deve ter o esquema que contém a tabela, ou ser um membro da função de servidor fixa **sysadmin**, a função de banco de dados fixa **db_owner** ou a função de banco de dados fixa **db_ddladmin**.

O SQL Data Warehouse do Azure exige permissões de **db_owner**.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-resetting-the-current-identity-value-if-its-needed"></a>a. Redefinindo o valor de identidade atual, se necessário  
 O exemplo a seguir redefine o valor de identidade atual, quando necessário, da tabela especificada no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql
USE AdventureWorks2012;  
GO  
DBCC CHECKIDENT ('Person.AddressType');  
GO  
```  
  
### <a name="b-reporting-the-current-identity-value"></a>B. Relatando o valor de identidade atual

 O exemplo a seguir informa o valor de identidade atual na tabela especificada no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], e não corrige esse valor quando ele está incorreto.  
  
```sql
USE AdventureWorks2012;
GO  
DBCC CHECKIDENT ('Person.AddressType', NORESEED);
GO  
```  
  
### <a name="c-forcing-the-current-identity-value-to-a-new-value"></a>C. Forçando o valor de identidade atual para um novo valor  
 O exemplo a seguir força o valor de identidade atual na coluna `AddressTypeID` na tabela `AddressType` para um valor de 10. Como a tabela tem linhas existentes, a próxima linha inserida usará 11 como o valor, isto é, o valor da identidade atual definido para a coluna mais 1 (que é o valor de incremento da coluna).  

```sql
USE AdventureWorks2012;  
GO  
DBCC CHECKIDENT ('Person.AddressType', RESEED, 10);  
GO  
```

### <a name="d-resetting-the-identity-value-on-an-empty-table"></a>D. Redefinindo o valor de identidade em uma tabela vazia

 O exemplo a seguir força o valor de identidade atual na coluna `ErrorLogID` na tabela `ErrorLog` para um valor de 1 após excluir todos os registros da tabela. Como a tabela não tem linhas existentes, a próxima linha inserida usará 1 como o valor, isto é, o novo valor de identidade atual, sem adicionar o valor de incremento definido para a coluna.  
  
```sql
USE AdventureWorks2012;  
GO  
TRUNCATE TABLE dbo.ErrorLog
GO
DBCC CHECKIDENT ('dbo.ErrorLog', RESEED, 1);  
GO  
```  
  
## <a name="see-also"></a>Consulte Também

[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[IDENTITY &#40;Propriedade&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
[Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md)  
[USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
[IDENT_SEED &#40;Transact-SQL&#41;](../../t-sql/functions/ident-seed-transact-sql.md)  
[IDENT_INCR &#40;Transact-SQL&#41;](../../t-sql/functions/ident-incr-transact-sql.md)  
