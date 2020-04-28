---
title: sys. dm_os_enumerate_fixed_drives (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/18/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_enumerate_fixed_drives
- sys.dm_os_enumerate_fixed_drives_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_enumerate_fixed_drives dynamic management view
ms.assetid: 2e27489e-cf69-4a89-9036-77723ac3de66
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fa5834c14bfb1fafe3123c28a60359d64d059dfc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "71342511"
---
# <a name="sysdm_os_enumerate_fixed_drives-transact-sql"></a>sys. dm_os_enumerate_fixed_drives (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Introduzido no SQL Server 2019.

Enumera volumes montados em letras de unidade `C:\`como.

|Nome da coluna|Tipo de dados|Descrição|
|-----------------|---------------|-----------------|  
|`fixed_drive_path`|`nvarchar(512)`|Caminho para o volume, como `C:\`.|  
|`drive_type`|`int`|Código para o tipo de unidade. Consulte [ `GetDriveTypeW` a função](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew).|
|`drive_type_desc`|`nvarchar(512)`|Descrição do tipo de unidade. Consulte [ `GetDriveTypeW` a função](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew).|
|`free_space_in_bytes`|`bigint`|Espaço livre em disco em bytes.|

## <a name="permissions"></a>Permissões

O usuário deve ter `VIEW SERVER STATE` permissão no servidor.

## <a name="see-also"></a>Consulte Também  

 [Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas a e/s &#40;&#41;de Transact-SQL](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
