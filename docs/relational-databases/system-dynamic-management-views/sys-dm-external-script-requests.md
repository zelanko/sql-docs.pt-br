---
title: sys.dm_external_script_requests | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 70f1024f73ff955facaa2b6a2af2b9f5f4ccf247
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488195"
---
# <a name="sysdm_external_script_requests"></a>sys.dm_external_script_requests
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Retorna uma linha para cada conta de trabalho ativa que executa um script externo.
  
> [!NOTE] 
>  
> Essa visão de gerenciamento dinâmico (Detran) só está disponível se você tiver instalado e habilitado o recurso que suporta a execução de script externo. Para obter mais informações, consulte [Serviços R no SQL Server 2016](../../machine-learning/r/sql-server-r-services.md) e [Serviços de Aprendizado de Máquina (R, Python) no SQL Server 2017 e posteriores](../../machine-learning/sql-server-machine-learning-services.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|external_script_request_id|**identificador exclusivo**|ID do processo que enviou a solicitação de script externo. Isso corresponde ao ID do processo recebido por[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]|  
|Linguagem|**nvarchar**|Palavra-chave que representa uma linguagem de script com suporte. |  
|degree_of_parallelism|**int**|Número que indica o número de processos paralelos que foram criados. Esse valor pode ser diferente do número de processos paralelos solicitados.|  
|external_user_name|**nvarchar**|A conta de trabalho do Windows na qual o script foi executado.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STATE no servidor.  
  
> [!NOTE]
>   
>  Os usuários que executam scripts externos devem ter a permissão adicional EXECUTE ANY EXTERNAL SCRIPT; no entanto, essa DMV pode ser usada por administradores sem essa permissão. 
  
## <a name="remarks"></a>Comentários  

Esta exibição pode ser filtrada usando o identificador de linguagem de script.

A exibição também retorna a conta de trabalho na qual o script está sendo executado. Para obter informações sobre contas de trabalhadores usadas pelos scripts externos, consulte a seção Identidades usadas no processamento (SQLRUserGroup) na [visão geral de segurança para a estrutura de extensibilidade no SQL Server Machine Learning Services](../../machine-learning/concepts/security.md#sqlrusergroup).

O GUID retornado no campo **external_script_request_id** também representa o nome do arquivo do diretório seguro no qual os arquivos temporários são armazenados. Cada conta de trabalho, como MSSQLSERVER01, representa um único logon SQL ou usuário do Windows, e pode ser usado para executar várias solicitações de script. Por padrão, esses arquivos temporários são removidos após a conclusão do script solicitado.
 
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


external_script_request_id  |Linguagem  |degree_of_parallelism  |external_user_name  
---------|---------|---------|---------
183EE6FC-7399-4318-AA2E-7A6C68E435A8     |     R    |      1   |  MSSQLSERVER01       


  
## <a name="see-also"></a>Consulte Também  
 [Visualizações e funções de gerenciamento dinâmico &#40;transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)
[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  

