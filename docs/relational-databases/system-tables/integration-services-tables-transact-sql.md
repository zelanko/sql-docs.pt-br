---
title: Tabelas (Transact-SQL) do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
ms.workload: Inactive
ms.openlocfilehash: 9a5349b8f36bc5abd9b61d5bd4d1677b3344c528
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
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
  
  
