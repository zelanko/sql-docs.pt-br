---
title: Catalog.worker_agents (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: d56af0ab150255c53746898a638a32112938755c
ms.contentlocale: pt-br
ms.lasthandoff: 09/08/2017

---
# <a name="catalogworkeragents-ssisdb-database"></a>Catalog.worker_agents (banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Exibe as informações sobre o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] escala fora do trabalho.

|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|O agente de trabalho ID de escala Out trabalhador.|
|IsEnabled|**bit**|Se o trabalho de fora de escala está habilitado.|
|DisplayName|**nvarchar(256)**|O nome de exibição da escala fora do trabalho.|
|Description|**nvarchar(256)**|A descrição da escala fora do trabalho.|
|MachineName|**nvarchar(256)**|O nome da máquina para escala fora do trabalho.|
|Marcas|**nvarchar(max)**|As marcas de escala fora do trabalho.|
|Conta do usuário|**nvarchar(256)**|A conta de usuário que executa o serviço de escala fora do trabalho.|
|LastOnlineTime|**DateTimeOffset(7)**|A última vez em que o trabalho de fora de escala está online.|

## <a name="remarks"></a>Comentários
Essa exibição mostra uma linha para cada escala Out conectar-se a escala Out mestre trabalhando com o catálogo do SSISDB.

## <a name="permissions"></a>Permissões
Esta exibição requer uma das seguintes permissões:

- Associação de **ssis_admin** função de banco de dados

- Associação de **ssis_cluster_executor** função de banco de dados

- Associação de **sysadmin** função de servidor

