---
title: dbo. syscategories (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fc4d6f55ca4e131abef21772911da923b854c81b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82813787"
---
# <a name="dbosyscategories-transact-sql"></a>dbo.syscategories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém as categorias usadas pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para organizar trabalhos, alertas e operadores. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|ID da categoria|  
|**category_class**|**int**|Tipo de item na categoria:<br /><br /> **1** = trabalho<br /><br /> **2** = alerta<br /><br /> **3** = operador|  
|**category_type**|**tinyint**|Tipo de categoria:<br /><br /> **1** = local<br /><br /> **2** = multisservidor<br /><br /> **3** = nenhum|  
|**name**|**sysname**|Nome da categoria|  
  
  
