---
title: sys.DM external_script_requests | Microsoft Docs
ms.custom: ''
ms.date: 06/24/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_external_script_requests
- sys.dm_external_script_requests_TSQL
- dm_external_script_requests
- dm_external_script_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_external_script_requests dynamic management view
ms.assetid: e7e7c50f-b8b2-403c-b8c8-1955da5636c3
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bc6db4816e4ba890e132600874d5db21aa190c02
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmexternalscriptrequests"></a>sys.dm_external_script_requests
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Retorna uma linha para cada conta de trabalho ativa que executa um script externo.
 
  
> [!NOTE] 
>  
>  Essa DMV estará disponível somente se você tiver instalado e habilitado o recurso que dá suporte à execução de script externo. Para obter informações sobre como fazer isso para scripts do R, consulte [Configurar o SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|external_script_request_id|**Identificador exclusivo**|ID do processo que enviou a solicitação de script externo. Isso corresponde à ID de processo como recebidas por [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]|  
|language|**nvarchar**|Palavra-chave que representa uma linguagem de script com suporte. Atualmente, há suporte apenas para `R` .|  
|degree_of_parallelism|**Int**|Número que indica o número de processos paralelos que foram criados. Esse valor pode ser diferente do número de processos paralelos solicitados.|  
|external_user_name|**nvarchar**|A conta de trabalho do Windows na qual o script foi executado.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STATE no servidor.  
  
> [!NOTE]
>   
>  Os usuários que executam scripts externos devem ter a permissão adicional EXECUTE ANY EXTERNAL SCRIPT; no entanto, essa DMV pode ser usada por administradores sem essa permissão. 
  
## <a name="remarks"></a>Remarks  

Esta exibição pode ser filtrada usando o identificador de linguagem de script.

A exibição também retorna a conta de trabalho na qual o script está sendo executado. Para obter informações sobre as contas de trabalho usadas pelos scripts do R, consulte [Modificar o pool de contas de usuário para o R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).

O GUID retornado no campo **external_script_request_id** também representa o nome do arquivo do diretório seguro no qual os arquivos temporários são armazenados. Cada conta de trabalho, como MSSQLSERVER01, representa um único logon SQL ou usuário do Windows, e pode ser usado para executar várias solicitações de script. Por padrão, esses arquivos temporários são removidos após a conclusão do script solicitado. Se você precisar preservar esses arquivos por um período para fins de depuração, você poderá alterar o sinalizador de limpeza, conforme descrito neste tópico: [Configurar e gerenciar Extensões de Análise Avançada](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md).  
 
Essa DMV monitora apenas os processos ativos e não pode relatar scripts que já foram concluídos. Se você precisar controlar a duração de scripts, recomendamos que você adicione informações de tempo no script e capture-o como parte da execução do script.


## <a name="examples"></a>Exemplos  
  
### <a name="viewing-the-currently-active-r-scripts-for-a-particular-process"></a>Exibindo os scripts do R ativos no momento de um processo específico 
 O exemplo a seguir exibe o número de execuções de script externo executadas na instância atual.  
  
```  
SELECT external_script_request_id 
  , [language]
  , degree_of_parallelism
  , external_user_name
FROM sys.dm_external_script_requests; 
```  

Resultados  


external_script_request_id  |language  |degree_of_parallelism  |external_user_name  
---------|---------|---------|---------
183EE6FC-7399-4318-AA2E-7A6C68E435A8     |     R    |      1   |  MSSQLSERVER01       


  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)
[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  

