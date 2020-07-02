---
title: Dispositivos sys.sys(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdevices
- sysdevices_TSQL
- sys.sysdevices
- sys.sysdevices_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysdevices compatibility view
- sysdevices system table
ms.assetid: ac5bcaf4-8fb6-4855-8856-d7643f469361
author: rothja
ms.author: jroth
ms.openlocfilehash: 23c6f77ab2ffe78a478a168a917339cb90e50df2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786374"
---
# <a name="syssysdevices-transact-sql"></a>sys.sysdevices (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada arquivo de backup de disco, arquivo de backup de fita e arquivo de banco de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome lógico do arquivo de backup ou arquivo de banco de dados.|  
|**size**|**int**|Tamanho do arquivo em páginas de 2 KB (quilobytes).|  
|**pequena**|**int**|Mantido somente para compatibilidade com versões anteriores.|  
|**elevada**|**int**|Mantido somente para compatibilidade com versões anteriores.|  
|**status**|**smallint**|Bitmap que indica o tipo de dispositivo:<br /><br /> 1 = Disco padrão<br /><br /> 2 = Disco físico<br /><br /> 4 = Disco lógico<br /><br /> 8 = Ignorar cabeçalho<br /><br /> 16 = Arquivo de backup<br /><br /> 32 = Gravações seriais<br /><br /> 4096 = Somente leitura|  
|**cntrltype**|**smallint**|Tipo de controlador:<br /><br /> 0 = Arquivo de banco de dados não CD ROM<br /><br /> 2 = Arquivo de backup de disco<br /><br /> 3 - 4 = Arquivo de backup de disquete<br /><br /> 5 = Arquivo de backup de fita<br /><br /> 6 = Arquivo de pipe nomeado|  
|**phyname**|**nvarchar(260)**|Nome do arquivo físico.|  
  
## <a name="see-also"></a>Consulte Também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
