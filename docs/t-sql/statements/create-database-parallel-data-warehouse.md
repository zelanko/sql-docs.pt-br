---
title: Criar banco de dados (Parallel Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 40cacde4-ac72-45f7-9564-d76e2b4a741a
caps.latest.revision: 13
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 52a55d6c275388e03e3f7be09d265a3b918f583f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-database-parallel-data-warehouse"></a>Criar banco de dados (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Cria um novo banco de dados em um [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dispositivo. Use esta instrução para criar todos os arquivos associados a um banco de dados do dispositivo e para definir as opções de aumento automático para as tabelas de banco de dados e log de transações e o tamanho máximo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 O nome do novo banco de dados. Para obter mais informações sobre nomes de banco de dados permitidos, consulte "Regras de nomenclatura de objeto" e "Nomes reservados do banco de dados" a [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 AUMENTO AUTOMÁTICO = ON | **OFF**  
 Especifica se o *replicated_size*, *distributed_size*, e *log_size* parâmetros para este banco de dados crescerá automaticamente conforme necessário, além de seus especificado tamanhos. Valor padrão é **OFF**.  
  
 Se o crescimento automático for ON, *replicated_size*, *distributed_size*, e *log_size* crescerá como necessária (não em blocos do tamanho inicial especificado) com cada inserção de dados atualização ou outra ação que requer mais armazenamento que já foi alocado.  
  
 Se o crescimento automático for OFF, os tamanhos não crescerá automaticamente. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]retornará um erro durante a tentativa de uma ação que requer *replicated_size*, *distributed_size*, ou *log_size* ultrapassar o valor especificado.  
  
 Aumento automático é ON para todos os tamanhos ou OFF para todos os tamanhos. Por exemplo, não é possível definir o crescimento automático ON para *log_size*, mas não defini-lo para *replicated_size*.  
  
 *replicated_size* [GB]  
 Um número positivo. Define o tamanho (em gigabytes de número inteiro ou decimal) para o espaço total alocado para tabelas replicadas e os dados correspondentes *em cada nó de computação*. Para mínimo e máximo *replicated_size* requisitos, consulte "Mínimo e máximo valores" a [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Se o crescimento automático for ON, tabelas replicadas terão permissão para crescer além desse limite.  
  
 Se o crescimento automático for OFF, um erro será retornado se um usuário tentar criar uma nova tabela replicada, inserir dados em um existente replicados da tabela ou atualizar uma existente replicadas a tabela de uma maneira que pode aumentar o tamanho além *replicated_size*.  
  
 *distributed_size* [GB]  
 Um número positivo. O tamanho, em gigabytes, inteiro ou decimal, para o espaço total alocado para tabelas distribuídas (e os dados correspondentes) *entre o dispositivo*. Para mínimo e máximo *distributed_size* requisitos, consulte "Mínimo e máximo valores" a [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Se o crescimento automático for ON, tabelas distribuídas terão permissão para crescer além desse limite.  
  
 Se o crescimento automático for OFF, um erro será retornado se um usuário tentar criar uma nova tabela distribuída, inserir dados em um existente distribuídas de tabela ou atualizar uma tabela existente distribuída de maneira que pode aumentar o tamanho além *distributed_size* .  
  
 *log_size* [GB]  
 Um número positivo. O tamanho (em gigabytes de número inteiro ou decimal) para o log de transações *entre o dispositivo*.  
  
 Para mínimo e máximo *log_size* requisitos, consulte "Mínimo e máximo valores" a [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Se o crescimento automático for ON, o arquivo de log pode crescer além desse limite. Use o [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) declaração para reduzir o tamanho dos arquivos de log para o tamanho original.  
  
 Se o crescimento automático for OFF, um erro será retornado para o usuário para qualquer ação que pode aumentar o tamanho do log em um nó de computação individual além *log_size*.  
  
## <a name="permissions"></a>Permissões  
 Requer o **CREATE ANY DATABASE** permissão no banco de dados mestre ou associação de **sysadmin** função de servidor fixa.  
  
 O exemplo a seguir fornece a permissão para criar um banco de dados para o usuário Fay de banco de dados.  
  
```  
USE master;  
GO  
GRANT CREATE ANY DATABASE TO [Fay];  
GO  
```  
  
## <a name="general-remarks"></a>Comentários gerais  
 Bancos de dados são criados com o nível de compatibilidade de banco de dados 120, que é a compatibilidade níveis para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Isso garante que o banco de dados será capaz de usar todos os [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] funcionalidade que usa o PDW.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 A instrução CREATE DATABASE não é permitida em uma transação explícita. Para obter mais informações, consulte [instruções](../../t-sql/statements/statements.md).  
  
 Para obter informações sobre restrições de mínimas e máxima em bancos de dados, consulte "Mínimo e máximo valores" a [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 No momento em um banco de dados é criado, deve haver espaço livre suficiente disponível *em cada nó de computação* para alocar o total combinado dos seguintes tamanhos de:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]banco de dados com tabelas com o tamanho de *replicated_table_size*.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]banco de dados com tabelas com o tamanho do (*distributed_table_size* / número de nós de computação).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]registra o tamanho do (*log_size* / número de nós de computação).  
  
## <a name="locking"></a>Bloqueio  
 Leva um bloqueio compartilhado no objeto de banco de dados.  
  
## <a name="metadata"></a>Metadados  
 Depois que essa operação for bem-sucedida, uma entrada para este banco de dados serão exibidos no [sys. Databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) e [sys. Objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)exibições de metadados.  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Exemplos:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-basic-database-creation-examples"></a>A. Exemplos de criação de banco de dados básicos  
 O exemplo a seguir cria o banco de dados `mytest` com uma alocação de 100 GB de armazenamento por nó de computação para tabelas replicadas, 500 GB por aplicação para tabelas distribuídas e 100 GB por dispositivo para o log de transações. Neste exemplo, o crescimento automático está desativado por padrão.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB );  
```  
  
 O exemplo a seguir cria o banco de dados `mytest` com os mesmos parâmetros acima, exceto que o crescimento automático está ativado. Isso permite que o banco de dados cresça fora os parâmetros de tamanho especificado.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (AUTOGROW = ON,  
   REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB);  
```  
  
### <a name="b-creating-a-database-with-partial-gigabyte-sizes"></a>B. Criando um banco de dados com tamanhos de gigabyte parcial  
 O exemplo a seguir cria o banco de dados `mytest`, com crescimento automático off, uma alocação de armazenamento de 1,5 GB por nó de computação para tabelas replicadas, 5,25 GB por aplicação para tabelas distribuídas e 10 GB por dispositivo para o log de transações.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 1.5 GB,  
   DISTRIBUTED_SIZE = 5.25 GB,  
   LOG_SIZE = 10 GB);  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40; Parallel Data Warehouse &#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
