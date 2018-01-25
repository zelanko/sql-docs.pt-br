---
title: DBCC SHRINKLOG (Azure SQL Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
caps.latest.revision: "11"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d06917a784e507ab5568e28b4d34273f5fe71063
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-shrinklog-azure-sql-data-warehouse"></a>DBCC SHRINKLOG (Azure SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Reduz o tamanho do log de transações *entre o dispositivo* atual [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] banco de dados. Os dados são desfragmentados para reduzir o log de transações. Ao longo do tempo, o log de transações do banco de dados pode se tornar fragmentado e ineficiente. Use DBCC SHRINKLOG para reduzir a fragmentação e reduzir o tamanho do log.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DBCC SHRINKLOG   
    [ ( SIZE = { target_size [ MB | GB | TB ]  } | DEFAULT ) ]   
    [ WITH NO_INFOMSGS ]   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
TAMANHO = { *target_size* [MB | **GB** | TB]} | **Padrão**.  
*target_size* é o tamanho desejado para o log de transações em todos os nós de computação, após a conclusão do DBCC SHRINKLOG. É um número inteiro maior que 0.  
O tamanho do log é medido em megabytes (MB), gigabytes (GB) ou terabytes (TB). É o tamanho combinado de log de transações em todos os nós de computação.  
Por padrão, o DBCC SHRINKLOG reduz o log de transações para o tamanho de log armazenado nos metadados do banco de dados. O tamanho do log nos metadados é determinado pelo parâmetro LOG_SIZE no [criar banco de dados &#40; Depósito de dados SQL do Azure &#41; ](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) ou [ALTER DATABASE &#40; Depósito de dados SQL do Azure &#41; ](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md). DBCC SHRINKLOG reduz o tamanho do log de transações para o padrão de tamanho quando `SIZE=DEFAULT` for especificado, ou quando o `SIZE` cláusula é omitida.
  
WITH NO_INFOMSGS  
Mensagens informativas não são exibidas nos resultados do DBCC SHRINKLOG.  
  
## <a name="permissions"></a>Permissões  
Requer a permissão ALTER SERVER STATE.
  
## <a name="general-remarks"></a>Comentários gerais  
DBCC SHRINKLOG não altera o tamanho de log armazenado nos metadados do banco de dados. Continua os metadados conter o parâmetro LOG_SIZE que foi especificado na instrução CREATE DATABASE ou ALTER DATABASE.
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-shrink-the-transaction-log-to-the-original-size-specified-by-create-database"></a>A. Reduza o log de transações para o tamanho original especificado ao criar o banco de dados.  
Suponha que o log de transações do banco de dados de endereços foi definido como 100 MB quando o banco de dados de endereços foi criado. Ou seja, a instrução CREATE DATABASE para endereços tinha LOG_SIZE = 100 MB. Agora, vamos supor que o log foi expandido para 150 MB e deseja reduzi-lo novamente como 100 MB.
  
Cada uma das instruções a seguir tenta reduzir o log de transações do banco de dados de endereços para o tamanho padrão de 100 MB. Se reduzir o log de 100 MB causará a perda de dados, o DBCC SHRINKLOG reduzir o log para o menor valor possível de tamanho, maior que 100 MB, sem perda de dados.
  
```sql
USE Addresses;  
DBCC SHRINKLOG ( SIZE = 100 MB );  
DBCC SHRINKLOG ( SIZE = DEFAULT );  
DBCC SHRINKLOG;  
```  
  
  
