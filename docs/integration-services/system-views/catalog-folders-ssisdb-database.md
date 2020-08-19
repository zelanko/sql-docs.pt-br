---
description: catalog.folders (Banco de dados SSISDB)
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
ms.openlocfilehash: 8ec7f8fad821c5c62d7b7ec58290050a52b0bf17
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422060"
---
# <a name="catalogfolders-ssisdb-database"></a>catalog.folders (Banco de dados SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe as pastas no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|id|**bigint**|O identificador exclusivo da pasta.|  
|name|**sysname(nvarchar(128)**|O nome da pasta que é exclusivo no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].|  
|descrição|**nvarchar(1024)**|A descrição da pasta.|  
|created_by_sid|**varbinary(85)**|O SID (identificador de segurança) do usuário que criou a pasta.|  
|created_by_name|**nvarchar(128)**|O nome do usuário que criou a pasta.|  
|created_time|**datetimeoffset(7)**|A data e a hora em que a pasta foi criada.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição mostra uma linha para cada pasta no catálogo.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na pasta  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
