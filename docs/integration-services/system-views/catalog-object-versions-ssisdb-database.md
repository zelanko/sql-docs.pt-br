---
description: catalog.object_versions (Banco de Dados SSISDB)
title: catalog.object_versions (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 2fd8c020-1c77-4702-8e6b-efa6a348daab
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1a2371508c40e60ebacbe60d656d4d9ffa3f70ce
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422030"
---
# <a name="catalogobject_versions-ssisdb-database"></a>catalog.object_versions (Banco de Dados SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe as versões dos objetos do catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Nesta versão, apenas versões de projetos têm suporte nesta exibição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|object_version_lsn|**bigint**|O ID (identificador exclusivo) da versão do objeto. Não há garantia de que este número seja sequencial.|  
|object_id|**bigint**|A ID exclusiva do objeto.|  
|object_type|**smallint**|O tipo de objeto. Um valor `20` será exibido para projetos.|  
|object_name|**sysname(nvarchar(128))**|O nome do objeto.|  
|descrição|**nvarchar(1024)**|A descrição do projeto.|  
|created_by|**nvarchar(128)**|O nome do usuário que adicionou o objeto ao catálogo.|  
|created_time|**datetimeoffset**|A data e a hora nas quais o objeto foi adicionado ao catálogo.|  
|restored_by|**nvarchar(128)**|O nome do usuário que restaurou o objeto.|  
|last_restored_time|**datetimeoffset**|A data e a hora na qual o objeto foi restaurado pela última vez.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição mostra uma linha para cada versão de um objeto no catálogo.  
  
## <a name="permissions"></a>Permissões  
 Para consultar linhas nesta exibição, você deve ter uma das permissões a seguir:  
  
-   Permissão READ no objeto  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação na função de servidor **sysadmin**.  
  
> [!NOTE]  
>  A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
