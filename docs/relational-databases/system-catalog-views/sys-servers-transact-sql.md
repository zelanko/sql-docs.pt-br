---
title: sys. Servers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: c4b141520b21902c4dadb26a3ac013b1ee334928
ms.sourcegitcommit: 9a0824aa9bf54b24039c6a533d11474cfb5423ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/16/2020
ms.locfileid: "84818214"
---
# <a name="sysservers-transact-sql"></a>sys.servers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Contém uma linha por servidor vinculado ou remoto registrada e uma linha para o servidor local que tem **server_id** = 0.  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|ID local do servidor vinculado.|  
|**name**|**sysname**|Quando **server_id** = 0, o valor retornado é o nome do servidor.<br /><br /> Quando **server_id** > 0, o valor retornado é o nome local do servidor vinculado.|  
|**remessa**|**sysname**|Nome de produto do servidor vinculado. Um valor de "SQL Server" indica outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**operador**|**sysname**|Nome do provedor OLE DB para conectar o servidor vinculado.|  
|**data_source**|**nvarchar(4000)**|Propriedade de conexão da fonte de dados OLE DB.|  
|**local**|**nvarchar(4000)**|Propriedade de conexão local OLE DB. NULL se nenhum.|  
|**provider_string**|**nvarchar(4000)**|Propriedade de conexão da cadeia de caracteres de provedor OLE DB.<br /><br /> É NULL, exceto se o chamador tiver a permissão ALTER ANY LINKED SERVER.|  
|**Catalog**|**sysname**|Propriedade de conexão do catálogo OLEDB. NULL se nenhum.|  
|**connect_timeout**|**int**|Tempo de limite de conexão em segundos, 0 se nenhum.|  
|**query_timeout**|**int**|Tempo de limite  de consulta em segundos, 0 se nenhum.|  
|**is_linked**|**bit**|0 = é um servidor de estilo antigo adicionado usando **sp_addserver**, com comportamento de RPC e de transação distribuída diferente.<br /><br /> 1 = Servidor vinculado padrão.|  
|**is_remote_login_enabled**|**bit**|Opção RPC está configurado para permitir logons remotos de entrada para este servidor.|  
|**is_rpc_out_enabled**|**bit**|RPC de saída (deste servidor) está habilitado.|  
|**is_data_access_enabled**|**bit**|Servidor está habilitado para consultas distribuídas.|  
|**is_collation_compatible**|**bit**|Assume-se que a ordenação de dados remotos é compatível com dados locais, caso nenhuma informação sobre ordenação estiver disponível.|  
|**uses_remote_collation**|**bit**|Se 1, use a ordenação informada pelo servidor remoto; caso contrário, use a ordenação especificada pela coluna seguinte.|  
|**collation_name**|**sysname**|Nome da ordenação a ser usado, ou NULL para uso apenas local.|  
|**lazy_schema_validation**|**bit**|Se 1, a validação de esquema não é verificada na inicialização de consulta.|  
|**is_system**|**bit**|Esse servidor só pode ser acessado pelo sistema interno.|  
|**is_publisher**|**bit**|Servidor é um Publicador de replicação.|  
|**is_subscriber**|**bit**|Servidor é um Assinante de replicação.|  
|**is_distributor**|**bit**|Servidor é um Distribuidor de replicação.|  
|**is_nonsql_subscriber**|**bit**|Servidor não é um Assinante de replicação.|  
|**is_remote_proc_transaction_promotion_enabled**|**bit**|Se 1, chamando um procedimento armazenado remoto dará início a uma transação distribuída e inscrever a transação com o MS DTC. Para obter mais informações, consulte [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md).|  
|**modify_date**|**datetime**|Data em que as informações do servidor foram alteradas pela última vez.|  
|**is_rda_server**|**bit**|O servidor é o arquivo morto de dados remotos habilitar (habilitado para Stretch). Para obter mais informações, consulte [habilitar Stretch Database no servidor](https://docs.microsoft.com/sql/sql-server/stretch-database/enable-stretch-database-for-a-database#EnableTSQLServer). Aplica-se a SQL Server 2016 e mais recente.|
  
## <a name="permissions"></a>Permissões  
 O valor em **provider_string** é sempre nulo, a menos que o chamador tenha a permissão ALTER ANY linkd Server.  
  
 Não são necessárias permissões para exibir o servidor local (**server_id** = 0).  
  
 Quando você cria um servidor vinculado ou remoto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o cria um mapeamento de logon padrão para a função de servidor **público** . O mapeamento de logon padrão significa que todos os logons podem exibir todos os servidores vinculados e remotos. Para restringir a visibilidade para esses servidores, remova o mapeamento de logon padrão executando [sp_droplinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md) e especificando NULL para o parâmetro *locallogin* .  
  
 Se o mapeamento padrão de logon for excluído, só usuários que foram adicionados explicitamente como um logon vinculado ou um logon remoto pode enxergar os servidores remotos e vinculados para os quais eles têm um logon.  As permissões a seguir são necessárias para exibir todos os servidores vinculados e remotos após o mapeamento de logon padrão:  
  
- `ALTER ANY LINKED SERVER` ou `ALTER ANY LOGIN ON SERVER`  
- Associação nas funções de servidor fixas **setupadmin** ou **sysadmin**  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de servidores vinculados &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addlinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)  
  
  
