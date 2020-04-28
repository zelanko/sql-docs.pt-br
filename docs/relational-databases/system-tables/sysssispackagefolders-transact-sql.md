---
title: sysssispackagefolders (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtspackagefolders90
- sysdtspackagefolders90_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackagefolders system table
ms.assetid: ddc4833f-27bf-4610-b739-d257961d17ac
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d2ff4537f5db246dd9bcdc114b02005402f8745f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68029600"
---
# <a name="sysssispackagefolders-transact-sql"></a>sysssispackagefolders (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada pasta lógica na hierarquia de pastas que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o usa. Estas pastas são listadas no Object Explorer do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] quando você se conectar ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Uma pasta lista os pacotes que são salvos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no sistema de arquivos.  
  
 A coluna **ParentFolderId** descreve a hierarquia de pastas. A pasta na parte superior da hierarquia de pastas contém um valor nulo em **ParentFolderId**.  
  
 A coluna **foldername** contém o nome das pastas que aparecem no Pesquisador de objetos.  
  
 Essa tabela é armazenada no banco de dados **msdb** .  

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**FolderId**|**uniqueidentifier**|O GUID da pasta.|  
|**ParentFolderId**|**uniqueidentifier**|O GUID da pasta que é a pasta pai.|  
|**FolderName**|**sysname**|O nome da pasta. Esse nome é exibido na hierarquia de pasta em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
  
  
