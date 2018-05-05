---
title: sp_adddistpublisher (Transact-SQL) | Microsoft Docs
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
- sp_adddistpublisher
- sp_adddistpublisher_TSQL
helpviewer_keywords:
- sp_adddistpublisher
ms.assetid: 04e15011-a902-4074-b38c-3ec2fc73b838
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3ca0d66f6b5a4df2e0d4f4fa79d9eb882159c431
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spadddistpublisher-transact-sql"></a>sp_adddistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Configura um Publicador para usar um banco de dados de distribuição especificado. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados. Observe que os procedimentos armazenados [sp_adddistributor &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) e [sp_adddistributiondb &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) deve executar antes de usar esse procedimento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_adddistpublisher [ @publisher= ] 'publisher'   
        , [ @distribution_db= ] 'distribution_db'   
    [ , [ @security_mode= ] security_mode ]   
    [ , [ @login= ] 'login' ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @working_directory= ] 'working_directory' ]   
    [ , [ @trusted= ] 'trusted' ]   
    [ , [ @encrypted_password= ] encrypted_password ]   
    [ , [ @thirdparty_flag = ] thirdparty_flag ]  
    [ , [ @publisher_type = ] 'publisher_type' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, sem padrão.  
  
 [  **@distribution_db=**] **'***distribution_db***'**  
 É o nome do banco de dados de distribuição. *distributor_db* é **sysname**, sem padrão. Esse parâmetro é usado por agentes de replicação para conexão com o Publicador.  
  
 [  **@security_mode=**] *security_mode*  
 É o modo de segurança implementado. Esse parâmetro é usado apenas pelos agentes de replicação para conexão ao Publicador para assinaturas de atualização na fila ou com um Publicador que não seja do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *security_mode* é **int**, e pode ser um destes valores.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**0**|Agentes de replicação no Distribuidor usam a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conexão com o Publicador.|  
|**1** (padrão)|Agentes de replicação no Distribuidor usam a Autenticação do Windows para conexão com o Publicador.|  
  
 [  **@login=**] **'***login***'**  
 É o logon. Esse parâmetro é necessário se *security_mode* é **0**. *login* é **sysname**, com um padrão de NULL. Esse parâmetro é usado por agentes de replicação para conexão com o Publicador.  
  
 [  **@password=**] **'***senha***'**]  
 É a senha. *senha* é **sysname**, com um padrão NULL. Esse parâmetro é usado por agentes de replicação para conexão com o Publicador.  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte.  
  
 [  **@working_directory=**] **'***working_directory***'**  
 É o nome do diretório de trabalho usado para armazenar dados e arquivos de esquema para a publicação. *working_directory* é **nvarchar (255)** e o padrão é a pasta ReplData para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por exemplo 'C:\Program Files\Microsoft SQL Server\MSSQL\MSSQ.1\ReplData'. O nome deve ser especificado no formato UNC.  
  
 [  **@trusted=**] **'***confiável***'**  
 Esse parâmetro foi substituído e é fornecido apenas para compatibilidade com versões anteriores. *confiável* é **nvarchar (5)** e configurá-lo como qualquer coisa **false** resultará em erro.  
  
 [  **@encrypted_password=**] *encrypted_password*  
 Configuração *encrypted_password* não é mais suportada. Tentativa de definir isso **bit** parâmetro **1** resultará em erro.  
  
 [  **@thirdparty_flag =**] *thirdparty_flag*  
 É quando o Publicador é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *thirdparty_flag* é **bit**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**0** (padrão)|Banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**1**|Banco de dados diferente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
 [ **@publisher_type**=] **'***publisher_type***'**  
 Especifica o tipo do Publicador quando o Publicador não é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publisher_type* é sysname, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**<br /><br /> (padrão)|Especifica um Editor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|Especifica um Publicador Oracle padrão.|  
|**ORACLE GATEWAY**|Especifica um Editor Oracle Gateway.|  
  
 Para obter mais informações sobre as diferenças entre um publicador Oracle e um publicador Oracle Gateway, consulte [configurar um publicador Oracle](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_adddistpublisher** é usada pela replicação de instantâneo, replicação transacional e replicação de mesclagem.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistpublisher-tran_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_adddistpublisher**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)  
  
  
