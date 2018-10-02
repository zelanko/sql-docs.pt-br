---
title: catalog.master_properties (Banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 85b3388be32ac33382ad34f12ec135e84313cb33
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687434"
---
# <a name="catalogmasterproperties-ssisdb-database"></a>catalog.master_properties (Banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Exibe as propriedades do Mestre do Scale Out [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|O nome da propriedade mestre de expansão.|  
|property_value|**nvarchar(max)**|O valor da propriedade mestre de expansão.|

## <a name="remarks"></a>Remarks
Esta exibição mostra uma linha para cada propriedade mestre de expansão. As propriedades mostradas por esta exibição incluem o seguinte:

|Nome da propriedade|Descrição|  
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
