---
title: Catalog. Packages (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- packages view [Integration Services]
- catalog.packages view [Integration Services]
ms.assetid: a634e94d-f492-4dfd-9611-a35f545106a1
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f836c2b1bdf59f157f10abb708ed55f99dfc9f0f
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogpackages-ssisdb-database"></a>catalog.packages (Banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe os detalhes de todos os pacotes que aparecem no **SSISDB** catálogo.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|package_id|**bigint**|O identificador exclusivo (ID) do pacote.|  
|name|**nvarchar(256)**|O nome exclusivo do pacote.|  
|package_guid|**uniqueidentifier**|O identificador exclusivo global (GUID) que identifica o pacote.|  
|descrição|**nvarchar (1024)**|Uma descrição opcional do pacote.|  
|package_format_version|**int**|A versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para desenvolver o pacote.|  
|version_major|**int**|A versão principal do pacote.|  
|version_minor|**int**|A versão secundária do pacote.|  
|versão compilação|**int**|A versão de compilação do pacote.|  
|version_comments|**nvarchar (1024)**|Comentários opcionais sobre a versão do pacote.|  
|version_guid|**uniqueidentifier**|O GUID que identifica com exclusividade a versão do pacote.|  
|project_id|**bigint**|O ID exclusivo do projeto.|  
|entry_point|**bit**|O valor de `1` significa que o pacote deve ser iniciado diretamente. O valor de `0` significa que o pacote deve ser iniciado por outro pacote com a tarefa Executar Pacote. O valor padrão é `1`.|  
|validation_status|**char (1)**|O status da validação.|  
|last_validation_time|**DateTimeOffset(7)**|A hora da última validação.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição mostra uma linha para cada pacote no catálogo.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ no projeto correspondente  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor.  
  
> [!NOTE]  
>  Se você tiver a permissão READ em um projeto, também terá a permissão READ em todas as referências de pacotes e ambientes associadas ao projeto. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  

