---
description: catalog.executions (Banco de Dados SSISDB)
title: catalog.executions (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- executions view [Integration Services]
- catalog.executions view [Integration Services]
ms.assetid: 879f13b0-331d-4dee-a079-edfaca11ae5b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 438d551f45447b0b03b075576af9cffb2bde8a36
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425098"
---
# <a name="catalogexecutions-ssisdb-database"></a>catalog.executions (Banco de Dados SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe as instâncias de execução de pacote no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Pacotes que são executados com a tarefa Executar Pacote na mesma instância de execução que o pacote pai.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|execution_id|**bigint**|O identificador global (ID) exclusivo da instância de execução.|  
|folder_name|**sysname(nvarchar(128))**|O nome da pasta que contém o projeto.|  
|project_name|**sysname(nvarchar(128))**|O nome do projeto.|  
|package_name|**nvarchar(260)**|O nome do primeiro pacote que foi iniciado durante a execução.|  
|reference_id|**bigint**|O ambiente referenciado pela instância de execução.|  
|reference_type|**char(1)**|Indica se o ambiente pode ser localizado na mesma pasta do projeto (referência relativa) ou em uma pasta diferente (referência absoluta). Quando o valor for `R`, o ambiente será localizado por meio de uma referência relativa. Quando o valor for `A`, o ambiente será localizado por meio de uma referência absoluta.|  
|environment_folder_name|**nvarchar(128)**|O nome da pasta que contém o ambiente.|  
|environment_name|**nvarchar(128)**|O nome do ambiente que foi referenciado durante a execução.|  
|project_lsn|**bigint**|A versão do projeto que corresponde à instância da execução. Não há garantia de que este número seja sequencial.|  
|executed_as_sid|**varbinary(85)**|A SID do usuário que iniciou a instância da execução.|  
|executed_as_name|**nvarchar(128)**|O nome da entidade do banco de dados que foi usada para iniciar a instância de execução.|  
|use32bitruntime|**bit**|Indica se o runtime de 32 bits é usado para executar o pacote em um sistema operacional de 64 bits. Quando o valor é `1`, a execução é realizada com o runtime de 32 bits. Quando o valor é `0`, a execução é realizada com o runtime de 64 bits.|  
|object_type|**smallint**|O tipo de objeto. O objeto pode ser um projeto (`20`) ou um pacote (`30`).|  
|object_id|**bigint**|A ID do objeto afetado pela operação.|  
|status|**int**|O status da operação. Os possíveis valores são criado (`1`), em execução (`2`), cancelado (`3`), com falha (`4`), pendente (`5`), encerrado inesperadamente (`6`), êxito (`7`), parando (`8`) e concluído (`9`).|  
|start_time|**datetimeoffset**|A hora em que a instância da execução foi iniciada.|  
|end_time|**datetimeoffsset**|A hora em que a instância da execução foi finalizada.|  
|caller_sid|**varbinary(85)**|O SID (identificador de segurança) do usuário se a Autenticação do Windows tiver sido usada para fazer logon.|  
|caller_name|**nvarchar(128)**|O nome da conta que executou a operação.|  
|process_id|**int**|A ID de processo do processo externo, se aplicável.|  
|stopped_by_sid|**varbinary(85)**|O SID (Identificador de Segurança) do usuário que interrompeu a instância de execução.|  
|stopped_by_name|**nvarchar(128)**|O nome do usuário que parou a instância da execução.|  
|total_physical_memory_kb|**bigint**|O total da memória física (em megabytes) no servidor quando a execução é iniciada.|  
|available_physical_memory_kb|**bigint**|A memória física disponível (em megabytes) no servidor quando a execução é iniciada.|  
|total_page_file_kb|**bigint**|O total da memória de páginas (em megabytes) no servidor quando a execução é iniciada.|  
|available_page_file_kb|**bigint**|A memória de páginas disponível (em megabytes) no servidor quando a execução é iniciada.|  
|cpu_count|**int**|O número de CPUs lógicas no servidor quando a execução é iniciada.|  
|server_name|**nvarchar(128)**|As informações do servidor e da instância do Windows de uma instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|machine_name|**nvarchar(128)**|O nome do computador no qual a instância de servidor está sendo executada.|  
|dump_id|**uniqueidentifier**|A ID de um despejo de execução.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição mostra uma linha para cada instância de execução no catálogo.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na instância de execução  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
