---
title: catalog.environment_references (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: efec53ef-3e5a-4b76-b71d-a0cf9e11ac00
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 23956f548b5bb768260ffc618c86cd93f0e82b23
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85673264"
---
# <a name="catalogenvironment_references-ssisdb-database"></a>catalog.environment_references (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe as referências de ambiente para todos os projetos no catálogo do **SSISDB**.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|reference_id|**bigint**|O ID (identificador exclusivo) da referência.|  
|project_id|**bigint**|O ID exclusivo do projeto.|  
|reference_type|**char(1)**|Indica se o ambiente pode ser localizado na mesma pasta do projeto (referência relativa) ou em uma pasta diferente (referência absoluta). Quando o valor for `R`, o ambiente será localizado por meio de uma referência relativa. Quando o valor for `A`, o ambiente será localizado por meio de uma referência absoluta.|  
|environment_folder_name|**sysname**|O nome da pasta quando o ambiente é localizado por meio de uma referência absoluta.|  
|environment_name|**sysname**|O nome do ambiente referenciado pelo projeto.|  
|validation_status|**char(1)**|O status da validação.|  
|last_validation_time|**datatimeoffset(7)**|A hora da última validação.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição mostra uma linha para cada referência de ambiente no catálogo.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ no projeto correspondente  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**.  
  
> [!NOTE]  
>  Se você tiver a permissão READ em um projeto, também terá a permissão READ em todas as referências de pacotes e ambientes associadas ao projeto. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
## <a name="remarks"></a>Comentários  
 Um projeto pode ter referências de ambiente relativas ou absolutas. As referências relativas fazem referência ao ambiente pelo nome e requerem que ele resida na mesma pasta do projeto. As referências absolutas fazem referência ao ambiente por nome e pasta. Elas podem fazer referência a ambientes que residam em uma pasta diferente da pasta do projeto. Um projeto pode fazer referência a vários ambientes.  
  
  
