---
title: sp_addlinkedsrvlogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addlinkedsrvlogin_TSQL
- sp_addlinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlinkedsrvlogin
ms.assetid: eb69f303-1adf-4602-b6ab-f62e028ed9f6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4ee38ac3c19c9f5d5b36f896c1018a16e98e37cc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758008"
---
# <a name="sp_addlinkedsrvlogin-transact-sql"></a>sp_addlinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Cria ou atualiza um mapeamento entre um logon na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e uma conta de segurança em um servidor remoto.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_addlinkedsrvlogin [ @rmtsrvname = ] 'rmtsrvname'   
     [ , [ @useself = ] { 'TRUE' | 'FALSE' | NULL } ]   
     [ , [ @locallogin = ] 'locallogin' ]   
     [ , [ @rmtuser = ] 'rmtuser' ]   
     [ , [ @rmtpassword = ] 'rmtpassword' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 `[ @rmtsrvname = ] 'rmtsrvname'`  
 É o nome do servidor vinculado ao qual o mapeamento de logon se aplica. *rmtsrvname* é **sysname**, sem padrão.  
  
 `[ @useself = ] { 'TRUE' | 'FALSE' | NULL }'`  
 Determina se deve se conectar ao *rmtsrvname* representando logons locais ou enviando explicitamente um logon e uma senha. O tipo de dados é **varchar (** 8 **)**, com um padrão de true.  
  
 Um valor TRUE especifica que os logons usam suas próprias credenciais para se conectar ao *rmtsrvname*, com os argumentos *rmtuser* e *rmtpassword* sendo ignorados. FALSE especifica que os argumentos *rmtuser* e *rmtpassword* são usados para se conectar ao *rmtsrvname* para o *locallogin*especificado. Se *rmtuser* e *rmtpassword* também forem definidos como NULL, nenhum logon ou senha será usado para se conectar ao servidor vinculado.  
  
 `[ @locallogin = ] 'locallogin'`  
 É um logon no servidor local. *locallogin* é **sysname**, com um padrão de NULL. NULL especifica que essa entrada se aplica a todos os logons locais que se conectam ao *rmtsrvname*. Se não for NULL, *locallogin* poderá ser um logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um logon do Windows. O logon do Windows deve ter acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diretamente ou por meio de sua associação em um grupo do Windows com acesso.  
  
 `[ @rmtuser = ] 'rmtuser'`  
 É o logon remoto usado para se conectar ao *rmtsrvname* quando @useself é falso. Quando o servidor remoto é uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não usa a autenticação do Windows, o *rmtuser* é um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon. *rmtuser* é **sysname**, com um padrão de NULL.  
  
 `[ @rmtpassword = ] 'rmtpassword'`  
 É a senha associada a *rmtuser*. *rmtpassword* é **sysname**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Quando o usuário faz logon no servidor local e executa uma consulta distribuída que acessa uma tabela no servidor vinculado, o servidor local deve fazer logon no servidor vinculado em nome do usuário para acessar essa tabela. Use sp_addlinkedsrvlogin para especificar as credenciais de logon que o servidor local usa para efetuar logon no servidor vinculado.  
  
> [!NOTE]  
>  Para criar os melhores planos de consulta quando você estiver usando uma tabela em um servidor vinculado, o processador de consulta deverá ter estatísticas de distribuição de dados do servidor vinculado. Usuários que limitaram permissões em qualquer coluna da tabela podem não ter permissões suficientes para obter todas as estatísticas úteis e podem receber um plano de consulta menos eficiente e de baixo desempenho. Se o servidor vinculado for uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], para obter todas as estatísticas disponíveis, o usuário deverá ser proprietário da tabela ou membro da função de servidor fixa sysadmin, da função de banco de dados fixa db_owner ou da função de banco de dados fixa db_ddladmin no servidor vinculado. O SQL Server 2012 SP1 altera as restrições de permissão para obter estatísticas e permite que usuários com permissão SELECT acessem as estatísticas disponíveis através de DBCC SHOW_STATISTICS. Para obter mais informações, consulte a seção permissões de [DBCC SHOW_STATISTICS &#40;&#41;Transact-SQL ](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md).  
  
 O mapeamento padrão entre todos os logons no servidor local e os logons remotos no servidor vinculado é criado automaticamente com a execução de sp_addlinkedserver. O mapeamento padrão declara que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa as credenciais do usuário do logon local ao se conectar ao servidor vinculado em nome do logon. Isso é equivalente a executar sp_addlinkedsrvlogin com @useself definido como **true** para o servidor vinculado, sem especificar um nome de usuário local. Use sp_addlinkedsrvlogin somente para alterar o mapeamento padrão ou adicionar novos mapeamentos para logons locais específicos. Para excluir o mapeamento padrão ou qualquer outro mapeamento, use sp_droplinkedsrvlogin.  
  
 Em vez de usar sp_addlinkedsrvlogin para criar um mapeamento de logon predeterminado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar automaticamente as credenciais de segurança do Windows (nome de logon e senha do Windows) de um usuário que emite a consulta para se conectar a um servidor vinculado quando todas as condições a seguir existirem:  
  
-   Um usuário é conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pelo Modo de Autenticação do Windows.  
  
-   A delegação da conta de segurança está disponível no cliente e no servidor destinatário.  
  
-   O provedor oferece suporte para o Modo de Autenticação do Windows; por exemplo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é executado no Windows.  
  
> [!NOTE]  
>  A delegação não deve estar habilitada para cenários de salto único, mas é obrigatória para cenários de vários saltos.  
  
 Após a autenticação ter sido executada pelo servidor vinculado com os mapeamentos definidos pela execução de sp_addlinkedsrvlogin na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as permissões em objetos individuais no banco de dados remoto são determinadas pelo servidor vinculado, não pelo servidor local.  
  
 sp_addlinkedsrvlogin não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY LOGIN no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-connecting-all-local-logins-to-the-linked-server-by-using-their-own-user-credentials"></a>a. Conectando todos os logons locais no servidor vinculado com suas próprias credenciais de usuário  
 O exemplo a seguir cria um mapeamento para verificar se todos os logons no servidor local se conectam por meio da `Accounts` do servidor vinculado usando suas próprias credenciais de usuário.  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts';  
```  
  
 Ou  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'true';  
```  
  
> [!NOTE]  
>  Se houver mapeamentos explícitos criados para logons individuais, eles têm prioridade com relação a qualquer mapeamento global que possa existir para o servidor vinculado.  
  
### <a name="b-connecting-a-specific-login-to-the-linked-server-by-using-different-user-credentials"></a>B. Conectando um logon específico no servidor vinculado com credenciais de usuário diferentes  
 O exemplo a seguir cria um mapeamento para verificar se o usuário `Domain\Mary` do Windows se conecta por meio de `Accounts` do servidor vinculado usando o logon `MaryP` e a senha `d89q3w4u`.  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'false', 'Domain\Mary', 'MaryP', 'd89q3w4u';  
```  
  
> [!IMPORTANT]  
>  Este exemplo não usa a Autenticação do Windows. As senhas serão transmitidas descriptografadas. As senhas podem ser visíveis em definições de fonte de dados e scripts salvos em disco, em backups e em arquivos de log. Nunca use uma senha de administrador nesse tipo de conexão. Consulte o administrador da rede para obter orientações sobre segurança específicas a seu ambiente.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de servidores vinculados &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droplinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
