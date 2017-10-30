---
title: Catalog. Projects (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: a6b595e1-5227-47ce-8ee2-a28c1e1d5645
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 668890ae464deb8dfa029eab38b608fee12af0ca
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogprojects-ssisdb-database"></a>catalog.projects (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe os detalhes de todos os projetos que aparecem no **SSISDB** catálogo.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|project_id|**bigint**|O identificador exclusivo (ID) do projeto.|  
|folder_id|**bigint**|O ID exclusivo da pasta onde o projeto reside.|  
|name|**sysname**|O nome do projeto.|  
|descrição|**nvarchar (1024)**|A descrição opcional do projeto.|  
|project_format_version|**int**|A versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para desenvolver o projeto.|  
|deployed_by_sid|**varbinary(85)**|O identificador de segurança (SID) exclusivo do usuário que instalou o projeto.|  
|deployed_by_name|**nvarchar (128)**|O nome do usuário que instalou o projeto.|  
|last_deployed_time|**DateTimeOffset(7)**|A data e a hora em que o projeto foi implantado ou reimplantado.|  
|created_time|**DateTimeOffset(7)**|A data e hora em que o projeto foi criado.|  
|object_version_lsn|**bigint**|A versão do projeto. Não há garantia de que este número seja sequencial.|  
|validation_status|**char (1)**|O status da validação.|  
|last_validation_time|**DateTimeOffset(7)**|A hora da última validação.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição mostra uma linha para cada projeto no catálogo.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ no projeto  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor.  
  
> [!NOTE]  
>  Se você tiver a permissão READ em um projeto, também terá a permissão READ em todas as referências de pacotes e ambientes associadas ao projeto. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  

