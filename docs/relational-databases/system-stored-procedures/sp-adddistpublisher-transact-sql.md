---
title: sp_adddistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddistpublisher
- sp_adddistpublisher_TSQL
helpviewer_keywords:
- sp_adddistpublisher
ms.assetid: 04e15011-a902-4074-b38c-3ec2fc73b838
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c01d00362dc55deb1fa9da8df49beebdaf82b170
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492768"
---
# <a name="spadddistpublisher-transact-sql"></a>sp_adddistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Configura um Publicador para usar um banco de dados de distribuição especificado. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados. Observe que os procedimentos armazenados [sp_adddistributor &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) e [sp_adddistributiondb &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) deverão ter sido executados antes de usar isso armazenados procedimento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_adddistpublisher [ @publisher= ] 'publisher'   
        , [ @distribution_db= ] 'distribution_db'   
    [ , [ @security_mode= ] security_mode ]   
    [ , [ @login= ] 'login' ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @working_directory= ] 'working_directory' ]   
    [ , [ @storage_connection_string= ] 'storage_connection_string']
    [ , [ @trusted= ] 'trusted' ]   
    [ , [ @encrypted_password= ] encrypted_password ]   
    [ , [ @thirdparty_flag = ] thirdparty_flag ]  
    [ , [ @publisher_type = ] 'publisher_type' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` É o nome do publicador. *Publisher* está **sysname**, sem padrão.  
  
`[ @distribution_db = ] 'distribution_db'` É o nome do banco de dados de distribuição. *distributor_db* está **sysname**, sem padrão. Esse parâmetro é usado por agentes de replicação para conexão com o Publicador.  
  
`[ @security_mode = ] security_mode` É o modo de segurança implementado. Esse parâmetro só é usado por agentes de replicação para se conectar ao publicador para assinaturas de atualização enfileirada ou com um não - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *security_mode* está **int**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Agentes de replicação no Distribuidor usam a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conexão com o Publicador.|  
|**1** (padrão)|Agentes de replicação no Distribuidor usam a Autenticação do Windows para conexão com o Publicador.|  
  
`[ @login = ] 'login'` É o logon. Esse parâmetro é necessário se *security_mode* é **0**. *login* é **sysname**, com um padrão de NULL. Esse parâmetro é usado por agentes de replicação para conexão com o Publicador.  
  
`[ @password = ] 'password']` É a senha. *senha* está **sysname**, com um padrão NULL. Esse parâmetro é usado por agentes de replicação para conexão com o Publicador.  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte.  
  
`[ @working_directory = ] 'working_directory'` É o nome do diretório de trabalho usado para armazenar dados e arquivos de esquema para a publicação. *working_directory* está **nvarchar (255)** e assume como padrão a pasta ReplData para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por exemplo `C:\Program Files\Microsoft SQL Server\MSSQL\MSSQ.1\ReplData`. O nome deve ser especificado no formato UNC.  

 Para o banco de dados SQL Azure, use `\\<storage_account>.file.core.windows.net\<share>`.

`[ @storage_connection_string = ] 'storage_connection_string'` É necessário para o banco de dados SQL. Use a chave de acesso no Portal do Azure em armazenamento > configurações.

 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]

`[ @trusted = ] 'trusted'` Esse parâmetro foi preterido e é fornecido para compatibilidade com versões anteriores. *confiável* está **nvarchar (5)** e defini-lo como qualquer coisa, exceto **falso** resultará em erro.  
  
`[ @encrypted_password = ] encrypted_password` Definindo *encrypted_password* não é mais suportada. Tentativa de definir isso **bits** parâmetro **1** resultará em erro.  
  
`[ @thirdparty_flag = ] thirdparty_flag` É quando o publicador é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *thirdparty_flag* está **bit**, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0** (padrão)|Banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**1**|Banco de dados diferente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
`[ @publisher_type = ] 'publisher_type'` Especifica o tipo de publicador quando o publicador não é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publisher_type* é sysname, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**MSSQLSERVER**<br /><br /> (padrão)|Especifica um Editor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|Especifica um Publicador Oracle padrão.|  
|**ORACLE GATEWAY**|Especifica um Editor Oracle Gateway.|  
  
 Para obter mais informações sobre as diferenças entre um publicador Oracle e um publicador Oracle Gateway, consulte [configurar um publicador Oracle](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_adddistpublisher** é usada pela replicação de instantâneo, replicação transacional e replicação de mesclagem.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistpublisher-tran_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** pode executar a função de servidor fixa **sp_adddistpublisher**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)  
  
  
