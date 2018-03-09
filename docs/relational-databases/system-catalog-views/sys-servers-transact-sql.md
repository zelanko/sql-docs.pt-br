---
title: sys (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- servers_TSQL
- sys.servers_TSQL
- servers
- sys.servers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.servers catalog view
ms.assetid: 4e774ed9-4e83-4726-9f1d-8efde8f9feff
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 858fe45f817572eea387ce3971a52e72cc23f045
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysservers-transact-sql"></a>sys.servers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada servidor vinculado ou remoto registrado e uma linha para o servidor local que tenha **server_id** = 0.  
  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|ID local do servidor vinculado.|  
|**name**|**sysname**|Quando **server_id** = 0, este é o nome do servidor.<br /><br /> Quando **server_id** > 0, este é o nome local do servidor vinculado.|  
|**product**|**sysname**|Nome de produto do servidor vinculado. "SQL Server" indica que esta é outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**provedor**|**sysname**|Nome do provedor OLE DB para conectar o servidor vinculado.|  
|**data_source**|**nvarchar(4000)**|Propriedade de conexão da fonte de dados OLE DB.|  
|**local**|**nvarchar(4000)**|Propriedade de conexão local OLE DB. NULL se nenhum.|  
|**provider_string**|**nvarchar(4000)**|Propriedade de conexão da cadeia de caracteres de provedor OLE DB.<br /><br /> É NULL, exceto se o chamador tiver a permissão ALTER ANY LINKED SERVER.|  
|**Catálogo**|**sysname**|Propriedade de conexão do catálogo OLEDB. NULL se nenhum.|  
|**connect_timeout**|**int**|Tempo de limite de conexão em segundos, 0 se nenhum.|  
|**query_timeout**|**int**|Tempo de limite  de consulta em segundos, 0 se nenhum.|  
|**is_linked**|**bit**|0 = é um servidor de estilo antigo adicionado usando **sp_addserver**com RPC diferente e o comportamento de transação distribuída.<br /><br /> 1 = Servidor vinculado padrão.|  
|**is_remote_login_enabled**|**bit**|Opção RPC está configurado para permitir logons remotos de entrada para este servidor.|  
|**is_rpc_out_enabled**|**bit**|RPC de saída (deste servidor) está habilitado.|  
|**is_data_access_enabled**|**bit**|Servidor está habilitado para consultas distribuídas.|  
|**is_collation_compatible**|**bit**|Assume-se que o agrupamento de dados remotos é compatível com dados locais, caso nenhuma informação sobre agrupamento estiver disponível.|  
|**uses_remote_collation**|**bit**|Se 1, use o agrupamento informado pelo servidor remoto; caso contrário, use o agrupamento especificado pela coluna seguinte.|  
|**collation_name**|**sysname**|Nome do agrupamento a ser usado, ou NULL para uso apenas local.|  
|**lazy_schema_validation**|**bit**|Se 1, a validação de esquema não é verificada na inicialização de consulta.|  
|**is_system**|**bit**|Esse servidor só pode ser acessado pelo sistema interno.|  
|**is_publisher**|**bit**|Servidor é um Publicador de replicação.|  
|**is_subscriber**|**bit**|Servidor é um Assinante de replicação.|  
|**is_distributor**|**bit**|Servidor é um Distribuidor de replicação.|  
|**is_nonsql_subscriber**|**bit**|Servidor não é um Assinante de replicação.|  
|**is_remote_proc_transaction_promotion_enabled**|**bit**|Se 1, chamando um procedimento armazenado remoto dará início a uma transação distribuída e inscrever a transação com o MS DTC. Para obter mais informações, consulte [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md).|  
|**modify_date**|**datetime**|Data em que as informações do servidor foram alteradas pela última vez.|  
  
## <a name="permissions"></a>Permissões  
 O valor em **provider_string** é sempre NULL, a menos que o chamador tenha a permissão ALTER ANY LINKED SERVER.  
  
 Não são necessárias permissões para exibir o servidor local (**server_id** = 0).  
  
 Quando você cria um servidor vinculado ou remoto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria um mapeamento de logon padrão para o **pública** função de servidor. Isso significa que, por padrão, todos os logons podem enxergar todos os servidores remotos e vinculados. Para restringir a visibilidade a estes servidores, remova o mapeamento de logon padrão executando [sp_droplinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md) e especificando NULL para o *locallogin* parâmetro.  
  
 Se o mapeamento padrão de logon for excluído, só usuários que foram adicionados explicitamente como um logon vinculado ou um logon remoto pode enxergar os servidores remotos e vinculados para os quais eles têm um logon. Para exibir todos os servidores vinculados e remotos, depois que o mapeamento de logon padrão for excluído requer as seguintes permissões:  
  
-   ALTER ANY LINKED SERVER ou ALTER ANY LOGIN ON SERVER  
  
-   Associação de **setupadmin** ou **sysadmin** funções de servidor fixas  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de servidores vinculados &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)  
  
  
