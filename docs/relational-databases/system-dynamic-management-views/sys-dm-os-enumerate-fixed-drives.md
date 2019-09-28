---
title: sys. dm _os_enumerate_fixed_drives (Transact-SQL) | Microsoft Docs
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
ms.sourcegitcommit: c4875c097e3aae1b76233777d15e0a0ec8e0d681
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71342511"
---
# <a name="sysdm_os_enumerate_fixed_drives-transact-sql"></a>sys. dm _os_enumerate_fixed_drives (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Introduzido no SQL Server 2019.

Enumera volumes montados em letras de unidade, como `C:\`.

|Nome da coluna|Tipo de dados|Descrição|
|-----------------|---------------|-----------------|  
|`fixed_drive_path`|`nvarchar(512)`|Caminho para o volume, como `C:\`.|  
|`drive_type`|`int`|Código para o tipo de unidade. Confira [a função `GetDriveTypeW`](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew).|
|`drive_type_desc`|`nvarchar(512)`|Descrição do tipo de unidade. Confira [a função `GetDriveTypeW`](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew).|
|`free_space_in_bytes`|`bigint`|Espaço livre em disco em bytes.|

## <a name="permissions"></a>Permissões

O usuário deve ter a permissão `VIEW SERVER STATE` no servidor.

## <a name="see-also"></a>Consulte também  

 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições e funções &#40;de gerenciamento dinâmico relacionadas a e/s do TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
