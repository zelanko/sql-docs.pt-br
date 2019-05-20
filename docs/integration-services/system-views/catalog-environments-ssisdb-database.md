---
title: catalog.environment (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 7014c0e3-65dc-4a46-842e-4decf3737748
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9c3660f7314ce9514b4dc03ee2d6fb1490a4eab7
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65715257"
---
# <a name="catalogenvironments-ssisdb-database"></a>catalog.environments (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe os detalhes de ambiente para todos os ambientes no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Os ambientes contêm variáveis que podem ser referenciadas por projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|environment_id|**bigint**|O ID (identificador exclusivo) do ambiente.|  
|NAME|**sysname**|O nome do ambiente.|  
|folder_id|**bigint**|O ID exclusivo da pasta na qual o ambiente reside.|  
|descrição|**nvarchar(1024)**|A descrição do ambiente. Esse valor é opcional.|  
|created_by_sid|**varbinary(85)**|O SID (identificador de segurança) do usuário que criou o ambiente.|  
|created_by_name|**nvarchar(128)**|O nome de usuário que criou o ambiente.|  
|created_time|**datetimeoffset**|A data e hora em que o ambiente foi criado.|  
  
## <a name="remarks"></a>Remarks  
 Essa exibição mostra uma linha para cada ambiente no catálogo. Nomes de ambiente somente são exclusivos em relação à pasta na qual estão localizados. Por exemplo, um ambiente denominado `E1` pode existir em mais de uma pasta no catálogo, mas cada pasta pode ter apenas um ambiente denominado `E1`.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ no ambiente  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
