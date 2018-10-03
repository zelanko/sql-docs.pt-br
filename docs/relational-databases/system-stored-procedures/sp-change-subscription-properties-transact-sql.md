---
title: sp_change_subscription_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_change_subscription_properties_TSQL
- sp_change_subscription_properties
helpviewer_keywords:
- sp_change_subscription_properties
ms.assetid: cf8137f9-f346-4aa1-ae35-91a2d3c16f17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f87fb9b43b723fa489e42f05f5f4f727bafd18dc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692284"
---
# <a name="spchangesubscriptionproperties-transact-sql"></a>sp_change_subscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza informações de assinaturas pull. Esse procedimento armazenado é executado no assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_change_subscription_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @property = ] 'property'  
        , [ @value = ] 'value'  
    [ , [ @publication_type = ] publication_type ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'***publisher***'**  
 É o nome do Publicador. *Publisher* está **sysname**, sem padrão.  
  
 [  **@publisher_db=**] **'***publisher_db***'**  
 É o nome do banco de dados Publicador. *publisher_db* está **sysname**, sem padrão.  
  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
 [  **@property=**] **'***propriedade***'**  
 É a propriedade a ser alterada. *propriedade* está **sysname**.  
  
 [  **@value=**] **'***valor***'**  
 É o novo valor da propriedade. *valor* está **nvarchar (1000)**, sem padrão.  
  
 [  **@publication_type =** ] *publication_type*  
 Especifica o tipo de replicação da publicação. *publication_type* está **int**, e pode ser um destes valores.  
  
|Valor|Tipo de Publicação|  
|-----------|----------------------|  
|**0**|Transacional.|  
|**1**|Instantâneo|  
|**2**|Mesclagem|  
|NULL (padrão)|A replicação determina o tipo da publicação. Como esse procedimento armazenado deve procurar em várias tabelas, essa opção é mais lenta do que quando o tipo de publicação exato é fornecido.|  
  
 Essa tabela descreve as propriedades de artigos e os valores dessas propriedades.  
  
|Propriedade|Valor|Description|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||Especifica o local da pasta alternativa para o instantâneo. Se definido como NULL, os arquivos de instantâneo serão retirados do local padrão especificado pelo Publicador.|  
|**distrib_job_login**||Logon para a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o agente é executado.|  
|**distrib_job_password**||Senha para a conta do Windows na qual o agente é executado.|  
|**distributor_login**||O logon do Distribuidor|  
|**distributor_password**||Senha do distribuidor.|  
|**distributor_security_mode**|**1**|Use a Autenticação do Windows ao se conectar ao Distribuidor.|  
||**0**|Use a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Distribuidor.|  
|**dts_package_name**||Especifica o nome do pacote DTS (Data Transformation Services) do SQL Server 2000. Esse valor só poderá ser especificado se a publicação for transacional ou de instantâneo.|  
|**dts_package_password**||Especifica a senha no pacote. *dts_package_password* está **sysname** com um padrão de NULL, que especifica que a propriedade de senha deve ser deixado inalterado.<br /><br /> Observação: Um pacote DTS deve ter uma senha.<br /><br /> Esse valor só poderá ser especificado se a publicação for transacional ou de instantâneo.|  
|**dts_package_location**||Local onde o pacote DTS é armazenado. Esse valor só poderá ser especificado se a publicação for transacional ou de instantâneo.|  
|**dynamic_snapshot_location**||Especifica o caminho para a pasta onde os arquivos de instantâneo são salvos. Esse valor só poderá ser especificado se a publicação for uma publicação de mesclagem.|  
|**ftp_address**||Somente para compatibilidade com versões anteriores.|  
|**ftp_login**||Somente para compatibilidade com versões anteriores.|  
|**ftp_password**||Somente para compatibilidade com versões anteriores.|  
|**ftp_port**||Somente para compatibilidade com versões anteriores.|  
|**nome do host**||Nome do host usado ao conectar ao Publicador.|  
|**internet_login**||Logon que o Agente de Mesclagem usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando Autenticação Básica.|  
|**internet_password**||Senha que o Agente de Mesclagem usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando Autenticação Básica.|  
|**internet_security_mode**|**1**|Use Autenticação Integrada do Windows para sincronização da Web. Recomendamos o uso da Autenticação Básica com sincronização da Web. Para obter mais informações, consulte [Configurar sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md).|  
||**0**|Use Autenticação Básica para sincronização da Web.<br /><br /> Observação: A sincronização da Web requer uma conexão SSL para o servidor Web.|  
|**internet_timeout**||Período de tempo, em segundos, antes que uma solicitação de sincronização da Web expire.|  
|**internet_url**||URL que representa o local do Replication Listener para sincronização da Web.|  
|**merge_job_login**||Logon para a conta do Windows na qual o agente é executado.|  
|**merge_job_password**||Senha para a conta do Windows na qual o agente é executado.|  
|**publisher_login**||Logon de Publicador. Alterando *publisher_login* só tem suporte para assinaturas para publicações de mesclagem.|  
|**publisher_password**||Senha do Publicador. Alterando *publisher_password* só tem suporte para assinaturas para publicações de mesclagem.|  
|**publisher_security_mode**|**1**|Use a Autenticação do Windows ao se conectar ao Publicador. Alterando *publisher_security_mode* só tem suporte para assinaturas para publicações de mesclagem.|  
||**0**|Use a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Publicador.|  
|**use_ftp**|**true**|Use o FTP em vez do protocolo comum para recuperar instantâneos.|  
||**false**|Use o protocolo comum para recuperar instantâneos.|  
|**use_web_sync**|**true**|Habilite a sincronização da Web.|  
||**false**|Desabilite a sincronização da Web.|  
|**working_directory**||Nome do diretório de trabalho usado para armazenar dados e arquivos de esquema temporariamente para a publicação quando o FTP (File Transfer Protocol) for usado para transferir arquivos de instantâneo.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_change_subscription_properties** é usado em todos os tipos de replicação.  
  
 **sp_change_subscription_properties** é usado para assinaturas pull.  
  
 Para editores Oracle, o valor de *publisher_db* é ignorado, pois a Oracle só permite um banco de dados por instância do servidor.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_change_subscription_properties**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [sp_addmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
