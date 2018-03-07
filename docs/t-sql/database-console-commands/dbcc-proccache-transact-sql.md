---
title: DBCC PROCCACHE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC PROCCACHE
- DBCC_PROCCACHE_TSQL
- PROCCACHE_TSQL
- PROCCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- procedure cache [SQL Server]
- displaying procedure cache information
- DBCC PROCCACHE statement
ms.assetid: 7a4f9f8a-13ff-4bf2-ba29-c17012a23659
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 27a247f0900ad39ef77d96a54d68c795dc8f6f07
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-proccache-transact-sql"></a>DBCC PROCCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Exibe informações em um formato de tabela sobre o cache de procedimento.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DBCC PROCCACHE [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
 com  
 Permite que as opções sejam especificadas.  
  
 NO_INFOMSGS  
 Suprime todas as mensagens informativas que têm níveis de severidade de 0 a 10.  
  
## <a name="remarks"></a>Remarks  
O cache de procedimento é usado para armazenar em cache os planos compilados e executáveis a fim de acelerar a execução de lotes. As entradas em um cache de procedimento estão no nível de um lote. O cache de procedimento inclui as seguintes entradas:
-   Planos compilados  
-   Planos de execução  
-   Árvore Algebrizer  
-   Procedimentos estendidos  
  
## <a name="result-sets"></a>Conjuntos de resultados  
A tabela a seguir descreve as colunas do conjunto de resultados.
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|**num proc buffs**|Número total de páginas usadas por todas as entradas no cache de procedimento.|  
|**num proc buffs usados**|Número total de páginas usadas por todas as entradas usadas atualmente.|  
|**num proc buffs ativas**|Somente para compatibilidade com versões anteriores. Número total de páginas usadas por todas as entradas usadas atualmente.|  
|**tamanho do cache de procedimento**|Número total de entradas no cache de procedimento.|  
|**proc cache usado**|Número total de entradas usadas atualmente.|  
|**proc cache ativo**|Somente para compatibilidade com versões anteriores. Número total de entradas usadas atualmente.|  
  
## <a name="permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** ou à função de banco de dados fixa **db_owner** .
  
## <a name="see-also"></a>Consulte também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
