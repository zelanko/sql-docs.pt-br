---
title: Catalog.master_properties (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: 0fcbdca57c7764eaec758d2ad9ef3ab8675a3a9b
ms.contentlocale: pt-br
ms.lasthandoff: 09/08/2017

---
# <a name="catalogmasterproperties-ssisdb-database"></a>Catalog.master_properties (banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Exibe as propriedades do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mestre fora de escala.

|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|O nome da propriedade mestre expansão.|  
|property_value|**nvarchar(max)**|O valor da propriedade mestre expansão.|

## <a name="remarks"></a>Comentários
Essa exibição mostra uma linha para cada propriedade mestre de expansão. As propriedades mostradas por esta exibição incluem o seguinte:

|Nome da propriedade|Description|  
|-------------------|-----------------| 
|**CLUSTER_LOGDB_SERVER**|Localiza o SQL Server que o banco de dados de log em.|
|**LAST_ONLINE_TIME**|A última vez em quando escala Out mestre está online.|
|**MACHINE_IP**|O IP da máquina.|
|**NOME_DO_COMPUTADOR**|O nome do computador.|
|**MASTER_ADDRESS**|O ponto de extremidade de escala Out mestre.|
|**MASTER_SERVICE_PORT**|A porta no ponto de extremidade de escala Out mestre.|
|**SSLCERT_THUMBPRINT**|A impressão digital do certificado de escala Out mestre.|

## <a name="permissions"></a>Permissões
Todos os membros da função de banco de dados público de tem permissão para este modo de exibição de leitura. 

