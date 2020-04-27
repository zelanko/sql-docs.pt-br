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
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2190e31245cde19eca4c5a47f21ac48e12f57f53
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68771394"
---
# <a name="sp_adddistpublisher-transact-sql"></a>sp_adddistpublisher (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Configura um Publicador para usar um banco de dados de distribuição especificado. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados. Observe que os procedimentos armazenados [sp_adddistributor &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) e [sp_adddistributiondb &#40;Transact-SQL](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)&#41;devem ter sido executados antes de usar esse procedimento armazenado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publisher = ] 'publisher'`É o nome do editor. o *Publicador* é **sysname**, sem padrão.  
  
`[ @distribution_db = ] 'distribution_db'`É o nome do banco de dados de distribuição. *distributor_db* é **sysname**, sem padrão. Esse parâmetro é usado por agentes de replicação para conexão com o Publicador.  
  
`[ @security_mode = ] security_mode`É o modo de segurança implementado. Esse parâmetro é usado apenas pelos agentes de replicação para se conectar ao Publicador para assinaturas de atualização enfileiradas ou com um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não publicador. *security_mode* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Agentes de replicação no Distribuidor usam a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conexão com o Publicador.|  
|**1** (padrão)|Agentes de replicação no Distribuidor usam a Autenticação do Windows para conexão com o Publicador.|  
  
`[ @login = ] 'login'`É o logon. Esse parâmetro será necessário se *security_mode* for **0**. *login* é **sysname**, com um padrão de NULL. Esse parâmetro é usado por agentes de replicação para conexão com o Publicador.  
  
`[ @password = ] 'password']`É a senha. a *senha* é **sysname**, com um padrão de NULL. Esse parâmetro é usado por agentes de replicação para conexão com o Publicador.  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte.  
  
`[ @working_directory = ] 'working_directory'`É o nome do diretório de trabalho usado para armazenar dados e arquivos de esquema para a publicação. *working_directory* é **nvarchar (255)** e usa como padrão a pasta repldata para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por exemplo. `C:\Program Files\Microsoft SQL Server\MSSQL\MSSQ.1\ReplData` O nome deve ser especificado no formato UNC.  

 Para o banco de dados SQL `\\<storage_account>.file.core.windows.net\<share>`do Azure, use.

`[ @storage_connection_string = ] 'storage_connection_string'`É necessário para o banco de dados SQL. Use a chave de acesso do portal do Azure em configurações de > de armazenamento.

 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]

`[ @trusted = ] 'trusted'`Esse parâmetro foi preterido e é fornecido somente para fins de compatibilidade com versões anteriores. *Trusted* é **nvarchar (5)** e defini-lo como qualquer coisa, exceto **false** , resultará em um erro.  
  
`[ @encrypted_password = ] encrypted_password`Não há mais suporte para a configuração de *encrypted_password* . A tentativa de definir esse parâmetro de **bit** como **1** resultará em um erro.  
  
`[ @thirdparty_flag = ] thirdparty_flag`É quando o Publicador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]é. *thirdparty_flag* é **bit**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0** (padrão)|Banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**1**|Banco de dados diferente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
`[ @publisher_type = ] 'publisher_type'`Especifica o tipo de Publicador quando o Publicador não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]estiver. *publisher_type* é sysname e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**MSSQLSERVER**<br /><br /> (padrão)|Especifica um Editor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|Especifica um Publicador Oracle padrão.|  
|**ORACLE GATEWAY**|Especifica um Editor Oracle Gateway.|  
  
 Para obter mais informações sobre as diferenças entre um Publicador Oracle e um Publicador de gateway Oracle, consulte [configurar um Publicador Oracle](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 o **sp_adddistpublisher** é usado pela replicação de instantâneo, replicação transacional e replicação de mesclagem.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistpublisher-tran_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_adddistpublisher**.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [&#41;&#40;Transact-SQL de sp_changedistpublisher](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropdistpublisher](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpdistpublisher](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Configurar a distribuição](../../relational-databases/replication/configure-distribution.md)  
  
  
