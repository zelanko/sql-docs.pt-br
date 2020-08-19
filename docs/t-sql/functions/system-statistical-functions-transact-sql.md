---
description: Funções estatísticas de sistema (Transact-SQL)
title: Funções estatísticas do sistema (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- statistical functions [SQL Server]
- system statistical functions [SQL Server]
- functions [SQL Server], statistical
ms.assetid: 45828c67-1b9a-4653-bb24-86246084d8ba
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 7368e6bdb14dfdabfe44b79ef68d764dceb40149
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459556"
---
# <a name="system-statistical-functions-transact-sql"></a>Funções estatísticas de sistema (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  As seguintes funções escalares retornam informações estatísticas sobre o sistema:  

:::row:::
    :::column:::
        [@@CONNECTIONS](../../t-sql/functions/connections-transact-sql.md)
    :::column-end:::
    :::column:::
        [@@PACK_RECEIVED](../../t-sql/functions/pack-received-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [@@CPU_BUSY](../../t-sql/functions/cpu-busy-transact-sql.md)
    :::column-end:::
    :::column:::
        [@@PACK_SENT](../../t-sql/functions/pack-sent-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [fn_virtualfilestats](../../relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql.md)
    :::column-end:::
    :::column:::
        [@@TIMETICKS](../../t-sql/functions/timeticks-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [@@IDLE](../../t-sql/functions/idle-transact-sql.md)
    :::column-end:::
    :::column:::
        [@@TOTAL_ERRORS](../../t-sql/functions/total-errors-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [@@IO_BUSY](../../t-sql/functions/io-busy-transact-sql.md)
    :::column-end:::
    :::column:::
        [@@TOTAL_READ](../../t-sql/functions/total-read-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [@@PACKET_ERRORS](../../t-sql/functions/packet-errors-transact-sql.md)
    :::column-end:::
    :::column:::
        [@@TOTAL_WRITE](../../t-sql/functions/total-write-transact-sql.md)
    :::column-end:::
:::row-end:::
  
  
 Todas as funções estatísticas do sistema são não determinísticas. Isso significa que essas funções nem sempre retornam os mesmos resultados a cada chamada, mesmo com o mesmo conjunto de valores de entrada. Para obter mais informações sobre determinismo de funções, consulte [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  
