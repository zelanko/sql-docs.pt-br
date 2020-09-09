---
description: MSsubscription_properties (Transact-SQL)
title: MSsubscription_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_properties
- MSsubscription_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_properties system table
ms.assetid: f96fc1ae-b798-4b05-82a7-564ae6ef23b8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8895f78aa31e5fa38b52de7163ddb2a1554e5617
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545506"
---
# <a name="mssubscription_properties-transact-sql"></a>MSsubscription_properties (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSsubscription_properties** contém linhas para as informações de parâmetro necessárias para executar agentes de replicação no Assinante. Essa tabela é armazenada no banco de dados de assinatura para uma assinatura pull e no banco de dados de distribuição, no Distribuidor, para uma assinatura push.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**programa**|**sysname**|O nome do Publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**documento**|**sysname**|O nome da publicação.|  
|**publication_type**|**int**|O tipo de publicação:<br /><br /> **0** = transacional.<br /><br /> **2** = mesclar.|  
|**publisher_login**|**sysname**|A ID do logon usada no Publicador para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**publisher_password**|**nvarchar (524)**|A senha (criptografada) usada no Publicador para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**publisher_security_mode**|**int**|O modo de segurança implementado no Publicador.<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server autenticação.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticação do Windows.<br /><br /> **2** = os gatilhos de sincronização usam uma entrada **sysservers** estática para fazer uma chamada de procedimento remoto (RPC) e o *Publicador* deve ser definido na tabela **sysservers** como um servidor remoto ou servidor vinculado.|  
|**distribuidor**|**sysname**|O nome do Distribuidor.|  
|**distributor_login**|**sysname**|A ID de logon usada no Distribuidor para Autenticação do SQL Server.|  
|**distributor_password**|**nvarchar (524)**|A senha (criptografada) usada no Distribuidor para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**distributor_security_mode**|**int**|O modo de segurança implementado no Distribuidor.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.<br /><br /> **1** = autenticação do Windows.|  
|**ftp_address**|**sysname**|O endereço de rede do serviço FTP (File Transfer Protocol) para o Distribuidor.|  
|**ftp_port**|**int**|O número da porta do serviço FTP do Distribuidor.|  
|**ftp_login**|**sysname**|O nome de usuário usado para se conectar ao serviço FTP.|  
|**ftp_password**|**nvarchar (524)**|A senha de usuário usada para se conectar ao serviço FTP.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Especifica o local da pasta alternativa para o instantâneo.|  
|**working_directory**|**nvarchar(255)**|O nome do diretório de trabalho usado para armazenar dados e arquivos de esquema.|  
|**use_ftp**|**bit**|Especifica o uso do FTP em vez do protocolo regular para recuperar instantâneos. Se for **1**, o FTP será usado.|  
|**dts_package_name**|**sysname**|Especifica o nome do pacote DTS (Data Transformation Services).|  
|**dts_package_password**|**nvarchar (524)**|Especifica a senha no pacote.|  
|**dts_package_location**|**int**|O local onde o pacote DTS é armazenado.|  
|**enabled_for_syncmgr**|**bit**|Especifica se a assinatura pode ou não ser sincronizada pelo Gerenciador de Sincronização da [!INCLUDE[msCoName](../../includes/msconame-md.md)].<br /><br /> **0** = a assinatura não está registrada com o Gerenciador de sincronização.<br /><br /> **1** = a assinatura é registrada com o Gerenciador de sincronização e pode ser sincronizada sem iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .|  
|**offload_agent**|**bit**|Especifica se o agente pode ser ativado remotamente ou não. Se for **0**, o agente não poderá ser ativado remotamente.|  
|**offload_server**|**sysname**|Especifica o nome da rede do servidor usado para ativação remota.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Especifica o caminho para a pasta onde os arquivos de instantâneo são salvos.|  
|**use_web_sync**|**bit**|Especifica se a assinatura pode ser sincronizada pelo HTTP ou não. Um valor de **1** significa que esse recurso está habilitado.|  
|**internet_url**|**nvarchar(260)**|O URL que representa o local do Replication Listener para sincronização da Web.|  
|**internet_login**|**sysname**|O logon que o Agente de Mesclagem usa ao se conectar ao servidor Web que está hospedando a sincronização da Web usando a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação do.|  
|**internet_password**|**nvarchar (524)**|A senha para o logon que o Agente de Mesclagem usa ao se conectar ao servidor Web que está hospedando a sincronização da Web usando a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação do.|  
|**internet_security_mode**|**int**|O modo de autenticação usado durante a conexão com o servidor Web que está hospedando a sincronização da Web, em que o valor **1** significa autenticação do Windows e um valor de **0** significa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.|  
|**internet_timeout**|**int**|O período de tempo, em segundos, antes que uma solicitação de sincronização da Web expire.|  
|**hostname**|**sysname**|Especifica o valor para **HOST_NAME** quando essa função é usada na cláusula **Where** de um filtro de junção ou relação de registro lógico.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helppullsubscription ](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpsubscription ](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
