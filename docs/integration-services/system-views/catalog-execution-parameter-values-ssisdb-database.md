---
title: Catalog. execution_parameter_values (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: ec93e67b-04ce-4aae-ab96-3ad20e9793ad
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 60907a82f3d0bb9f273355fd6bfbd7378ce72c9f
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexecutionparametervalues-ssisdb-database"></a>catalog.execution_parameter_values (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe os valores de parâmetros reais que são usados por pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] durante uma instância de execução.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|execution_parameter_id|**bigint**|ID (identificador exclusivo) do parâmetro de execução.|  
|execution_id|**bigint**|ID exclusivo da instância de execução.|  
|object_type|**smallint**|Quando o valor é `20`, o parâmetro é um parâmetro do projeto. Quando o valor é `30`, o parâmetro é um parâmetro do pacote. Quando o valor for `50`, o parâmetro é um dos seguintes:<br /><br /> **LOGGING_LEVEL**<br /><br /> **DUMP_ON_ERROR**<br /><br /> **DUMP_ON_EVENT**<br /><br /> **DUMP_EVENT_CODE**<br /><br /> **CALLER_INFO**<br /><br /> **SINCRONIZADO**|  
|parameter_data_type|**nvarchar (128)**|O tipo de dados do parâmetro.|  
|parameter_name|**sysname**|O nome do parâmetro.|  
|parameter_value|**sql_variant**|O valor do parâmetro. Quando confidenciais é `0`, o valor de texto sem formatação é mostrado. Quando confidenciais é `1`, o **nulo** valor é exibido.|  
|sensitive|**bit**|Quando o valor é `1`, o valor do parâmetro é confidencial. Quando o valor é `0`, o valor do parâmetro não é confidencial.|  
|required|**bit**|Quando o valor é `1`, o valor do parâmetro é necessário para iniciar a execução. Quando o valor é `0`, o valor de parâmetro não é necessário para iniciar a execução.|  
|value_set|**bit**|Quando o valor é `1`, o valor do parâmetro foi atribuído. Quando o valor é `0`, o valor do parâmetro não foi atribuído.|  
|runtime_override|**bit**|Quando o valor é `1`, o valor do parâmetro foi alterado em relação ao valor original antes do início da execução. Quando o valor é `0`, o valor do parâmetro é o valor original que foi definido.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição mostra uma linha para cada parâmetro de execução no catálogo. Um valor de parâmetro de execução é o valor atribuído a um parâmetro de projeto ou parâmetro de pacote durante uma única instância de execução.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na instância de execução  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  

