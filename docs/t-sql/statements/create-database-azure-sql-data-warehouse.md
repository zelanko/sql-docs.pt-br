---
title: CREATE DATABASE (SQL Data Warehouse do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 02/14/20178
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
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 621d348cface10d459693fc64b261fc2fa2ddf04
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33702569"
---
# <a name="create-database-azure-sql-data-warehouse"></a>CREATE DATABASE (SQL Data Warehouse do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Cria um novo banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE DATABASE database_name [ COLLATE collation_name ]  
(  
    [ MAXSIZE = { 
          250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 | 30720 
        | 40960 | 51200 | 61440 | 71680 | 81920 | 92160 | 102400 
        | 153600 | 204800 | 245760 
      } GB ,
    ]  
    EDITION = 'datawarehouse',  
    SERVICE_OBJECTIVE = { 
         'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' | 'DW600' 
        | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' | 'DW3000' | 'DW6000' 
        | 'DW1000c' | 'DW1500c' | 'DW2000c' | 'DW2500c' | 'DW3000c' | 'DW5000c' 
        | 'DW6000c' | 'DW7500c' | 'DW10000c' | 'DW15000c' | 'DW30000c'
    }  
)  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
*database_name*  
O nome do novo banco de dados. Esse nome deve ser exclusivo no servidor SQL, que pode hospedar os bancos de dados [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], e ser compatível com as regras [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para identificadores. Para obter mais informações, consulte [Identificadores](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
*collation_name*  
Especifica o agrupamento padrão do banco de dados. O nome do agrupamento pode ser um nome de agrupamento do Windows ou um nome de agrupamento SQL. Se não for especificado, o banco de dados receberá o agrupamento padrão, que é SQL_Latin1_General_CP1_CI_AS.  
  
Para obter mais informações sobre os nomes de agrupamento do Windows e do SQL, consulte [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx).  
  
*EDITION*  
Especifica a camada de serviço do banco de dados. Para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], use 'datawarehouse'.  
  
*MAXSIZE*  
O padrão é 245.760 GB (240 TB).  

**Aplica-se a:** nível de desempenho otimizado para elasticidade

O tamanho máximo permitido para o banco de dados. O banco de dados não pode ultrapassar o MAXSIZE. 

**Aplica-se a:** nível de desempenho otimizado para computação

O tamanho máximo permitido para dados de rowstore no banco de dados. Os dados armazenados em tabelas rowstore, um deltastore de um índice columstore ou um índice não clusterizado em um índice columnstore clusterizado não podem exceder o MAXSIZE.  Os dados compactados no formato columnstore não têm um limite de tamanho e não estão restritos pelo MAXSIZE.
  
SERVICE_OBJECTIVE  
Especifica o nível de desempenho. Para obter mais informações sobre os objetivos do serviço para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], consulte [Níveis de desempenho](https://azure.microsoft.com/documentation/articles/performance-tiers/).  
  
## <a name="general-remarks"></a>Comentários gerais  
Use [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md) para ver as propriedades do banco de dados.  
  
Use [ALTER DATABASE &#40;SQL Data Warehouse do Azure&#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md) para alterar o tamanho máximo ou os valores objetivos de serviço posteriormente.   

O SQL Data Warehouse é definido como COMPATIBILITY_LEVEL 130 e não pode ser alterado. Para obter mais detalhes, confira [Improved Query Performance with Compatibility Level 130 in Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/) (Melhor desempenho de consulta com o nível de compatibilidade 130 no Banco de Dados SQL do Azure).
  
## <a name="permissions"></a>Permissões  
Permissões necessárias:  
  
-   Logon de entidade de segurança de nível de serviço, criado pelo processo de provisionamento ou  
  
-   Membro da função de banco de dados `dbmanager`.  
  
## <a name="error-handling"></a>Tratamento de erros  
Se o tamanho do banco de dados atingir MAXSIZE, você receberá o código de erro 40544. Quando isso ocorre, não é possível inserir, atualizar dados nem criar novos objetos (como tabelas, procedimentos armazenados, exibições e funções). Ainda é possível ler e excluir dados, truncar tabelas, remover tabelas e índices e recriar índices. Você pode atualizar MAXSIZE para um valor maior que o tamanho atual do banco de dados ou excluir alguns dados para liberar espaço de armazenamento. Pode haver um atraso máximo de quinze minutos para que você possa inserir novos dados.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
Você deve estar conectado ao banco de dados mestre para criar um novo banco de dados.  
  
A instrução `CREATE DATABASE` deve ser a única instrução em um lote do [!INCLUDE[tsql](../../includes/tsql-md.md)].

Não é possível alterar o agrupamento de banco de dados depois que o banco de dados é criado.   
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]  
  
### <a name="a-simple-example"></a>A. Exemplo simples  
Um exemplo simples para criar um banco de dados de data warehouse. Isso cria o banco de dados com o menor tamanho máximo que é 10240 GB, o agrupamento padrão que é SQL_Latin1_General_CP1_CI_AS e a menor potência de computação que é DW100.  
  
```  
CREATE DATABASE TestDW  
(EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');  
```  
  
### <a name="b-create-a-data-warehouse-database-with-all-the-options"></a>B. Criar um banco de dados de data warehouse com todas as opções  
Um exemplo da criação de um data warehouse de 10 terabytes que usa todas as opções.  
  
```  
CREATE DATABASE TestDW COLLATE Latin1_General_100_CI_AS_KS_WS  
(MAXSIZE = 10240 GB, EDITION = 'datawarehouse', SERVICE_OBJECTIVE = 'DW1000');  
```  
  
## <a name="see-also"></a>Consulte Também  
[ALTER DATABASE &#40;SQL Data Warehouse do Azure &#40;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)
[CREATE TABLE &#40;SQL Data Warehouse do Azure &#41;](../../t-sql/statements/create-table-azure-sql-data-warehouse.md) 
[DROP DATABASE &#40;Transact-SQL&#40;](../../t-sql/statements/drop-database-transact-sql.md) 
  

