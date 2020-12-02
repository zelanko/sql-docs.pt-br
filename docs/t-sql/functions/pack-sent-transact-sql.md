---
description: '&#x40;&#x40;PACK_SENT (Transact-SQL)'
title: '@@PACK_SENT (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@PACK_SENT'
- '@@PACK_SENT_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- number of output packets written
- '@@PACK_SENT function'
- packets [SQL Server], output
- networking [SQL Server], output packets
- connections [SQL Server], packets
- output packets written to network [SQL Server]
ms.assetid: 8a322162-24c9-48e9-bfa4-c060e4e11dba
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3cea756a7ba5ddb79bc9855af183663f53c91dd0
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128383"
---
# <a name="x40x40pack_sent-transact-sql"></a>&#x40;&#x40;PACK_SENT (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna o número de pacotes de saída gravado na rede pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde que ele foi iniciado pela última vez.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
@@PACK_SENT  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 **inteiro**  
  
## <a name="remarks"></a>Comentários  
 Para exibir um relatório que contém várias estatísticas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluindo pacotes enviados e recebidos, execute **sp_monitor**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra o uso de `@@PACK_SENT`.  
  
```sql
SELECT @@PACK_SENT AS 'Pack Sent';  
```  
  
 Este é um exemplo de conjunto de resultados.  
  
```  
Pack Sent  
-----------  
291  
```  
  
## <a name="see-also"></a>Consulte Também  
 [@@PACK_RECEIVED &#40;Transact-SQL&#41;](../../t-sql/functions/pack-received-transact-sql.md)   
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [Funções estatísticas do sistema &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
