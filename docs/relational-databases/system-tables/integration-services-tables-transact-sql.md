---
title: Tabelas (Transact-SQL) do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Integration Services system tables
- system tables [SQL Server], Integration Services
- system tables [Integration Services]
- SSIS, system tables
ms.assetid: 683b181b-0091-4a9c-86db-bc577af43cec
caps.latest.revision: 21
author: douglasl
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fc5df46211b3de92b054fea4120d9b7c884a0ccb
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="integration-services-tables-transact-sql"></a>Tabelas do Integration Services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Os tópicos desta seção descrevem as tabelas do sistema no banco de dados msdb que armazenam as informações usadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 [sysssislog](../../relational-databases/system-tables/sysssislog-transact-sql.md)  
 Contém uma linha para cada entrada de log gerada por um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em tempo de execução.  
  
 Essa tabela só é usada quando os pacotes usam o provedor de logs do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [sysssispackagefolders](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md)  
 Contém uma linha para cada pasta lógica que o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa para organizar pacotes. Os valores de coluna definem as relações pai/filho entre pastas aninhadas.  
  
> [!NOTE]  
>  O [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] exibe os pacotes armazenados em uma exibição hierárquica quando você se conecta ao serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [sysssispackages](../../relational-databases/system-tables/sysssispackages-transact-sql.md)  
 Contém uma linha para cada pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Essa tabela é usada somente quando você armazena pacotes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
