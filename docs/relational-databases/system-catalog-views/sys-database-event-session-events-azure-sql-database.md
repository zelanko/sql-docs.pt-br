---
title: sys. database_event_session_events (banco de dados SQL do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: f4c9eb0a-173c-4c66-8dd8-6f7176b2657f
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6ab2f62063c87dcf55fdbb52eaaa9f7ba2d075a8
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913162"
---
# <a name="sysdatabase_event_session_events-azure-sql-database"></a>sys.database_event_session_events (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada evento em uma sessão de eventos.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e a todas as versões posteriores.|  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|A identificação da sessão de evento. Não permite valor nulo.|  
|event_id|**int**|A ID do evento. Essa ID é exclusiva dentro de um objeto de sessão de evento. Não permite valor nulo.|  
|name|**sysname**|O nome do evento. Não permite valor nulo.|  
|pacote|**sysname**|O nome do pacote de eventos que contém um evento. Não permite valor nulo.|  
|module|**sysname**|O nome do módulo que contém o evento. Não permite valor nulo.|  
|predicate|**nvarchar (3000)**|A expressão de predicado que é aplicada ao evento. Permite valor nulo.|  
|predicate_xml|**nvarchar (3000)**|A expressão de predicado XML que é aplicada ao evento. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no servidor.  
  
## <a name="remarks"></a>Comentários  
 Essa exibição tem as cardinalidades de relação a seguir.  
  
| De | Para | Relação |
| ---- | -- | ------------ |
|sys. database_event_session_events. event_session_id|sys. database_event_sessions. event_session_id|Muitos para um|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
