---
title: Catalog. environment_references (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: efec53ef-3e5a-4b76-b71d-a0cf9e11ac00
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ee6f15af7a5384fea850aa67c7b5a95483530740
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogenvironmentreferences-ssisdb-database"></a>catalog.environment_references (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe as referências de ambiente para todos os projetos a **SSISDB** catálogo.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|reference_id|**bigint**|O ID (identificador exclusivo) da referência.|  
|project_id|**bigint**|O ID exclusivo do projeto.|  
|reference_type|**char (1)**|Indica se o ambiente pode ser localizado na mesma pasta do projeto (referência relativa) ou em uma pasta diferente (referência absoluta). Quando o valor for `R`, o ambiente será localizado por meio de uma referência relativa. Quando o valor for `A`, o ambiente será localizado por meio de uma referência absoluta.|  
|environment_folder_name|**sysname**|O nome da pasta quando o ambiente é localizado por meio de uma referência absoluta.|  
|environment_name|**sysname**|O nome do ambiente referenciado pelo projeto.|  
|validation_status|**char (1)**|O status da validação.|  
|last_validation_time|**datatimeoffset(7)**|A hora da última validação.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição mostra uma linha para cada referência de ambiente no catálogo.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ no projeto correspondente  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor.  
  
> [!NOTE]  
>  Se você tiver a permissão READ em um projeto, também terá a permissão READ em todas as referências de pacotes e ambientes associadas ao projeto. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
## <a name="remarks"></a>Comentários  
 Um projeto pode ter referências de ambiente relativas ou absolutas. As referências relativas fazem referência ao ambiente pelo nome e requerem que ele resida na mesma pasta do projeto. As referências absolutas fazem referência ao ambiente por nome e pasta. Elas podem fazer referência a ambientes que residam em uma pasta diferente da pasta do projeto. Um projeto pode fazer referência a vários ambientes.  
  
  
