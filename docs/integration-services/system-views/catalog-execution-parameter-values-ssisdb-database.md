---
description: catalog.execution_parameter_values (Banco de Dados SSISDB)
title: catalog.execution_parameter_values (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: ec93e67b-04ce-4aae-ab96-3ad20e9793ad
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 022d1d29438da9bebeb7e7544b01445f27803fce
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495205"
---
# <a name="catalogexecution_parameter_values-ssisdb-database"></a>catalog.execution_parameter_values (Banco de Dados SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe os valores de parâmetros reais que são usados por pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] durante uma instância de execução.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|execution_parameter_id|**bigint**|ID (identificador exclusivo) do parâmetro de execução.|  
|execution_id|**bigint**|ID exclusivo da instância de execução.|  
|object_type|**smallint**|Quando o valor é `20`, o parâmetro é um parâmetro do projeto. Quando o valor é `30`, o parâmetro é um parâmetro do pacote. Quando o valor é `50`, o parâmetro é um dos apresentados a seguir:<br /><br /> **LOGGING_LEVEL**<br /><br /> **DUMP_ON_ERROR**<br /><br /> **DUMP_ON_EVENT**<br /><br /> **DUMP_EVENT_CODE**<br /><br /> **CALLER_INFO**<br /><br /> **SYNCHRONIZED**|  
|parameter_data_type|**nvarchar(128)**|O tipo de dados do parâmetro.|  
|parameter_name|**sysname**|O nome do parâmetro.|  
|parameter_value|**sql_variant**|O valor do parâmetro. Quando sensitive é `0`, o valor do texto sem formatação é mostrado. Quando sensitive é `1`, o valor **NULL** é exibido.|  
|sensitive|**bit**|Quando o valor é `1`, o valor do parâmetro é confidencial. Quando o valor é `0`, o valor do parâmetro não é confidencial.|  
|exigido|**bit**|Quando o valor é `1`, o valor do parâmetro é necessário para iniciar a execução. Quando o valor é `0`, o valor de parâmetro não é necessário para iniciar a execução.|  
|value_set|**bit**|Quando o valor é `1`, o valor do parâmetro foi atribuído. Quando o valor é `0`, o valor do parâmetro não foi atribuído.|  
|runtime_override|**bit**|Quando o valor é `1`, o valor do parâmetro foi alterado em relação ao valor original antes do início da execução. Quando o valor é `0`, o valor do parâmetro é o valor original que foi definido.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição mostra uma linha para cada parâmetro de execução no catálogo. Um valor de parâmetro de execução é o valor atribuído a um parâmetro de projeto ou parâmetro de pacote durante uma única instância de execução.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na instância de execução  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
