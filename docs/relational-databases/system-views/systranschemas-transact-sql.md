---
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
ms.openlocfilehash: f3ba5516920cee6cb2f6f18f0120844e4320afe5
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881186"
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
  
  
