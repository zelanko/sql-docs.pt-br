---
title: Catalog. Operations (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- operations view [Integration Services]
- catalog.operations view [Integration Services]
ms.assetid: 9455c5b1-60ff-45fc-8599-cc3abbd6daf5
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f9d1969e9fe7bcb2104003cfab057effcd35da5d
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogoperations-ssisdb-database"></a>catalog.operations (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe os detalhes de todas as operações no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|operation_id|**bigint**|O ID (identificador exclusivo) da operação.|  
|operation_type|**smallint**|O tipo de operação.|  
|created_time|**datetimeoffset**|A hora em que a operação foi criada.|  
|object_type|**smallint**|O tipo de objeto afetado pela operação. O objeto pode ser uma pasta (`10`), um projeto (`20`), um pacote (`30`), um ambiente (`40`) ou uma instância de execução (`50`).|  
|object_id|**bigint**|A ID do objeto afetado pela operação.|  
|object_name|**nvarchar (260)**|O nome do objeto.|  
|status|**int**|O status da operação. Os possíveis valores são criado (`1`), em execução (`2`), cancelado (`3`), com falha (`4`), pendente (`5`), encerrado inesperadamente (`6`), êxito (`7`), parando (`8`) e concluído (`9`).|  
|start_time|**datetimeoffset**|A hora de início da operação.|  
|end_time|**datetimeoffsset**|A hora em que a operação é concluída.|  
|caller_sid|**varbinary(85)**|O SID (identificador de segurança) do usuário se a Autenticação do Windows tiver sido usada para fazer logon.|  
|caller_name|**nvarchar (128)**|O nome da conta que executou a operação.|  
|process_id|**int**|A ID de processo do processo externo, se aplicável.|  
|stopped_by_sid|**varbinary(85)**|O SID do usuário que interrompeu a operação.|  
|stopped_by_name|**nvarchar (128)**|O nome do usuário que interrompeu a operação.|  
|server_name|**nvarchar (128)**|As informações do servidor e da instância do Windows de uma instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|machine_name|**nvarchar (128)**|O nome do computador no qual a instância de servidor está sendo executada.|  
  
## <a name="remarks"></a>Comentários  
 Essa exibição mostra uma linha para cada operação no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Permite que o administrador enumere todas as operações lógicas que foram executadas no servidor, como implantar um projeto ou executar um pacote.  
  
 Este modo exibe os seguintes tipos de operação, conforme listado no **operation_type** coluna:  
  
|**operation_type** valor|**operation_type** descrição|**object_id** descrição|**object_name** descrição|  
|-------------------------------|-------------------------------------|--------------------------------|----------------------------------|  
|`1`|Inicialização [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|**NULL**|**NULL**|  
|`2`|Janela de retenção<br /><br /> (trabalho do SQL Agent)|**NULL**|**NULL**|  
|`3`|MaxProjectVersion<br /><br /> (trabalho do SQL Agent)|**NULL**|**NULL**|  
|`101`|**deploy_project**<br /><br /> (Procedimento armazenado)|Project ID|Nome do projeto|  
|`106`|**restore_project**<br /><br /> (Procedimento armazenado)|Project ID|Nome do projeto|  
|`200`|**create_execution** e **start_execution**<br /><br /> (Procedimentos armazenados)|Project ID|**NULL**|  
|`202`|**stop_operation**<br /><br /> (Procedimento armazenado)|Project ID|**NULL**|  
|`300`|**validate_project**<br /><br /> (Procedimento armazenado)|Project ID|Nome do projeto|  
|`301`|**validate_package**<br /><br /> (Procedimento armazenado)|Project ID|Nome do pacote|  
|`1000`|**configure_catalog**<br /><br /> (Procedimento armazenado)|**NULL**|**NULL**||  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na operação  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  

