---
description: sys. dm_os_enumerate_fixed_drives (Transact-SQL)
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6be0f2083a39bad3d232fd3105fa94c92fb71640
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454915"
---
# <a name="sysdm_os_enumerate_fixed_drives-transact-sql"></a>sys. dm_os_enumerate_fixed_drives (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Introduzida no SQL Server 2019.

Enumera volumes montados em letras de unidade como `C:\` .

|Nome da coluna|Tipo de dados|Descrição|
|-----------------|---------------|-----------------|  
|`fixed_drive_path`|`nvarchar(512)`|Caminho para o volume, como `C:\` .|  
|`drive_type`|`int`|Código para o tipo de unidade. Consulte a [ `GetDriveTypeW` função](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew).|
|`drive_type_desc`|`nvarchar(512)`|Descrição do tipo de unidade. Consulte a [ `GetDriveTypeW` função](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew).|
|`free_space_in_bytes`|`bigint`|Espaço livre em disco em bytes.|

## <a name="permissions"></a>Permissões

O usuário deve ter `VIEW SERVER STATE` permissão no servidor.

## <a name="see-also"></a>Consulte Também  

 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas a e/s &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
