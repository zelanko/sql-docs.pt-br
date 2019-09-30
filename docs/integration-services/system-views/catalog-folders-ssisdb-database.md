---
title: catalog.folders (Banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 21a37c16-60aa-4b3f-8bca-ac90ad1697ac
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 14930bfd90b242f30a8b3f265f6ed3b367bd07f9
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296533"
---
# <a name="catalogfolders-ssisdb-database"></a>catalog.folders (Banco de dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe as pastas no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|id|**bigint**|O identificador exclusivo da pasta.|  
|NAME|**sysname(nvarchar(128)**|O nome da pasta que é exclusivo no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].|  
|descrição|**nvarchar(1024)**|A descrição da pasta.|  
|created_by_sid|**varbinary(85)**|O SID (identificador de segurança) do usuário que criou a pasta.|  
|created_by_name|**nvarchar(128)**|O nome do usuário que criou a pasta.|  
|created_time|**datetimeoffset(7)**|A data e a hora em que a pasta foi criada.|  
  
## <a name="remarks"></a>Remarks  
 Esta exibição mostra uma linha para cada pasta no catálogo.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na pasta  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
