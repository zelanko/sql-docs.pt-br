---
title: MSsubscription_properties (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSsubscription_properties
- MSsubscription_properties_TSQL
dev_langs: TSQL
helpviewer_keywords: MSsubscription_properties system table
ms.assetid: f96fc1ae-b798-4b05-82a7-564ae6ef23b8
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0811b4b8705fda92ff57e782d04f6543b9fd1ebb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssubscriptionproperties-transact-sql"></a>MSsubscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSsubscription_properties** tabela contém linhas para as informações de parâmetro necessárias para executar os agentes de replicação no assinante. Essa tabela é armazenada no banco de dados de assinatura para uma assinatura pull e no banco de dados de distribuição, no Distribuidor, para uma assinatura push.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**Publicador**|**sysname**|O nome do publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**publicação**|**sysname**|O nome da publicação.|  
|**publication_type**|**int**|O tipo de publicação:<br /><br /> **0** = transacional.<br /><br /> **2** = mesclagem.|  
|**publisher_login**|**sysname**|A ID do logon usada no Publicador para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**publisher_password**|**nvarchar (524)**|A senha (criptografada) usada no Publicador para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**publisher_security_mode**|**int**|O modo de segurança implementado no Publicador.<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticação do SQL Server.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticação do Windows.<br /><br /> **2** = os gatilhos de sincronização usam uma estática **sysservers** entrada para fazer uma chamada de procedimento remoto (RPC), e *publicador* deve ser definido na **sysservers**tabela como um servidor remoto ou vinculado.|  
|**distribuidor**|**sysname**|O nome do Distribuidor.|  
|**distributor_login**|**sysname**|A ID de logon usada no distribuidor para autenticação do SQL Server.|  
|**distributor_password**|**nvarchar (524)**|A senha (criptografada) usada no Distribuidor para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**distributor_security_mode**|**int**|O modo de segurança implementado no Distribuidor.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.<br /><br /> **1** = autenticação do Windows.|  
|**ftp_address**|**sysname**|O endereço de rede do serviço FTP (File Transfer Protocol) para o Distribuidor.|  
|**ftp_port**|**int**|O número da porta do serviço FTP do Distribuidor.|  
|**ftp_login**|**sysname**|O nome de usuário usado para se conectar ao serviço FTP.|  
|**ftp_password**|**nvarchar (524)**|A senha de usuário usada para se conectar ao serviço FTP.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Especifica o local da pasta alternativa para o instantâneo.|  
|**working_directory**|**nvarchar(255)**|O nome do diretório de trabalho usado para armazenar dados e arquivos de esquema.|  
|**use_ftp**|**bit**|Especifica o uso do FTP em vez do protocolo regular para recuperar instantâneos. Se **1**, FTP é usado.|  
|**dts_package_name**|**sysname**|Especifica o nome do pacote DTS (Data Transformation Services).|  
|**dts_package_password**|**nvarchar (524)**|Especifica a senha no pacote.|  
|**dts_package_location**|**int**|O local onde o pacote DTS é armazenado.|  
|**enabled_for_syncmgr**|**bit**|Especifica se a assinatura pode ou não ser sincronizada pelo Gerenciador de Sincronização da [!INCLUDE[msCoName](../../includes/msconame-md.md)].<br /><br /> **0** = assinatura não está registrada com o Gerenciador de sincronização.<br /><br /> **1** = assinatura será registrada com o Gerenciador de sincronização e será sincronizada sem iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
|**offload_agent**|**bit**|Especifica se o agente pode ser ativado remotamente ou não. Se **0**, o agente não pode ser ativado remotamente.|  
|**offload_server**|**sysname**|Especifica o nome da rede do servidor usado para ativação remota.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Especifica o caminho para a pasta onde os arquivos de instantâneo são salvos.|  
|**use_web_sync**|**bit**|Especifica se a assinatura pode ser sincronizada pelo HTTP ou não. Um valor de **1** significa que esse recurso está habilitado.|  
|**internet_url**|**nvarchar (260)**|O URL que representa o local do Replication Listener para sincronização da Web.|  
|**internet_login**|**sysname**|O logon que o Merge Agent usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.|  
|**internet_password**|**nvarchar (524)**|A senha para o logon que o Merge Agent usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.|  
|**internet_security_mode**|**int**|O modo de autenticação usado ao se conectar ao servidor da Web que está hospedando a sincronização da Web, onde um valor de **1** significa autenticação do Windows e um valor de **0** significa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticação.|  
|**internet_timeout**|**int**|O período de tempo, em segundos, antes que uma solicitação de sincronização da Web expire.|  
|**nome do host**|**sysname**|Especifica o valor de **HOST_NAME** quando essa função é usada no **onde** cláusula de um filtro de junção ou relação de registro lógico.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helppullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
