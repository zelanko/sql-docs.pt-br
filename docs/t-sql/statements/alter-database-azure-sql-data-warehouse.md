---
title: ALTER DATABASE (SQL Data Warehouse do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: da712a46-5f8a-4888-9d33-773e828ba845
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 2e89ba1dde52c1b5cb919ff34181d7ca723b6c61
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="alter-database-azure-sql-data-warehouse"></a>ALTER DATABASE (SQL Data Warehouse do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Modifica o nome, o tamanho máximo ou o objetivo de serviço de um banco de dados.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER DATABASE database_name  

  MODIFY NAME = new_database_name  
| MODIFY ( <edition_option> [, ... n] )  
  
<edition_option> ::=   
      MAXSIZE = { 
            250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 
          | 30720 | 40960 | 51200 | 61440 | 71680 | 81920 
          | 92160 | 102400 | 153600 | 204800 | 245760 
      } GB  
      | SERVICE_OBJECTIVE = { 
            'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' 
          | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' 
          | 'DW3000' | 'DW6000' | 'DW1000c' | 'DW1500c' | 'DW2000c' 
          | 'DW2500c' | 'DW3000c' | 'DW5000c' | 'DW6000c' | 'DW7500c' 
          | 'DW10000c' | 'DW15000c' | 'DW30000c'
      }  
```  
  
## <a name="arguments"></a>Argumentos  
*database_name*  
Especifica o nome do banco de dados a ser modificado.  

MODIFY NAME = *novo_nome_do_banco_de_dados*  
Renomeia o banco de dados com o nome especificado como *novo_nome_do_banco_de_dados*.  
  
MAXSIZE  
O padrão é 245.760 GB (240 TB).  

**Aplica-se a:** nível de desempenho otimizado para elasticidade

O tamanho máximo permitido para o banco de dados. O banco de dados não pode ultrapassar o MAXSIZE. 

**Aplica-se a:** nível de desempenho otimizado para computação

O tamanho máximo permitido para dados de rowstore no banco de dados. Os dados armazenados em tabelas rowstore, um deltastore de um índice columstore ou um índice não clusterizado em um índice columnstore clusterizado não podem exceder o MAXSIZE.  Os dados compactados no formato columnstore não têm um limite de tamanho e não estão restritos pelo MAXSIZE. 
  
SERVICE_OBJECTIVE  
Especifica o nível de desempenho. Para obter mais informações sobre os objetivos do serviço para [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)], consulte [Níveis de desempenho](https://azure.microsoft.com/documentation/articles/performance-tiers/).  
  
## <a name="permissions"></a>Permissões  
Requer estas permissões:  
  
-   Logon da entidade de segurança no nível do servidor (aquele criado pelo processo de provisionamento), ou  
  
-   Membro da função de banco de dados `dbmanager`.  
  
O proprietário do banco de dados não pode alterar o banco de dados, a menos que ele seja membro da função `dbmanager`.  
  
## <a name="general-remarks"></a>Comentários gerais  
O banco de dados atual deve ser um banco de dados diferente daquele que você está alterando, portanto **ALTER deve ser executado enquanto você está conectado ao banco de dados mestre**.  
  
O SQL Data Warehouse é definido como COMPATIBILITY_LEVEL 130 e não pode ser alterado. Para obter mais detalhes, confira [Improved Query Performance with Compatibility Level 130 in Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/) (Melhor desempenho de consulta com o nível de compatibilidade 130 no Banco de Dados SQL do Azure).
  
Para diminuir o tamanho de um banco de dados, use [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
Para executar ALTER DATABASE, o banco de dados deve estar online e não pode estar no estado em pausa.  
  
A instrução ALTER DATABASE precisa ser executada no modo de confirmação automática, que é o modo padrão de gerenciamento de transações. Isso é definido nas configurações de conexão.  
  
A instrução ALTER DATABASE não pode fazer parte de uma transação definida pelo usuário.

Você não pode alterar o agrupamento de banco de dados.  
  
## <a name="examples"></a>Exemplos  
Antes de executar esses exemplos, verifique se o banco de dados que você está alterando não é o banco de dados atual. O banco de dados atual deve ser um banco de dados diferente daquele que você está alterando, portanto **ALTER deve ser executado enquanto você está conectado ao banco de dados mestre**.  

### <a name="a-change-the-name-of-the-database"></a>A. Alterar o nome do banco de dados  

```  
ALTER DATABASE AdventureWorks2012  
MODIFY NAME = Northwind;  
```  
  
### <a name="b-change-max-size-for-the-database"></a>B. Alterar o tamanho máximo do banco de dados  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB );  
```  
  
### <a name="c-change-the-performance-level"></a>C. Alterar o nível de desempenho  
  
```  
ALTER DATABASE dw1 MODIFY ( SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
### <a name="d-change-the-max-size-and-the-performance-level"></a>D. Alterar o tamanho máximo e o nível de desempenho  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB, SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
## <a name="see-also"></a>Consulte Também  
[CREATE DATABASE (SQL Data Warehouse do Azure)](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)
[Lista de tópicos de referência do SQL Data Warehouse](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-overview-reference/)  
  
