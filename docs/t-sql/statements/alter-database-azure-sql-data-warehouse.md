---
title: ALTER DATABASE (Azure SQL Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: da712a46-5f8a-4888-9d33-773e828ba845
caps.latest.revision: "20"
author: barbkess
ms.author: barbkess
manager: craigg
ms.openlocfilehash: 71737beb817cfeebed195c90d056768aef678a3e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="alter-database-azure-sql-data-warehouse"></a>ALTERAR o banco de dados (SQL Azure Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Modifica o nome, o tamanho máximo ou o objetivo de serviço para um banco de dados.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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

MODIFY NAME = *new_database_name*  
Renomeia o banco de dados com o nome especificado como *new_database_name*.  
  
MAXSIZE  
O padrão é 10.240 GB (10 TB).  

**Aplica-se a:** otimizado para o nível de desempenho de elasticidade

O tamanho máximo permitido para o banco de dados. O banco de dados não pode ultrapassar o MAXSIZE. 

**Aplica-se a:** otimizado para o nível de desempenho de computação

O tamanho máximo permitido para dados de rowstore no banco de dados. Dados armazenados em tabelas rowstore, deltastore de um índice columnstore ou um índice não clusterizado em um índice columnstore clusterizado não podem ultrapassar o MAXSIZE.  Os dados compactados no formato columnstore não tem um limite de tamanho e não está restrito a MAXSIZE. 
  
SERVICE_OBJECTIVE  
Especifica o nível de desempenho. Para obter mais informações sobre os objetivos do serviço para [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)], consulte [níveis de desempenho](https://azure.microsoft.com/documentation/articles/performance-tiers/).  
  
## <a name="permissions"></a>Permissões  
Requer estas permissões:  
  
-   Logon principal no nível de servidor (aquele criado pelo processo de provisionamento), ou  
  
-   Membro de `dbmanager` função de banco de dados.  
  
O proprietário do banco de dados não é possível alterar o banco de dados, a menos que o proprietário é membro de `dbmanager` função.  
  
## <a name="general-remarks"></a>Comentários gerais  
O banco de dados atual deve ser um banco de dados diferente daquele que você está alterando, portanto **ALTER deve ser executado enquanto estiver conectado ao banco de dados mestre**.  
  
SQL Data Warehouse é definido como COMPATIBILITY_LEVEL 130 e não pode ser alterado. Para obter mais detalhes, consulte [melhor desempenho de consultas com compatibilidade nível 130 no banco de dados do SQL Azure](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/).
  
Para diminuir o tamanho de um banco de dados, use [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
Para executar ALTER DATABASE, o banco de dados deve estar online e não pode estar em um estado de pausa.  
  
A instrução ALTER DATABASE deve ser executado em modo de confirmação automática, que é o modo padrão de gerenciamento de transações. Isso é definido nas configurações de conexão.  
  
A instrução ALTER DATABASE não pode ser parte de uma transação definida pelo usuário.

Você não pode alterar o agrupamento de banco de dados.  
  
## <a name="examples"></a>Exemplos  
Antes de executar esses exemplos, verifique se o banco de dados que você está alterando não é o banco de dados atual. O banco de dados atual deve ser um banco de dados diferente daquele que você está alterando, portanto **ALTER deve ser executado enquanto estiver conectado ao banco de dados mestre**.  

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
  
## <a name="see-also"></a>Consulte também  
[Criar banco de dados (SQL Azure Data Warehouse)](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)
[lista de SQL Data Warehouse de tópicos de referência](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-overview-reference/)  
  
