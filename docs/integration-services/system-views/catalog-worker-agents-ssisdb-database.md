---
title: catalog.worker_agents (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 198f730938d316a97948c51c893a5e651733ef64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997787"
---
# <a name="catalogworkeragents-ssisdb-database"></a>catalog.worker_agents (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Exibe as informações do Trabalho do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out.

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|A ID do agente de trabalho do Trabalhador do Scale Out.|
|IsEnabled|**bit**|Se o Trabalho do Scale Out está habilitado.|
|DisplayName|**nvarchar(256)**|O nome de exibição do Trabalho do Scale Out.|
|Descrição|**nvarchar(256)**|A descrição do Trabalho do Scale Out.|
|MachineName|**nvarchar(256)**|O nome do computador do Trabalho do Scale Out.|
|Marcas|**nvarchar(max)**|As marcas do Trabalho do Scale Out.|
|UserAccount|**nvarchar(256)**|A conta de usuário que executa o serviço Trabalho do Scale Out.|
|LastOnlineTime|**datetimeoffset(7)**|A última vez em que o Trabalho do Scale Out esteve online.|

## <a name="remarks"></a>Remarks
Essa exibição mostra uma linha para cada Trabalho do Scale Out se conectando ao Mestre do Scale Out trabalhando com o catálogo do SSISDB.

## <a name="permissions"></a>Permissões
Esta exibição requer uma das seguintes permissões:

- Associação à função de banco de dados **ssis_admin**

- Associação à função de banco de dados **ssis_cluster_executor**

- Associação à função de servidor **sysadmin**
