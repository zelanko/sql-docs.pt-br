---
title: sp_helpsubscription_properties (Transact-SQL) | Microsoft Docs
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
- sp_helpsubscription_properties
- sp_helpsubscription_properties_TSQL
helpviewer_keywords:
- sp_helpsubscription_properties
ms.assetid: 7a76a645-97eb-47ac-b3ea-e2d75012cbed
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 78637041673509151652fd1e6d4125c8e41e2aa2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpsubscriptionproperties-transact-sql"></a>sp_helpsubscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Recupera informações de segurança de [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) tabela. Esse procedimento armazenado é executado no Assinante.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpsubscription_properties [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db =] 'publisher_db' ]   
    [ , [ @publication =] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, com um padrão de **%**, que retorna informações sobre todos os publicadores.  
  
 [  **@publisher_db=**] **'***publisher_db***'**  
 É o nome do banco de dados Publicador. *publisher_db* é **sysname**, com um padrão de **%**, que retorna informações sobre todos os bancos de dados do publicador.  
  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, com um padrão de **%**, que retorna informações sobre todas as publicações.  
  
 [  **@publication_type=**] *publication_type*  
 É o tipo de publicação. *publication_type* é **int**, com um padrão NULL. Se fornecido, *publication_type* deve ser um dos seguintes valores:  
  
|Value|Descrição|  
|-----------|-----------------|  
|**0**|Publicação transacional|  
|**1**|Publicação de instantâneo|  
|**2**|Publicação de mesclagem|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Nome do Publicador.|  
|**publisher_db**|**sysname**|Nome do banco de dados publicador.|  
|**Publicação**|**sysname**|Nome da publicação.|  
|**publication_type**|**Int**|O tipo de publicação:<br /><br /> **0** = transacional<br /><br /> **1** = instantâneo<br /><br /> **2** = mesclagem|  
|**publisher_login**|**sysname**|ID do logon usado no Publicador para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**publisher_password**|**nvarchar (524)**|Senha usada no Publicador para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (criptografada).|  
|**publisher_security_mode**|**Int**|Modo de segurança usado no Publicador:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows|  
|**Distribuidor**|**sysname**|Nome do Distribuidor.|  
|**distributor_login**|**sysname**|O logon do Distribuidor|  
|**distributor_password**|**nvarchar (524)**|Senha do Distribuidor (criptografada).|  
|**distributor_security_mode**|**Int**|Modo de segurança usado no Distribuidor:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows|  
|**ftp_address**|**sysname**|Somente para compatibilidade com versões anteriores. Endereço de rede do serviço FTP (File Transfer Protocol) para o Distribuidor.|  
|**ftp_port**|**Int**|Somente para compatibilidade com versões anteriores. Número da porta do serviço FTP para Distribuidor.|  
|**ftp_login**|**sysname**|Somente para compatibilidade com versões anteriores. Nome de usuário usado para se conectar ao serviço FTP.|  
|**ftp_password**|**nvarchar (524)**|Somente para compatibilidade com versões anteriores. Senha de usuário usada para se conectar ao serviço FTP.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Especifica o local da pasta alternativa para o instantâneo.|  
|**working_directory**|**nvarchar(255)**|Nome do diretório de trabalho usado para armazenar dados e arquivos de esquema.|  
|**use_ftp**|**bit**|Especifica o uso do FTP em vez do protocolo regular para recuperar instantâneos. Se **1**, FTP é usado.|  
|**dts_package_name**|**sysame**|Especifica o nome do pacote DTS (Data Transformation Services).|  
|**dts_package_password**|**nvarchar (524)**|Especifica a senha no pacote, se houver um.|  
|**dts_package_location**|**Int**|Local onde o pacote DTS é armazenado.<br /><br /> **0** = o pacote local estiver no distribuidor.<br /><br /> **1** = o pacote local é no assinante.|  
|**offload_agent**|**bit**|Especifica se o agente pode ser ativado remotamente. Se **0**, o agente não pode ser ativado remotamente.|  
|**offload_server**|**sysname**|Especifica o nome da rede do servidor usado para ativação remota.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Especifica o caminho para a pasta onde os arquivos de instantâneo são salvos.|  
|**use_web_sync**|**bit**|Especifica se a assinatura pode ser sincronizada por HTTPS, onde um valor de **1** significa que esse recurso está habilitado.|  
|**internet_url**|**nvarchar(260)**|URL que representa o local do Replication Listener para sincronização da Web.|  
|**internet_login**|**nvarchar(128)**|Logon que o Agente de Mesclagem usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando Autenticação Básica.|  
|**internet_password**|**nvarchar (524)**|Senha para o logon que o Merge Agent usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando Autenticação Básica.|  
|**internet_security_mode**|**Int**|O modo de autenticação usado ao se conectar ao servidor da Web que está hospedando a sincronização da Web, onde um valor de **1** significa autenticação do Windows e um valor de **0** significa autenticação básica.|  
|**internet_timeout**|**Int**|Período de tempo, em segundos, antes que uma solicitação de sincronização da Web expire.|  
|**Nome do host**|**nvarchar(128)**|Especifica o valor para HOST_NAME() onde essa função é usada no filtro de linha com parâmetros da cláusula WHERE.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpsubscription_properties** é usado em replicação de instantâneo, replicação transacional e replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_helpsubscription_properties**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
