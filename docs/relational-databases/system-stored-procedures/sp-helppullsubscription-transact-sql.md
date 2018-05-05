---
title: sp_helppullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helppullsubscription_TSQL
- sp_helppullsubscription
helpviewer_keywords:
- sp_helppullsubscription
ms.assetid: a0d9c3f1-1fe9-497c-8e2f-5b74f47a7346
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: dc273a0c9ab017d400beddca2b00eaa23ab9c1a4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelppullsubscription-transact-sql"></a>sp_helppullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe informações sobre uma ou mais assinaturas no Assinante. Esse procedimento armazenado é executado no assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helppullsubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @show_push = ] 'show_push' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'***publicador***'**  
 É o nome do servidor remoto. *publicador* é **sysname**, com um padrão de **%**, que retorna informações para todos os publicadores.  
  
 [  **@publisher_db=**] **'***publisher_db***'**  
 É o nome do banco de dados Publicador. *publisher_db* é **sysname**, com um padrão de **%**, que retorna todos os bancos de dados do publicador.  
  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, com um padrão de **%**, que retorna todas as publicações. Se esse parâmetro for igual a ALL, somente assinaturas pull com independent_agent = **0** são retornados.  
  
 [  **@show_push=**] **'***show_push***'**  
 Especifica se todas as assinaturas push devem ser retornadas. *show_push*é **nvarchar (5)**, com um padrão de FALSE, que não retorna assinaturas push.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Nome do Publicador.|  
|**banco de dados do publicador**|**sysname**|Nome do banco de dados publicador.|  
|**Publicação**|**sysname**|Nome da publicação.|  
|**independent_agent**|**bit**|Indica se existe um Distribution Agent autônomo para essa publicação.|  
|**tipo de assinatura**|**Int**|O tipo de assinatura da publicação.|  
|**Agente de distribuição**|**nvarchar(100)**|O Distribution Agent que trata a assinatura.|  
|**Descrição da publicação**|**nvarchar(255)**|Descrição da publicação.|  
|**hora da última atualização**|**date**|Hora em que as informações de assinatura foram atualizadas. Esta é uma cadeia de caracteres UNICODE de data ISO (114) + hora de ODBC (121). O formato é yyyymmdd hh:mi:sss.mmm onde 'yyyy' é ano, 'mm' é mês, 'dd' é dia, 'hh' é hora, 'mi' é minuto, 'sss' é segundo e 'mmm' é milissegundo.|  
|**Nome da assinatura**|**varchar(386)**|O nome da assinatura.|  
|**último carimbo de hora de transação**|**varbinary(16)**|Carimbo de data e hora da última transação replicada.|  
|**modo de atualização**|**tinyint**|O tipo de atualizações permitido.|  
|**job_id do agente de distribuição**|**Int**|A ID de trabalho do Distribution Agent.|  
|**enabled_for_synmgr**|**Int**|Se a assinatura pode ou não ser sincronizada pelo Gerenciador de Sincronização da [!INCLUDE[msCoName](../../includes/msconame-md.md)].|  
|**guid de assinatura**|**binary(16)**|Identificador global para a versão da assinatura na publicação.|  
|**subid**|**binary(16)**|Identificador global para uma assinatura anônima.|  
|**immediate_sync**|**bit**|Se os arquivos de sincronização serão criados ou recriados em cada execução do Agente de Instantâneo.|  
|**logon do publicador**|**sysname**|ID do logon usado no Publicador para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**senha do publicador**|**nvarchar (524)**|A senha (criptografada) usada no Publicador para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**security_mode de publicador**|**Int**|O modo de segurança implementado no Publicador.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows<br /><br /> **2** = os gatilhos de sincronização usam uma estática **sysservers** entrada para fazer a chamada de procedimento remoto (RPC), e *publicador* deve ser definido na **sysservers**tabela como um servidor remoto ou vinculado.|  
|**Distribuidor**|**sysname**|Nome do Distribuidor.|  
|**distributor_login**|**sysname**|A ID de logon usado no Distribuidor para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**distributor_password**|**nvarchar (524)**|A senha (criptografada) usada no Distribuidor para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**distributor_security_mode**|**Int**|Modo de segurança implementado no distribuidor.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows|  
|**ftp_address**|**sysname**|Somente para compatibilidade com versões anteriores.|  
|**ftp_port**|**Int**|Somente para compatibilidade com versões anteriores.|  
|**ftp_login**|**sysname**|Somente para compatibilidade com versões anteriores.|  
|**ftp_password**|**nvarchar (524)**|Somente para compatibilidade com versões anteriores.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Local onde a pasta de instantâneo é armazenada se o local for diferente ou for uma adição ao local padrão.|  
|**working_directory**|**nvarchar(255)**|Caminho completamente qualificado para o diretório onde os arquivos de instantâneo são transferidos usando o FTP (Protocolo de Transferência de Arquivo) quando essa opção é especificada.|  
|**use_ftp**|**bit**|A assinatura está assinando a Publicação pela Internet e as propriedades de endereçamento do FTP estão configuradas. Se **0**, assinatura não está usando o FTP. Se **1**, assinatura usando o FTP.|  
|**publication_type**|**Int**|Especifica o tipo de replicação da publicação:<br /><br /> **0** = replicação transacional<br /><br /> **1** = replicação de instantâneo<br /><br /> **2** = replicação de mesclagem|  
|**dts_package_name**|**sysname**|Especifica o nome do pacote DTS (Data Transformation Services).|  
|**dts_package_location**|**Int**|Local onde o pacote DTS é armazenado:<br /><br /> **0** = distribuidor<br /><br /> **1** = assinante|  
|**offload_agent**|**bit**|Especifica se o agente pode ser ativado remotamente. Se **0**, o agente não pode ser ativado remotamente.|  
|**offload_server**|**sysname**|Especifica o nome da rede do servidor usado para ativação remota.|  
|**last_sync_status**|**Int**|O status da assinatura:<br /><br /> **0** = todos os trabalhos estão esperando para iniciar<br /><br /> **1** = um ou mais trabalhos estão iniciando<br /><br /> **2** = todos os trabalhos foram executados com êxito<br /><br /> **3** = pelo menos um trabalho está em execução<br /><br /> **4** = todos os trabalhos estão agendados e ociosos<br /><br /> **5** = pelo menos um trabalho está tentando executar após uma falha anterior<br /><br /> **6** = pelo menos um trabalho falhou em executar com êxito|  
|**last_sync_summary**|**sysname**|Descrição dos resultados da última sincronização.|  
|**last_sync_time**|**datetime**|Hora em que as informações de assinatura foram atualizadas. Esta é uma cadeia de caracteres UNICODE de data ISO (114) + hora de ODBC (121). O formato é yyyymmdd hh:mi:sss.mmm onde 'yyyy' é ano, 'mm' é mês, 'dd' é dia, 'hh' é hora, 'mi' é minuto, 'sss' é segundo e 'mmm' é milissegundo.|  
|**job_login**|**nvarchar(512)**|É a conta do Windows sob a qual o Distribution agent é executado, que é retornada no formato *domínio*\\*nome de usuário*.|  
|**job_password**|**sysname**|Por motivos de segurança, um valor de "**\*\*\*\*\*\*\*\*\*\***" é sempre retornado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_helppullsubscription** é usado em replicação de instantâneo e transacional.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_helppullsubscription** .  
  
## <a name="see-also"></a>Consulte também  
 [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_droppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
