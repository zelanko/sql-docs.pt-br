---
description: sys.pdw_health_components (Transact-SQL)
title: sys.pdw_health_components (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: d5c7589b-09b0-4f12-ab84-feb3ec3fbaaa
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: 84c5d002a357dd8780596d61d27b32088e659914
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479007"
---
# <a name="syspdw_health_components-transact-sql"></a>sys.pdw_health_components (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Armazena informações sobre todos os componentes e dispositivos que existem no sistema. Isso inclui hardware, dispositivos de armazenamento e dispositivos de rede.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|component_id|**int**|Identificador exclusivo de um componente ou dispositivo.<br /><br /> Chave para esta exibição.|NOT NULL|  
|group_id|**Int**|O grupo de componentes lógicos ao qual este componente pertence. Consulte [Sys.pdw_health_components (paralelo data warehouse)](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).|NOT NULL|  
|component_name|**nvarchar(255)**|Nome do componente.|NOT NULL|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do Azure Synapse Analytics e do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
