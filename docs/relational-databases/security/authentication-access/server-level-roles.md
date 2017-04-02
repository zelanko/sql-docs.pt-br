---
title: "Fun&#231;&#245;es de n&#237;vel de servidor | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.Security.NT_AUTHORITY.SYSTEM"
  - "sql13.Security.BUILTIN.administrators"
helpviewer_keywords: 
  - "funções [SQL Server], nível de servidor"
  - "entidades [SQL Server], nível de servidor"
  - "Permissão CONTROL SERVER"
  - "funções de servidor fixas [SQL Server]"
  - "credenciais [SQL Server], funções"
  - "função de servidor fixa sysadmin"
  - "funções de nível de servidor [SQL Server]"
  - "autenticação [SQL Server], funções"
ms.assetid: 7adf2ad7-015d-4cbe-9e29-abaefd779008
caps.latest.revision: 52
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 50
---
# Fun&#231;&#245;es de n&#237;vel de servidor
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece funções do nível de servidor para ajudar a gerenciar as permissões em um servidor. Estas funções são entidades de segurança que agrupam outras entidades de segurança. Essas funções abrangem todo o servidor em seus escopos de permissões. (As *funções* são como *grupos* no sistema operacional Windows.)  
  
 As funções de servidor fixas são fornecidas para conveniência e compatibilidade com versões anteriores. Atribua mais permissões específicas sempre que possível.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece nove funções de servidor fixas. A permissões que são concedidas às funções de servidor fixas não podem ser alteradas. A partir do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], você pode criar funções de servidor definidas pelo usuário e adicionar permissões do nível de servidor às funções de servidor definidas pelo usuário.  
  
 Você pode adicionar entidades de segurança no nível do servidor (logons do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], contas do Windows e grupos do Windows) em funções de nível de servidor. Cada membro de uma função de servidor fixa pode adicionar outros logons a essa mesma função. Os membros de funções de servidor definidas pelo usuário não podem acrescentar outras entidades de segurança de servidor à função.  
  
## Funções fixas de nível de servidor  
 A tabela a seguir mostra as funções fixas de nível de servidor e seus recursos.  
  
|Função fixa de nível de servidor|Descrição|  
|------------------------------|-----------------|  
|sysadmin|Os membros da função de servidor fixa sysadmin podem executar qualquer atividade no servidor.|  
|serveradmin|Os membros da função de servidor fixa serveradmin podem alterar as opções de configuração de todo o servidor e fechar o servidor.|  
|securityadmin|Os membros da função de servidor fixa securityadmin gerenciam logons e suas propriedades. Eles podem CONCEDER, NEGAR e REVOGAR permissões de nível de servidor. Também podem executar as permissões de nível de banco de dados GRANT, DENY e REVOKE se tiverem acesso ao banco de dados. Além disso, eles podem redefinir senhas para logons do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> **\*\* Observação de segurança \*\*** A capacidade de permitir acesso ao [!INCLUDE[ssDE](../../../includes/ssde-md.md)] e de configurar permissões de usuário permite que o administrador de segurança atribua a maioria das permissões de servidor. A função **securityadmin** deve ser tratada como equivalente à função **sysadmin** .|  
|processadmin|Os membros da função de servidor fixa processadmin podem encerrar os processos em execução em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|setupadmin|Os membros da função de servidor fixa setupadmin podem adicionar e remover servidores vinculados usando instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)]. (A associação sysadmin é necessária ao usar o [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].)|  
|bulkadmin|Os membros da função de servidor fixa bulkadmin podem executar a instrução BULK INSERT.|  
|diskadmin|A função de servidor fixa diskadmin é usada para gerenciar arquivos em disco.|  
|dbcreator|Os membros da função de servidor fixa dbcreator podem criar, alterar, descartar e restaurar qualquer banco de dados.|  
|público|Todo logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pertence à função de servidor pública. Quando permissões específicas não são concedidas ou são negadas a uma entidade de servidor em um objeto seguro, o usuário herda as permissões concedidas como públicas naquele objeto. Somente atribua permissões públicas em qualquer objeto quando você quiser que ele esteja disponível para todos os usuários. Não é possível alterar associação em public.<br /><br /> Observação: public é implementado de modo diferente de outras funções. No entanto, as permissões podem ser concedidas, negadas ou revogadas e negadas por meio de public.|  
  
## Permissões de funções de servidor fixas  
 Cada função de servidor fixa tem certas permissões atribuídas a ela. Para um gráfico das permissões atribuídas às funções de servidor, consulte [Funções fixas de servidor e de banco de dados do Mecanismo de Banco de Dados](http://social.technet.microsoft.com/wiki/contents/articles/2024.database-engine-fixed-server-and-fixed-database-roles.aspx).  
  
> [!IMPORTANT]  
>  A permissão **CONTROL SERVER** é semelhante, mas não idêntica à função de servidor fixa do **sysadmin** . As permissões não implicam associações de função e as associações de função não concedem permissões. (Por ex.: **CONTROL SERVER** não implica a associação à função de servidor fixa **sysadmin**.) No entanto, às vezes é possível representar entre funções e permissões equivalentes. A maioria dos comandos **DBCC** e muitos procedimentos do sistema requerem associação na função de servidor fixa **sysadmin** . Para obter uma lista dos 171 procedimentos armazenados do sistema que exigem associação ao **sysadmin**, veja a seguinte postagem de blog de Andreas Wolter [CONTROL SERVER vs. sysadmin/sa: permissions, system procedures, DBCC, automatic schema creation and privilege escalation – caveats](http://www.insidesql.org/blogs/andreaswolter/2013/08/control-server-vs-sysadmin-sa-permissions-privilege-escalation-caveats).  
  
## Permissão em nível de servidor  
 Somente podem ser acrescentadas permissões do nível de servidor a funções de servidor definidas pelo usuário. Para listar as permissões em nível de servidor, execute a instrução a seguir. As permissões em nível de servidor são:  
  
```tsql  
SELECT * FROM sys.fn_builtin_permissions('SERVER') ORDER BY permission_name;  
```  
  
 Para obter mais informações sobre as permissões, veja [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/permissions-database-engine.md) e [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md).  
  
## Trabalhando com funções de nível de servidor  
 A tabela a seguir explica os comandos, exibições e funções que você pode usar para trabalhar com funções de nível de servidor.  
  
|Recurso|Tipo|Descrição|  
|-------------|----------|-----------------|  
|[sp_helpsrvrole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql.md)|Metadados|Retorna uma lista de funções de nível de servidor.|  
|[sp_helpsrvrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)|Metadados|Retorna informações sobre os membros de uma função de nível de servidor.|  
|[sp_srvrolepermission &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md)|Metadados|Exibe as permissões de uma função de nível de servidor.|  
|[IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../../t-sql/functions/is-srvrolemember-transact-sql.md)|Metadados|Indica se um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é membro da função de nível de servidor especificada.|  
|[sys.server_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)|Metadados|Retorna uma linha para cada membro de cada função de nível de servidor.|  
|[sp_addsrvrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)|Comando|Adiciona um logon como um membro de uma função de nível de servidor. Preterido. Use [ALTER SERVER ROLE](../../../t-sql/statements/alter-server-role-transact-sql.md) em vez disso.|  
|[sp_dropsrvrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)|Comando|Remove um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou um usuário ou grupo do Windows de uma função de nível de servidor. Preterido. Use [ALTER SERVER ROLE](../../../t-sql/statements/alter-server-role-transact-sql.md) em vez disso.|  
|[CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-role-transact-sql.md)|Comando|Cria uma função de servidor definida pelo usuário.|  
|[ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-role-transact-sql.md)|Comando|Altera a associação de uma função de servidor ou altera nome de uma função de servidor definida pelo usuário.|  
|[DROP SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-role-transact-sql.md)|Comando|Remove uma função de servidor definida pelo usuário.|  
|[IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../../t-sql/functions/is-srvrolemember-transact-sql.md)|Função|Determina associação de função de servidor.|  
  
## Consulte também  
 [Funções de nível de banco de dados](../../../relational-databases/security/authentication-access/database-level-roles.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../../t-sql/functions/security-functions-transact-sql.md)   
 [Protegendo o SQL Server](../../../relational-databases/security/securing-sql-server.md)   
 [Permissões GRANT de entidade do servidor &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [Permissões REVOKE de entidade do servidor &#40;Transact-SQL&#41;](../../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)   
 [Permissões DENY de entidade do servidor &#40;Transact-SQL&#41;](../../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)   
 [Criar uma função de servidor](../../../relational-databases/security/authentication-access/create-a-server-role.md)  
  
  