---
title: catalog.execution_data_taps | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 54226c01-5b8f-4730-8a5f-1da2613f9689
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 582c0554d7ffab10ee65bf74ecdb50e72169dd24
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="catalogexecutiondatataps"></a>catalog.execution_data_taps
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe informações para cada toque de dados definido em uma execução.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|data_tap_id|**bigint**|O ID (identificador exclusivo) do toque de dados.|  
|execution_id|**bigint**|O ID (identificador exclusivo) da instância de execução.|  
|package_path|**nvarchar(max)**|O caminho do pacote da tarefa de fluxo de dados, onde os dados são tocados.|  
|dataflow_path_id_string|**nvarchar(4000)**|A cadeia de caracteres de identificação do caminho de fluxo de dados.|  
|dataflow_task_guid|**uniqueidentifier**|O ID da tarefa de fluxo de dados.|  
|max_rows|**int**|O número de linhas a serem capturadas. Se esse valor não for especificado, todas as linhas serão capturadas.|  
|filename|**nvarchar(4000)**|O nome do arquivo de despejo de dados. Para obter mais informações, consulte [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).|  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na instância de execução  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerar arquivos de despejo para execução de pacote](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
