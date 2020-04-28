---
title: sp_changemergepullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergepullsubscription
- sp_changemergepullsubscription_TSQL
helpviewer_keywords:
- sp_changemergepullsubscription
ms.assetid: 5e0d04f2-6175-44a2-ad96-a8e2986ce4c9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8771d7c821a82733b0664f09c5dadf2128baf877
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68090848"
---
# <a name="sp_changemergepullsubscription-transact-sql"></a>sp_changemergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades da assinatura pull de mesclagem. Esse procedimento armazenado é executado no Assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changemergepullsubscription [ [ @publication= ] 'publication' ]  
    [ , [ @publisher= ] 'publisher' ]  
    [ , [ @publisher_db= ] 'publisher_db' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, com um padrão de%.  
  
`[ @publisher = ] 'publisher'`É o nome do Publicador. o *Publicador*é **sysname**, com um padrão de%.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados do Publicador. *publisher_db*é **sysname**, com um padrão de%.  
  
`[ @property = ] 'property'`É o nome da propriedade a ser alterada. a *Propriedade* é **sysname**e pode ser um dos valores na tabela.  
  
`[ @value = ] 'value'`É o novo valor para a propriedade especificada. o *valor*é **nvarchar (255)** e pode ser um dos valores na tabela.  
  
|Propriedade|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||Local em que a pasta de instantâneo é armazenada se o local for diferente de ou além do local padrão.|  
|**ndescrição**||Descrição da assinatura pull de mesclagem.|  
|**distribuidor**||Nome do Distribuidor.|  
|**distributor_login**||ID do logon usado no Distribuidor para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**distributor_password**||A senha (criptografada) usada no Distribuidor para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**distributor_security_mode**|**1**|Use a Autenticação do Windows ao se conectar ao Distribuidor.|  
||**0**|Use a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Distribuidor.|  
|**dynamic_snapshot_location**||Caminho para a pasta onde os arquivos de instantâneo são salvos.|  
|**ftp_address**||Disponível somente para compatibilidade com versões anteriores. É o endereço de rede do serviço FTP (File Transfer Protocol) para o Distribuidor.|  
|**ftp_login**||Disponível somente para compatibilidade com versões anteriores. É o nome de usuário usado para se conectar ao serviço FTP.|  
|**ftp_password**||Disponível somente para compatibilidade com versões anteriores. É a senha de usuário usada para se conectar ao serviço FTP.|  
|**ftp_port**||Disponível somente para compatibilidade com versões anteriores. É o número da porta do serviço FTP para o Distribuidor.|  
|**hostname**||Especifica o valor para HOST_NAME() quando essa função for usada na cláusula WHERE de uma relação de filtro de junção ou registro lógico.|  
|**internet_login**||Logon que o Agente de Mesclagem usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando Autenticação Básica.|  
|**internet_password**||Senha para o logon que o Merge Agent usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando Autenticação Básica.|  
|**internet_security_mode**|**1**|Use a Autenticação do Windows para se conectar ao servidor da Web que está hospedando a sincronização da Web.|  
||**0**|Use a Autenticação Básica para se conectar ao servidor da Web que está hospedando a sincronização da Web.|  
|**internet_timeout**||Período de tempo, em segundos, antes que uma solicitação de sincronização da Web expire.|  
|**internet_url**||URL que representa o local do Replication Listener para sincronização da Web.|  
|**merge_job_login**||Logon para a conta do Windows na qual o agente é executado.|  
|**merge_job_password**||Senha para a conta do Windows na qual o agente é executado.|  
|**prioridade**||Disponível somente para compatibilidade com versões anteriores; Execute [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md) no Publicador em vez de modificar a prioridade de uma assinatura.|  
|**publisher_login**||ID do logon usado no Publicador para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**publisher_password**||A senha (criptografada) usada no Publicador para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**publisher_security_mode**|**0**|Use a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Publicador.|  
||**1**|Use a Autenticação do Windows ao se conectar ao Publicador.|  
||**2**|Os gatilhos de sincronização usam uma entrada **sysservers** estática para fazer RPC (chamada de procedimento remoto) e o Publicador deve ser definido na tabela **sysservers** como um servidor remoto ou servidor vinculado.|  
|**sync_type**|**Automático**|Esquema e dados iniciais de tabelas publicadas são transferidos ao Assinante primeiro.|  
||**nenhum**|O Assinante já tem o esquema e os dados iniciais para as tabelas publicadas; tabelas de sistema e dados são sempre transferidos.|  
|**use_ftp**|**true**|Use o FTP em vez do protocolo típico para recuperar instantâneos.|  
||**false**|Use o FTP em vez do protocolo típico para recuperar instantâneos.|  
|**use_web_sync**|**true**|A assinatura pode ser sincronizada pelo HTTP.|  
||**false**|A assinatura não pode ser sincronizada pelo HTTP.|  
|**use_interactive_resolver**|**true**|Resolvedor interativo usado durante a reconciliação.|  
||**false**|Resolvedor interativo não é usado.|  
|**working_directory**||Caminho completamente qualificado para o diretório onde os arquivos de instantâneo são transferidos usando o FTP quando essa opção é especificada.|  
|NULL (padrão)||Retorna a lista de valores com suporte para a *Propriedade*.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changemergepullsubscription** é usado na replicação de mesclagem.  
  
 O servidor e o banco de dados atual deveriam ser o Assinante e banco de dados do Assinante.  
  
 Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_changemergepullsubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [&#41;&#40;Transact-SQL de sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropmergepullsubscription](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
