---
title: catalog.object_versions (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 2fd8c020-1c77-4702-8e6b-efa6a348daab
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b68fcc0cffada1ac895548a0c6858f0bde76fe6c
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65714491"
---
# <a name="catalogobjectversions-ssisdb-database"></a>catalog.object_versions (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe as versões dos objetos do catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Nesta versão, apenas versões de projetos têm suporte nesta exibição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|object_version_lsn|**bigint**|O ID (identificador exclusivo) da versão do objeto. Não há garantia de que este número seja sequencial.|  
|object_id|**bigint**|A ID exclusiva do objeto.|  
|object_type|**smallint**|O tipo do objeto. Um valor `20` será exibido para projetos.|  
|object_name|**sysname(nvarchar(128))**|O nome do objeto.|  
|descrição|**nvarchar(1024)**|A descrição do projeto.|  
|created_by|**nvarchar(128)**|O nome do usuário que adicionou o objeto ao catálogo.|  
|created_time|**datetimeoffset**|A data e a hora nas quais o objeto foi adicionado ao catálogo.|  
|restored_by|**nvarchar(128)**|O nome do usuário que restaurou o objeto.|  
|last_restored_time|**datetimeoffset**|A data e a hora na qual o objeto foi restaurado pela última vez.|  
  
## <a name="remarks"></a>Remarks  
 Esta exibição mostra uma linha para cada versão de um objeto no catálogo.  
  
## <a name="permissions"></a>Permissões  
 Para consultar linhas nesta exibição, você deve ter uma das permissões a seguir:  
  
-   Permissão READ no objeto  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação na função de servidor **sysadmin**.  
  
> [!NOTE]  
>  A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
