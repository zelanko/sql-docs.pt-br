---
title: Tabelas (Transact-SQL) do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Integration Services system tables
- system tables [SQL Server], Integration Services
- system tables [Integration Services]
- SSIS, system tables
ms.assetid: 683b181b-0091-4a9c-86db-bc577af43cec
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2298117a10f27a53532d2f4e2346eb699bc2b39c
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65485020"
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
  
  
