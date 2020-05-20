---
title: sp_helpsubscription_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscription_properties
- sp_helpsubscription_properties_TSQL
helpviewer_keywords:
- sp_helpsubscription_properties
ms.assetid: 7a76a645-97eb-47ac-b3ea-e2d75012cbed
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cf8c3510ffbd2d40c882061cc81bb8f6a80d294f
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82815272"
---
# <a name="sp_helpsubscription_properties-transact-sql"></a>sp_helpsubscription_properties (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Recupera informações de segurança da tabela [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) . Esse procedimento armazenado é executado no Assinante.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpsubscription_properties [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db =] 'publisher_db' ]   
    [ , [ @publication =] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`É o nome do Publicador. o *Publicador* é **sysname**, com um padrão de **%** , que retorna informações sobre todos os Publicadores.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados do Publicador. *publisher_db* é **sysname**, com um padrão de **%** , que retorna informações sobre todos os bancos de dados do Publicador.  
  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, com um padrão de **%** , que retorna informações sobre todas as publicações.  
  
`[ @publication_type = ] publication_type`É o tipo de publicação. *publication_type* é **int**, com um padrão de NULL. Se fornecido, *publication_type* deve ser um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Publicação transacional|  
|**1**|Publicação de instantâneo|  
|**2**|Publicação de mesclagem|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**programa**|**sysname**|Nome do Publicador.|  
|**publisher_db**|**sysname**|Nome do banco de dados do Publicador.|  
|**documento**|**sysname**|Nome da publicação.|  
|**publication_type**|**int**|O tipo de publicação:<br /><br /> **0** = transacional<br /><br /> **1** = instantâneo<br /><br /> **2** = mesclagem|  
|**publisher_login**|**sysname**|ID do logon usado no Publicador para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**publisher_password**|**nvarchar (524)**|Senha usada no Publicador para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (criptografada).|  
|**publisher_security_mode**|**int**|Modo de segurança usado no Publicador:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows|  
|**distribuidor**|**sysname**|Nome do Distribuidor.|  
|**distributor_login**|**sysname**|O logon do Distribuidor|  
|**distributor_password**|**nvarchar (524)**|Senha do Distribuidor (criptografada).|  
|**distributor_security_mode**|**int**|Modo de segurança usado no Distribuidor:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows|  
|**ftp_address**|**sysname**|Somente para compatibilidade com versões anteriores. Endereço de rede do serviço FTP (File Transfer Protocol) para o Distribuidor.|  
|**ftp_port**|**int**|Somente para compatibilidade com versões anteriores. Número da porta do serviço FTP para Distribuidor.|  
|**ftp_login**|**sysname**|Somente para compatibilidade com versões anteriores. Nome de usuário usado para se conectar ao serviço FTP.|  
|**ftp_password**|**nvarchar (524)**|Somente para compatibilidade com versões anteriores. Senha de usuário usada para se conectar ao serviço FTP.|  
|**alt_snapshot_folder**|**nvarchar (255)**|Especifica o local da pasta alternativa para o instantâneo.|  
|**working_directory**|**nvarchar (255)**|Nome do diretório de trabalho usado para armazenar dados e arquivos de esquema.|  
|**use_ftp**|**bit**|Especifica o uso do FTP em vez do protocolo regular para recuperar instantâneos. Se for **1**, o FTP será usado.|  
|**dts_package_name**|**sysame**|Especifica o nome do pacote DTS (Data Transformation Services).|  
|**dts_package_password**|**nvarchar (524)**|Especifica a senha no pacote, se houver um.|  
|**dts_package_location**|**int**|Local onde o pacote DTS é armazenado.<br /><br /> **0** = o local do pacote está no distribuidor.<br /><br /> **1** = o local do pacote está no Assinante.|  
|**offload_agent**|**bit**|Especifica se o agente pode ser ativado remotamente. Se for **0**, o agente não poderá ser ativado remotamente.|  
|**offload_server**|**sysname**|Especifica o nome da rede do servidor usado para ativação remota.|  
|**dynamic_snapshot_location**|**nvarchar (255)**|Especifica o caminho para a pasta onde os arquivos de instantâneo são salvos.|  
|**use_web_sync**|**bit**|Especifica se a assinatura pode ser sincronizada via HTTPS, em que o valor **1** significa que esse recurso está habilitado.|  
|**internet_url**|**nvarchar(260)**|URL que representa o local do Replication Listener para sincronização da Web.|  
|**internet_login**|**nvarchar(128)**|Logon que o Agente de Mesclagem usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando Autenticação Básica.|  
|**internet_password**|**nvarchar (524)**|Senha para o logon que o Merge Agent usa ao se conectar ao servidor da Web que está hospedando a sincronização da Web usando Autenticação Básica.|  
|**internet_security_mode**|**int**|O modo de autenticação usado durante a conexão com o servidor Web que está hospedando a sincronização da Web, em que o valor **1** significa autenticação do Windows e um valor de **0** significa autenticação básica.|  
|**internet_timeout**|**int**|Período de tempo, em segundos, antes que uma solicitação de sincronização da Web expire.|  
|**hostname**|**nvarchar(128)**|Especifica o valor para HOST_NAME() onde essa função é usada no filtro de linha com parâmetros da cláusula WHERE.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpsubscription_properties** é usado na replicação de instantâneos, na replicação transacional e na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_helpsubscription_properties**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
