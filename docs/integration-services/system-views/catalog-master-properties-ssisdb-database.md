---
title: catalog.master_properties (Banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c48f9e25d0a662f5f1f756b16b7f3edbe361de29
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="catalogmasterproperties-ssisdb-database"></a>catalog.master_properties (Banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Exibe as propriedades do Mestre do Scale Out [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|O nome da propriedade mestre de expansão.|  
|property_value|**nvarchar(max)**|O valor da propriedade mestre de expansão.|

## <a name="remarks"></a>Remarks
Esta exibição mostra uma linha para cada propriedade mestre de expansão. As propriedades mostradas por esta exibição incluem o seguinte:

|Nome da propriedade|Description|  
|-------------------|-----------------| 
|**CLUSTER_LOGDB_SERVER**|O SQL Server no qual banco de dados está localizado.|
|**LAST_ONLINE_TIME**|A última vez em que o Mestre do Scale Out esteve online.|
|**MACHINE_IP**|O IP do computador.|
|**MACHINE_NAME**|O nome do computador.|
|**MASTER_ADDRESS**|O ponto de extremidade do Mestre do Scale Out.|
|**MASTER_SERVICE_PORT**|A porta no ponto de extremidade do Mestre do Scale Out.|
|**SSLCERT_THUMBPRINT**|A impressão digital do certificado do Mestre do Scale Out.|

## <a name="permissions"></a>Permissões
Todos os membros da função de banco de dados público têm permissão de leitura para esta exibição. 
