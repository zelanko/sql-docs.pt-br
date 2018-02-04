---
title: dbo.syscategories (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.syscategories_TSQL
- syscategories
- syscategories_TSQL
- dbo.syscategories
dev_langs:
- TSQL
helpviewer_keywords:
- syscategories system table
ms.assetid: eb2cb75c-dc58-4a5b-b329-664e9fe20ce0
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 870bd7217d215b7304ceed911d0dd8da2cca5837
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="dbosyscategories-transact-sql"></a>dbo.syscategories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém as categorias usadas pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para organizar trabalhos, alertas e operadores. Essa tabela é armazenada no **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**category_id**|**Int**|ID da categoria|  
|**category_class**|**Int**|Tipo de item na categoria:<br /><br /> **1** = Job<br /><br /> **2** = alerta<br /><br /> **3** operador =|  
|**category_type**|**tinyint**|Tipo de categoria:<br /><br /> **1** = Local<br /><br /> **2** = multisservidor<br /><br /> **3** = nenhum|  
|**name**|**sysname**|Nome da categoria|  
  
  
