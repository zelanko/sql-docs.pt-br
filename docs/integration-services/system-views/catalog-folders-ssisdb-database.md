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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9723e705f116f84e53edded861d80b7342a3d260
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47786204"
---
# <a name="catalogfolders-ssisdb-database"></a>catalog.folders (Banco de dados SSISDB)
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
  
  
