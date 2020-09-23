---
description: DBCC SHRINKLOG (Parallel Data Warehouse)
title: DBCC SHRINKLOG (Parallel Data Warehouse)
ms.custom: ''
ms.date: 03/16/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
author: pmasl
ms.author: umajay
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: bae2ef1468110ba89d77d5f7a6360aecb324abd0
ms.sourcegitcommit: 1126792200d3b26ad4c29be1f561cf36f2e82e13
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076695"
---
# <a name="dbcc-shrinklog-parallel-data-warehouse"></a>DBCC SHRINKLOG (Parallel Data Warehouse)

[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

Reduz o tamanho do log de transações *no dispositivo* para o banco de dados [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] atual. Os dados são desfragmentados para reduzir o log de transações. Ao longo do tempo, o log de transações do banco de dados pode se tornar fragmentado e ineficiente. Use o DBCC SHRINKLOG para reduzir a fragmentação e reduzir o tamanho do log.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DBCC SHRINKLOG   
    [ ( SIZE = { target_size [ MB | GB | TB ]  } | DEFAULT ) ]   
    [ WITH NO_INFOMSGS ]   
[;]  
```  

## <a name="arguments"></a>Argumentos

SIZE = { *target_size* [ MB \| **GB** \| TB ]  } \| **DEFAULT**.  
*target_size* é o tamanho desejado para o log de transações em todos os nós de computação, após a conclusão do DBCC SHRINKLOG. É um número inteiro maior que 0.  
O tamanho do log é medido em megabytes (MB), gigabytes (GB) ou terabytes (TB). É o tamanho combinado do log de transações em todos os nós de computação.  
Por padrão, o DBCC SHRINKLOG reduz o log de transações para o tamanho do log armazenado nos metadados do banco de dados. O tamanho do log nos metadados é determinado pelo parâmetro LOG_SIZE em [CREATE DATABASE &#40;Azure Synapse Analytics&#41;](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) ou [ALTER DATABASE &#40;Azure Synapse Analytics&#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md). O DBCC SHRINKLOG reduz o tamanho do log de transações para o tamanho padrão quando `SIZE=DEFAULT` é especificado ou quando a cláusula `SIZE` é omitida.
  
WITH NO_INFOMSGS  
As mensagens informativas não são exibidas nos resultados do DBCC SHRINKLOG.  
  
## <a name="permissions"></a>Permissões

Requer a permissão ALTER SERVER STATE.

## <a name="general-remarks"></a>Comentários gerais

O DBCC SHRINKLOG não altera o tamanho do log armazenado nos metadados do banco de dados. Os metadados continuam contendo o parâmetro LOG_SIZE que foi especificado na instrução CREATE DATABASE ou ALTER DATABASE.
  
## <a name="examples"></a>Exemplos

### <a name="a-shrink-the-transaction-log-to-the-original-size-specified-by-create-database"></a>a. Reduza o log de transações para o tamanho original especificado por CREATE DATABASE.  
Suponha que o log de transações do banco de dados de endereços tenha sido definido com 100 MB quando o banco de dados de endereços foi criado. Ou seja, a instrução CREATE DATABASE para endereços tinha LOG_SIZE = 100 MB. Agora, vamos supor que o log tenha aumentado para 150 MB e que você deseje reduzi-lo novamente para 100 MB.
  
Cada uma das instruções a seguir tentará reduzir o log de transações do banco de dados de endereços para o tamanho padrão de 100 MB. Se a redução do log para 100 MB for causar perda de dados, o DBCC SHRINKLOG reduzirá o log para o menor valor de tamanho possível que seja maior que 100 MB, sem perda de dados.

```sql
USE Addresses;  
DBCC SHRINKLOG ( SIZE = 100 MB );  
DBCC SHRINKLOG ( SIZE = DEFAULT );  
DBCC SHRINKLOG;  
```
