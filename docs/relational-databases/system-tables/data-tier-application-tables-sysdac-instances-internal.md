---
description: Tabelas de aplicativo da camada de dados – sysdac_instances_internal
title: sysdac_instances_internal (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdac_instances_internal_TSQL
- sysdac_instances_internal
dev_langs:
- TSQL
helpviewer_keywords:
- sysdac_instances_internal
ms.assetid: d2d52cc4-3463-431a-b779-6fbfdeee1dfc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7ccda567989211074c8d151de7f2b3936ccd2b69
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544602"
---
# <a name="data-tier-application-tables---sysdac_instances_internal"></a>Tabelas de aplicativo da camada de dados – sysdac_instances_internal
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe uma linha para cada instância do DAC (Aplicativo da Camada de Dados) implantada a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Essa tabela é armazenada no esquema dbo no banco de dados msdb.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|instance_id|**uniqueidentifier**|Identificador da instância do DAC.|  
|instance_name|**sysname**|Nome da instância do DAC especificada quando a instância foi implantada.|  
|type_name|**sysname**|Nome do DAC especificado quando o pacote do DAC foi criado.|  
|type_version|**nvarchar (64)**|Versão do DAC especificado quando o pacote do DAC foi criado.|  
|description|**nvarchar(4000)**|Uma descrição do DAC escrita quando o pacote do DAC foi criado.|  
|type_stream|**varbinary(max)**|Um fluxo de bits que contém a representação codificada dos objetos lógicos, como tabelas e exibições, contidos no DAC.|  
|date_created|**datetime**|Data e hora em que a instância do DAC foi criada.|  
|created_by|**sysname**|Logon que criou a instância do DAC|  
  
## <a name="remarks"></a>Comentários  
 O acesso somente leitura a essa exibição está disponível para todos os usuários com permissões para se conectar ao banco de dados mestre.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa sysadmin.  
  
## <a name="see-also"></a>Consulte Também  
 [Aplicativos da Camada de Dados](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [dbo.sysdac_instances &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)  
  
  
