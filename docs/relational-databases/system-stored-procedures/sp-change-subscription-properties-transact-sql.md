---
title: sp_change_subscription_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_change_subscription_properties_TSQL
- sp_change_subscription_properties
helpviewer_keywords:
- sp_change_subscription_properties
ms.assetid: cf8137f9-f346-4aa1-ae35-91a2d3c16f17
author: stevestein
ms.author: sstein
ms.openlocfilehash: e033e446fc771ad87542474edb1e90caf08faebd
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528756"
---
# <a name="sp_change_subscription_properties-transact-sql"></a>sp_change_subscription_properties (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Atualiza informações de assinaturas pull. Este procedimento armazenado é executado no Assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publisher = ] 'publisher'`É o nome da Editora. *editor* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados do Publisher. *publisher_db* **é sysname,** sem padrão.  
  
`[ @publication = ] 'publication'`É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
`[ @property = ] 'property'`A propriedade deve ser mudada. *propriedade* é **sysname**.  
  
`[ @value = ] 'value'`É o novo valor da propriedade. *valor* é **nvarchar(1000)**, sem padrão.  
  
`[ @publication_type = ] publication_type`Especifica o tipo de replicação da publicação. *publication_type* é **int**, e pode ser um desses valores.  
  
|Valor|Tipo de Publicação|  
|-----------|----------------------|  
|**0**|Transacional|  
|**1**|Instantâneo|  
|**2**|Mesclar|  
|NULL (padrão)|A replicação determina o tipo da publicação. Como esse procedimento armazenado deve procurar em várias tabelas, essa opção é mais lenta do que quando o tipo de publicação exato é fornecido.|  
  
 Essa tabela descreve as propriedades de artigos e os valores dessas propriedades.  
  
|Propriedade|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||Especifica o local da pasta alternativa para o instantâneo. Se definido como NULL, os arquivos de instantâneo serão retirados do local padrão especificado pelo Publicador.|  
|**distrib_job_login**||Logon para a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o agente é executado.|  
|**distrib_job_password**||Senha para a conta do Windows na qual o agente é executado.|  
|**Distributor_login**||O logon do Distribuidor|  
|**Distributor_password**||Senha do distribuidor.|  
|**distributor_security_mode**|**1**|Use a Autenticação do Windows ao se conectar ao Distribuidor.|  
||**0**|Use a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Distribuidor.|  
|**Dts_package_name**||Especifica o nome do pacote DTS (Data Transformation Services) do SQL Server 2000. Esse valor só poderá ser especificado se a publicação for transacional ou de instantâneo.|  
|**Dts_package_password**||Especifica a senha no pacote. *dts_package_password* é **sysname** com um padrão de NULL, que especifica que a propriedade de senha deve ser deixada inalterada.<br /><br /> Nota: Um pacote DTS deve ter uma senha.<br /><br /> Esse valor só poderá ser especificado se a publicação for transacional ou de instantâneo.|  
|**Dts_package_location**||Local onde o pacote DTS é armazenado. Esse valor só poderá ser especificado se a publicação for transacional ou de instantâneo.|  
|**dynamic_snapshot_location**||Especifica o caminho para a pasta onde os arquivos de instantâneo são salvos. Esse valor só poderá ser especificado se a publicação for uma publicação de mesclagem.|  
|**ftp_address**||Somente para compatibilidade com versões anteriores.|  
|**ftp_login**||Somente para compatibilidade com versões anteriores.|  
|**ftp_password**||Somente para compatibilidade com versões anteriores.|  
|**ftp_port**||Somente para compatibilidade com versões anteriores.|  
|**Hostname**||Nome do host usado ao conectar ao Publicador.|  
|**internet_login**||Logon que o Agente de Mesclagem usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando Autenticação Básica.|  
|**internet_password**||Senha que o Agente de Mesclagem usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando Autenticação Básica.|  
|**internet_security_mode**|**1**|Use Autenticação Integrada do Windows para sincronização da Web. Recomendamos o uso da Autenticação Básica com sincronização da Web. Para obter mais informações, consulte [Configurar sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md).|  
||**0**|Use Autenticação Básica para sincronização da Web.<br /><br /> Nota: A sincronização da Web requer uma conexão TLS com o servidor Web.|  
|**internet_timeout**||Período de tempo, em segundos, antes que uma solicitação de sincronização da Web expire.|  
|**internet_url**||URL que representa o local do Replication Listener para sincronização da Web.|  
|**merge_job_login**||Logon para a conta do Windows na qual o agente é executado.|  
|**merge_job_password**||Senha para a conta do Windows na qual o agente é executado.|  
|**Publisher_login**||Logon de Publicador. A *alteração publisher_login* só é suportada para assinaturas para mesclar publicações.|  
|**Publisher_password**||Senha do Publicador. A *mudança publisher_password* só é suportada para assinaturas para mesclar publicações.|  
|**publisher_security_mode**|**1**|Use a Autenticação do Windows ao se conectar ao Publicador. A publisher_security_mode em *mudança* só é suportada para assinaturas para mesclar publicações.|  
||**0**|Use a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Publicador.|  
|**use_ftp**|**true**|Use o FTP em vez do protocolo comum para recuperar instantâneos.|  
||**false**|Use o protocolo comum para recuperar instantâneos.|  
|**use_web_sync**|**true**|Habilite a sincronização da Web.|  
||**false**|Desabilite a sincronização da Web.|  
|**working_directory**||Nome do diretório de trabalho usado para armazenar dados e arquivos de esquema temporariamente para a publicação quando o FTP (File Transfer Protocol) for usado para transferir arquivos de instantâneo.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (sucesso) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_change_subscription_properties** é usado em todos os tipos de replicação.  
  
 **sp_change_subscription_properties** é usado para assinaturas de puxar.  
  
 Para o Oracle Publishers, o valor de *publisher_db* é ignorado, uma vez que o Oracle só permite um banco de dados por instância do servidor.  
  
## <a name="permissions"></a>Permissões  
 Somente membros da função servidor fixo **sysadmin** ou **db_owner** função de banco de dados fixo podem executar **sp_change_subscription_properties**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [sp_addmergepullsubscription &#40;&#41;transact-SQL de sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_addmergepullsubscription_agent &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_addpullsubscription &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_addpullsubscription_agent &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
