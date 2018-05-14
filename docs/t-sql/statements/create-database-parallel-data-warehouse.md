---
title: CREATE DATABASE (Parallel Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 40cacde4-ac72-45f7-9564-d76e2b4a741a
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a7cef1f977e59e8145a57c806d7edaeb262b1275
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="create-database-parallel-data-warehouse"></a>CREATE DATABASE (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Cria um novo banco de dados em um dispositivo [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Use essa instrução para criar todos os arquivos associados a um banco de dados do dispositivo e para definir as opções de tamanho máximo e aumento automático para as tabelas de banco de dados e o log de transações.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE DATABASE database_name   
WITH (   
    [ AUTOGROW = ON | OFF , ]   
    REPLICATED_SIZE = replicated_size [ GB ] ,  
    DISTRIBUTED_SIZE = distributed_size [ GB ] ,  
    LOG_SIZE = log_size [ GB ] )  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 O nome do novo banco de dados. Para obter mais informações sobre nomes de banco de dados permitidos, consulte "Regras de nomenclatura de objeto" e "Nomes de banco de dados reservados" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 AUTOGROW = ON | **OFF**  
 Especifica se os parâmetros *replicated_size*, *distributed_size* e *log_size* para esse banco de dados aumentarão automaticamente, conforme necessário, além de seus tamanhos especificados. O valor padrão é **OFF**.  
  
 Se AUTOGROW for ON, *replicated_size*, *distributed_size* e *log_size* aumentará conforme necessário (não em blocos do tamanho inicial especificado) com cada inserção de dados, atualização ou outra ação que exige mais armazenamento do que já foi alocado.  
  
 Se AUTOGROW for OFF, os tamanhos não aumentarão automaticamente. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] retornará um erro durante a tentativa de uma ação que exige que *replicated_size*, *distributed_size* ou *log_size* aumente além do valor especificado.  
  
 AUTOGROW é ON ou OFF para todos os tamanhos. Por exemplo, não é possível definir AUTOGROW ON para *log_size*, mas não defini-lo para *replicated_size*.  
  
 *replicated_size* [ GB ]  
 Um número positivo. Define o tamanho (em gigabytes de inteiro ou decimal) para o espaço total alocado a tabelas replicadas e os dados correspondentes *em cada nó de Computação*. Para os requisitos de *replicated_size* mínimo e máximo, consulte "Valores mínimos e máximos" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Se AUTOGROW for ON, as tabelas replicadas terão permissão para aumentar além desse limite.  
  
 Se AUTOGROW for OFF, um erro será retornado, caso um usuário tente criar uma nova tabela replicada, inserir dados em uma tabela replicada existente ou atualizar uma tabela replicada existente de uma maneira que aumente o tamanho além de *replicated_size*.  
  
 *distributed_size* [ GB ]  
 Um número positivo. O tamanho, em gigabytes de inteiro ou decimal, para o espaço total alocado para tabelas distribuídas (e os dados correspondentes) *entre o dispositivo*. Para os requisitos de *distributed_size* mínimo e máximo, consulte "Valores mínimos e máximos" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Se AUTOGROW for ON, as tabelas distribuídas terão permissão para aumentar além desse limite.  
  
 Se AUTOGROW for OFF, um erro será retornado, caso um usuário tente criar uma nova tabela distribuída, inserir dados em uma tabela distribuída existente ou atualizar uma tabela distribuída existente de uma maneira que aumente o tamanho além de *distributed_size*.  
  
 *log_size* [ GB ]  
 Um número positivo. O tamanho (em gigabytes de inteiro ou decimal) para o log de transações *entre o dispositivo*.  
  
 Para os requisitos de *log_size* mínimo e máximo, consulte "Valores mínimos e máximos" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Se AUTOGROW for ON, o arquivo de log poderá aumentar além desse limite. Use a instrução [DBCC SHRINKLOG (SQL Data Warehouse do Azure)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) para reduzir o tamanho dos arquivos de log para seu tamanho original.  
  
 Se AUTOGROW for OFF, um erro será retornado para o usuário para qualquer ação que aumente o tamanho do log em um nó de Computação individual para além de *log_size*.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão **CREATE ANY DATABASE** no banco de dados mestre ou a associação à função de servidor fixa **sysadmin**.  
  
 O exemplo a seguir fornece a permissão para criar um banco de dados para o usuário Fay de banco de dados.  
  
```  
USE master;  
GO  
GRANT CREATE ANY DATABASE TO [Fay];  
GO  
```  
  
## <a name="general-remarks"></a>Comentários gerais  
 Os bancos de dados são criados com o nível de compatibilidade de banco de dados 120, que é o nível de compatibilidade do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Isso garante que o banco de dados poderá usar toda as funcionalidade do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] usada pelo PDW.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 A instrução CREATE DATABASE não é permitida em uma transação explícita. Para obter mais informações, consulte [Instruções](../../t-sql/statements/statements.md).  
  
 Para obter informações sobre restrições mínimas e máximas em bancos de dados, consulte "Valores mínimos e máximos" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 No momento em um banco de dados é criado, deve haver espaço livre suficiente disponível *em cada nó de Computação* para alocar o total combinado dos seguintes tamanhos:  
  
-   Banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com tabelas com o tamanho de *replicated_table_size*.  
  
-   Banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com tabelas com o tamanho do (*distributed_table_size*/número de nós de Computação).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registra em log o tamanho de (*log_size*/número de nós de Computação).  
  
## <a name="locking"></a>Bloqueio  
 Usa um bloqueio compartilhado no objeto DATABASE.  
  
## <a name="metadata"></a>Metadados  
 Depois que essa operação for bem-sucedida, uma entrada para esse banco de dados será mostrada nas exibições de metadados [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) e [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-basic-database-creation-examples"></a>A. Exemplos de criação de banco de dados básicos  
 O exemplo a seguir cria o banco de dados `mytest` com uma alocação de armazenamento de 100 GB por nó de Computação para tabelas replicadas, 500 GB por dispositivo para tabelas distribuídas e 100 GB por dispositivo para o log de transações. Neste exemplo, AUTOGROW está desativado por padrão.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB );  
```  
  
 O exemplo a seguir cria o banco de dados `mytest` com os mesmos parâmetros acima, exceto que AUTOGROW está ativado. Isso permite que o banco de dados aumente para fora dos parâmetros de tamanho especificados.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (AUTOGROW = ON,  
   REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB);  
```  
  
### <a name="b-creating-a-database-with-partial-gigabyte-sizes"></a>B. Criando um banco de dados com tamanhos de gigabyte parcial  
 O exemplo a seguir cria o banco de dados `mytest`, com AUTOGROW desativado, uma alocação de armazenamento de 1,5 GB por nó de Computação para tabelas replicadas, 5,25 GB por dispositivo para tabelas distribuídas e 10 GB por dispositivo para o log de transações.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 1.5 GB,  
   DISTRIBUTED_SIZE = 5.25 GB,  
   LOG_SIZE = 10 GB);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
