---
title: sysdac_instances_internal (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- sysdac_instances_internal_TSQL
- sysdac_instances_internal
dev_langs:
- TSQL
helpviewer_keywords:
- sysdac_instances_internal
ms.assetid: d2d52cc4-3463-431a-b779-6fbfdeee1dfc
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5389e86dee17cd4a8a4e5432e98d7c5a554c1469
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-tier-application-tables---sysdacinstancesinternal"></a>Tabelas de aplicativo da camada de dados - sysdac_instances_internal
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe uma linha para cada instância do DAC (Aplicativo da Camada de Dados) implantada a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Essa tabela é armazenada no esquema dbo no banco de dados msdb.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|instance_id|**uniqueidentifier**|Identificador da instância do DAC.|  
|instance_name|**sysname**|Nome da instância do DAC especificada quando a instância foi implantada.|  
|type_name|**sysname**|Nome do DAC especificado quando o pacote do DAC foi criado.|  
|type_version|**nvarchar(64)**|Versão do DAC especificado quando o pacote do DAC foi criado.|  
|descrição|**nvarchar(4000)**|Uma descrição do DAC escrita quando o pacote do DAC foi criado.|  
|type_stream|**varbinary(max)**|Um fluxo de bits que contém a representação codificada dos objetos lógicos, como tabelas e exibições, contidos no DAC.|  
|date_created|**datetime**|Data e hora em que a instância do DAC foi criada.|  
|created_by|**sysname**|Logon que criou a instância do DAC|  
  
## <a name="remarks"></a>Remarks  
 Acesso somente leitura a essa exibição está disponível para todos os usuários com permissões para se conectar ao banco de dados mestre.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa sysadmin.  
  
## <a name="see-also"></a>Consulte também  
 [Aplicativos da camada de dados](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [dbo.sysdac_instances &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)  
  
  
