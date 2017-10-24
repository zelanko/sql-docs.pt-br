---
title: DBCC PROCCACHE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 97e617e7867c90bf1e66c5e64e37b9039087d463
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-proccache-transact-sql"></a>DBCC PROCCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>Comentários  
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
  
  

