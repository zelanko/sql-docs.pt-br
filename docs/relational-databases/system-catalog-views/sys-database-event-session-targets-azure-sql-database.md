---
title: sys. database_event_session_targets (banco de dados SQL do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 38d775ee-1fe1-4820-88c6-02b2f875a66b
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7e736adef1648785ec0d037688c340f31a0e1bda
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915105"
---
# <a name="sysdatabase_event_session_targets-azure-sql-database"></a>sys.database_event_session_targets (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada destino de evento em uma sessão de evento.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e a todas as versões posteriores.|  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|A identificação da sessão de evento. Não permite valor nulo.|  
|target_id|**int**|A identificação do destino. Essa identificação é exclusiva dentro de um objeto de sessão de evento. Não permite valor nulo.|  
|name|**sysname**|O nome do destino de evento. Não permite valor nulo.|  
|pacote|**sysname**|O nome do pacote de eventos que contém um destino de evento. Não permite valor nulo.|  
|modulo|**sysname**|O nome do módulo que contém um destino de evento. Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no servidor.  
  
## <a name="remarks"></a>Comentários  
 Essa exibição tem as cardinalidades de relação a seguir.  
  
||||  
|-|-|-|  
|De|Para|Relação|  
|sys. database_event_session_targets. event_session_id|sys. database_event_sessions. event_session_id|Muitos para um|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
