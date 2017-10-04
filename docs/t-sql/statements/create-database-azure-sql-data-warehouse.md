---
title: Criar banco de dados (SQL Azure Data Warehouse) | Microsoft Docs
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 03/14/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 42819b93-b757-4b2c-8179-d4be3c512c19
caps.latest.revision: 20
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a178756610f0d0e463c21a2a62a287ada6c863a1
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-database-azure-sql-data-warehouse"></a>Criar banco de dados (SQL Azure Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Cria um novo banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE DATABASE database_name [ COLLATE collation_name ]  
(  
    [ MAXSIZE = { 250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 | 30720 | 40960 | 51200 | 61440 | 71680 | 81920 | 92160 | 102400 | 153600 | 204800 | 245760 } GB ,]  
    EDITION = 'datawarehouse',  
    SERVICE_OBJECTIVE = { 'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' | 'DW3000' | 'DW6000' }  
)  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
*database_name*  
O nome do novo banco de dados. Esse nome deve ser exclusivo no SQL server, que pode hospedar ambos [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] bancos de dados e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] bancos de dados e estar de acordo com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] regras para identificadores. Para obter mais informações, consulte [identificadores](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
*collation_name*  
Especifica o agrupamento padrão do banco de dados. O nome do agrupamento pode ser um nome de agrupamento do Windows ou um nome de agrupamento SQL. Se não for especificado, o banco de dados é atribuído o agrupamento padrão, que é SQL_Latin1_General_CP1_CI_AS.  
  
Para obter mais informações sobre os nomes de agrupamento do Windows e do SQL, consulte [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx).  
  
*EDIÇÃO*  
Especifica a camada de serviço do banco de dados. Para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] usar 'datawarehouse'.  
  
*MAXSIZE*  
O tamanho máximo que do banco de dados pode atingir. Definir esse valor impede que o aumento do tamanho do banco de dados além do conjunto de tamanho. O padrão *MAXSIZE* quando não especificado é 10240 GB (10 TB).  Outros valores possíveis variam de 250 GB até 240 TB.  
  
SERVICE_OBJECTIVE  
Especifica o nível de desempenho. Para obter mais informações sobre os objetivos do serviço para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], consulte [dimensionar o desempenho no SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-performance-scale/).  
  
## <a name="general-remarks"></a>Comentários gerais  
Use [DATABASEPROPERTYEX &#40; Transact-SQL &#41; ](../../t-sql/functions/databasepropertyex-transact-sql.md) para ver as propriedades de banco de dados.  
  
Use [ALTER DATABASE &#40; Depósito de dados SQL do Azure &#41; ](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md) para alterar o tamanho máximo ou os valores do objetivo de serviço mais tarde.   

SQL Data Warehouse é definido como COMPATIBILITY_LEVEL 130 e não pode ser alterado. Para obter mais detalhes, consulte [melhor desempenho de consultas com compatibilidade nível 130 no banco de dados do SQL Azure](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/).
  
## <a name="permissions"></a>Permissões  
Permissões necessárias:  
  
-   Logon nível do servidor principal, criado pelo processo de provisionamento, ou  
  
-   Membro de `dbmanager` função de banco de dados.  
  
## <a name="error-handling"></a>Tratamento de erros  
Se o tamanho do banco de dados atingir MAXSIZE, você receberá o código de erro 40544. Quando isso ocorrer, você não pode inserir e atualizar dados ou criar novos objetos (como tabelas, procedimentos armazenados, exibições e funções). Você pode ainda ler e excluir dados, truncar tabelas, Descartar tabelas e índices e reconstruir índices. Você pode atualizar MAXSIZE para um valor maior que o tamanho atual do banco de dados ou excluir alguns dados para liberar espaço de armazenamento. Pode haver um atraso máximo de quinze minutos para que você possa inserir novos dados.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
Você deve estar conectado ao banco de dados mestre para criar um novo banco de dados.  
  
A instrução `CREATE DATABASE` deve ser a única instrução em um lote do [!INCLUDE[tsql](../../includes/tsql-md.md)].

Você não pode alterar o agrupamento de banco de dados depois que o banco de dados é criado.   
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd"></a>Exemplos:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]  
  
### <a name="a-simple-example"></a>A. Exemplo simples  
Um exemplo simples para a criação de um banco de dados do data warehouse. Isso cria o banco de dados com o menor tamanho máximo que é 10240 GB, o agrupamento padrão que é SQL_Latin1_General_CP1_CI_AS e a capacidade de computação menor que é DW100.  
  
```  
CREATE DATABASE TestDW  
(EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');  
```  
  
### <a name="b-create-a-data-warehouse-database-with-all-the-options"></a>B. Criar um banco de dados do data warehouse com todas as opções  
Um exemplo de como criar um um data warehouse de 10 terabytes usando todas as opções.  
  
```  
CREATE DATABASE TestDW COLLATE Latin1_General_100_CI_AS_KS_WS  
(MAXSIZE = 10240 GB, EDITION = 'datawarehouse', SERVICE_OBJECTIVE = 'DW1000');  
```  
  
## <a name="see-also"></a>Consulte também  
[ALTER DATABASE &#40; Depósito de dados SQL do Azure &#40; ](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md) 
 [Criar tabela &#40; Depósito de dados SQL do Azure &#41; ](../../t-sql/statements/create-table-azure-sql-data-warehouse.md)  
 [Remover banco de dados &#40; Transact-SQL &#40;](../../t-sql/statements/drop-database-transact-sql.md) 
  


