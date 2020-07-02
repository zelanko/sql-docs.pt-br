---
title: sp_helppullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppullsubscription_TSQL
- sp_helppullsubscription
helpviewer_keywords:
- sp_helppullsubscription
ms.assetid: a0d9c3f1-1fe9-497c-8e2f-5b74f47a7346
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3b12ffb31836bfde3cb29cf240dbfc5d9da66eac
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729209"
---
# <a name="sp_helppullsubscription-transact-sql"></a>sp_helppullsubscription (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Exibe informações sobre uma ou mais assinaturas no Assinante. Esse procedimento armazenado é executado no Assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helppullsubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @show_push = ] 'show_push' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`É o nome do servidor remoto. o *Publicador* é **sysname**, com um padrão de **%** , que retorna informações para todos os Publicadores.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados do Publicador. *publisher_db* é **sysname**, com um padrão de **%** , que retorna todos os bancos de dados do Publicador.  
  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, com um padrão de **%** , que retorna todas as publicações. Se esse parâmetro for igual a ALL, somente as assinaturas pull com independent_agent = **0** serão retornadas.  
  
`[ @show_push = ] 'show_push'`É se todas as assinaturas push devem ser retornadas. *show_push*é **nvarchar (5)**, com um padrão de false, que não retorna assinaturas push.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**programa**|**sysname**|Nome do Publicador.|  
|**publisher database**|**sysname**|Nome do banco de dados do Publicador.|  
|**documento**|**sysname**|Nome da publicação.|  
|**independent_agent**|**bit**|Indica se existe um Distribution Agent autônomo para essa publicação.|  
|**tipo de assinatura**|**int**|O tipo de assinatura da publicação.|  
|**Agente de distribuição**|**nvarchar (100)**|O Distribution Agent que trata a assinatura.|  
|**publication description**|**nvarchar (255)**|Descrição da publicação.|  
|**last updating time**|**date**|Hora em que as informações de assinatura foram atualizadas. Esta é uma cadeia de caracteres UNICODE de data ISO (114) + hora de ODBC (121). O formato é yyyymmdd hh:mi:sss.mmm onde 'yyyy' é ano, 'mm' é mês, 'dd' é dia, 'hh' é hora, 'mi' é minuto, 'sss' é segundo e 'mmm' é milissegundo.|  
|**nome da assinatura**|**varchar (386)**|O nome da assinatura.|  
|**último carimbo de data/hora da transação**|**varbinary(16)**|Carimbo de data e hora da última transação replicada.|  
|**update mode**|**tinyint**|O tipo de atualizações permitido.|  
|**distribution agent job_id**|**int**|A ID de trabalho do Distribution Agent.|  
|**enabled_for_synmgr**|**int**|Se a assinatura pode ou não ser sincronizada pelo Gerenciador de Sincronização da [!INCLUDE[msCoName](../../includes/msconame-md.md)].|  
|**GUID da assinatura**|**binary(16)**|Identificador global para a versão da assinatura na publicação.|  
|**subid**|**binary(16)**|Identificador global para uma assinatura anônima.|  
|**immediate_sync**|**bit**|Se os arquivos de sincronização serão criados ou recriados em cada execução do Agente de Instantâneo.|  
|**logon do Publicador**|**sysname**|ID do logon usado no Publicador para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**senha do Publicador**|**nvarchar (524)**|A senha (criptografada) usada no Publicador para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**security_mode de publicador**|**int**|O modo de segurança implementado no Publicador.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows<br /><br /> **2** = os gatilhos de sincronização usam uma entrada **sysservers** estática para fazer RPC (chamada de procedimento remoto) e o *Publicador* deve ser definido na tabela **sysservers** como um servidor remoto ou servidor vinculado.|  
|**distribuidor**|**sysname**|Nome do Distribuidor.|  
|**distributor_login**|**sysname**|A ID de logon usado no Distribuidor para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**distributor_password**|**nvarchar (524)**|A senha (criptografada) usada no Distribuidor para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**distributor_security_mode**|**int**|Modo de segurança implementado no distribuidor:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows|  
|**ftp_address**|**sysname**|Somente para compatibilidade com versões anteriores.|  
|**ftp_port**|**int**|Somente para compatibilidade com versões anteriores.|  
|**ftp_login**|**sysname**|Somente para compatibilidade com versões anteriores.|  
|**ftp_password**|**nvarchar (524)**|Somente para compatibilidade com versões anteriores.|  
|**alt_snapshot_folder**|**nvarchar (255)**|Local onde a pasta de instantâneo é armazenada se o local for diferente ou for uma adição ao local padrão.|  
|**working_directory**|**nvarchar (255)**|Caminho completamente qualificado para o diretório onde os arquivos de instantâneo são transferidos usando o FTP (Protocolo de Transferência de Arquivo) quando essa opção é especificada.|  
|**use_ftp**|**bit**|A assinatura está assinando a Publicação pela Internet e as propriedades de endereçamento do FTP estão configuradas. Se **0**, a assinatura não está usando o FTP. Se **1**, a assinatura está usando FTP.|  
|**publication_type**|**int**|Especifica o tipo de replicação da publicação:<br /><br /> **0** = replicação transacional<br /><br /> **1** = replicação de instantâneo<br /><br /> **2** = replicação de mesclagem|  
|**dts_package_name**|**sysname**|Especifica o nome do pacote DTS (Data Transformation Services).|  
|**dts_package_location**|**int**|Local onde o pacote DTS é armazenado:<br /><br /> **0** = distribuidor<br /><br /> **1** = assinante|  
|**offload_agent**|**bit**|Especifica se o agente pode ser ativado remotamente. Se for **0**, o agente não poderá ser ativado remotamente.|  
|**offload_server**|**sysname**|Especifica o nome da rede do servidor usado para ativação remota.|  
|**last_sync_status**|**int**|O status da assinatura:<br /><br /> **0** = todos os trabalhos estão aguardando para iniciar<br /><br /> **1** = um ou mais trabalhos estão sendo iniciados<br /><br /> **2** = todos os trabalhos foram executados com êxito<br /><br /> **3** = pelo menos um trabalho está em execução<br /><br /> **4** = todos os trabalhos estão agendados e ociosos<br /><br /> **5** = pelo menos um trabalho está tentando ser executado após uma falha anterior<br /><br /> **6** = pelo menos um trabalho falhou ao ser executado com êxito|  
|**last_sync_summary**|**sysname**|Descrição dos últimos resultados da sincronização.|  
|**last_sync_time**|**datetime**|Hora em que as informações de assinatura foram atualizadas. Esta é uma cadeia de caracteres UNICODE de data ISO (114) + hora de ODBC (121). O formato é yyyymmdd hh:mi:sss.mmm onde 'yyyy' é ano, 'mm' é mês, 'dd' é dia, 'hh' é hora, 'mi' é minuto, 'sss' é segundo e 'mmm' é milissegundo.|  
|**job_login**|**nvarchar(512)**|É a conta do Windows na qual o Distribution Agent é executado, que é retornado no formato *domínio* \\ *nome de usuário*.|  
|**job_password**|**sysname**|Por motivos de segurança, um valor de " **\*\*\*\*\*\*\*\*\*\*** " é sempre retornado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helppullsubscription** é usado em instantâneo e replicação transacional.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou a função de banco de dados fixa **db_owner** podem ser executados **sp_helppullsubscription** .  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addpullsubscription](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droppullsubscription](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
