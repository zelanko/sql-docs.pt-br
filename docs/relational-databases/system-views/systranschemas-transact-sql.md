---
description: systranschemas (Transact-SQL)
title: systranschemas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- systranschemas
- systranschemas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- systranschemas system table
ms.assetid: 864c3966-cb61-4f2b-8939-ccda112de853
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0f034b802eca4a3349b69067d10280b886ffb22a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446508"
---
# <a name="systranschemas-transact-sql"></a>systranschemas (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **systranschemas** é usada para acompanhar as alterações de esquema nos artigos publicados em publicações transacionais e de instantâneo. Essa tabela é armazenada nos bancos de dados de assinatura e publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**tabid**|**int**|Identifica o artigo de tabela em que a alteração de esquema ocorreu.|  
|**registrou startlsn**|**binary**|Valor LSN no início da alteração de esquema.|  
|**endlsn**|**binary**|Valor LSN no fim da alteração de esquema.|  
|**identificação**|**int**|Tipo de alteração de esquema.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
