---
title: catalog.extended_operation_info (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: db299b45-557d-4c62-8e14-355cdb051f63
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ca82bdc8a04ffee4426ffb934a9e9a4ddaf4654f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296605"
---
# <a name="catalogextended_operation_info-ssisdb-database"></a>catalog.extended_operation_info (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe informações estendidas de todas as operações no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|info_id|**bigint**|O identificador exclusivo (ID) da informação estendida.|  
|operation_id|**bigint**|A ID exclusiva da operação que corresponde à informação estendida.|  
|object_name|**nvarchar(260)**|O nome do objeto.|  
|object_type|**smallint**|O tipo de objeto afetado pela operação. O objeto pode ser uma pasta (`10`), um projeto (`20`), um pacote (`30`), um ambiente (`40`) ou uma instância de execução (`50`).|  
|reference_id|**bigint**|A ID exclusiva da referência usada na operação.|  
|status|**int**|O status da operação. Os possíveis valores são criado (`1`), em execução (`2`), cancelado (`3`), com falha (`4`), pendente (`5`), encerrado inesperadamente (`6`), êxito (`7`), parando (`8`) e concluído (`9`).|  
|start_time|**datetimeoffset(7)**|A data e a hora de início da operação.|  
|end_time|**datetimeoffset(7)**|A data e a hora de término da operação.|  
  
## <a name="remarks"></a>Comentários  
 Uma única operação pode ter várias linhas de informações estendidas.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na operação  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
