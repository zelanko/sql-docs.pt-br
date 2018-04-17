---
title: sysssispackagefolders (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysdtspackagefolders90
- sysdtspackagefolders90_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackagefolders system table
ms.assetid: ddc4833f-27bf-4610-b739-d257961d17ac
caps.latest.revision: 22
author: douglasl
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 179e6c1241ccbe42528eae591696727c9cea541a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysssispackagefolders-transact-sql"></a>sysssispackagefolders (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada pasta lógica na hierarquia de pastas que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa. Estas pastas são listadas no Object Explorer do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] quando você se conectar ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Uma pasta lista os pacotes que são salvos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no sistema de arquivos.  
  
 O **parentfolderid** coluna descreve a hierarquia de pastas. A pasta na parte superior da hierarquia de pasta contém um valor nulo em **parentfolderid**.  
  
 O **foldername** coluna contém o nome das pastas que aparecem no Pesquisador de objetos.  
  
 Essa tabela é armazenada no **msdb** banco de dados.  

  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**folderid**|**uniqueidentifier**|O GUID da pasta.|  
|**parentfolderid**|**uniqueidentifier**|O GUID da pasta que é a pasta pai.|  
|**foldername**|**sysname**|O nome da pasta. Esse nome é exibido na hierarquia de pasta em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
  
  
