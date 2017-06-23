---
title: "Funções de nível de banco de dados | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.roleproperties.database.f1
- sql13.swb.roleproperties.object.f1
- SQL13.SWB.DBROLEPROPERTIES.GENERAL.F1
- sql13.swb.roleproperties.general.f1
helpviewer_keywords:
- db_denydatareader role
- users [SQL Server], database roles
- database-level roles [SQL Server]
- db_denydatawriter role
- roles [SQL Server], database
- principals [SQL Server], database-level
- db_backupoperator role
- credentials [SQL Server], roles
- db_accessadmin role
- schemas [SQL Server], roles
- permissions [SQL Server], roles
- database roles [SQL Server], listed
- db_datareader role
- db_ddladmin role
- db_datawriter role
- db_securityadmin role
- db_owner role
- database roles [SQL Server]
- fixed database roles [SQL Server]
- authentication [SQL Server], roles
- groups [SQL Server], roles
ms.assetid: 7f3fa5f6-6b50-43bb-9047-1544ade55e39
caps.latest.revision: 49
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: 411da6974090c9ccad6aa6184c248537bfdebe79
ms.contentlocale: pt-br
ms.lasthandoff: 06/23/2017

---
# <a name="database-level-roles"></a>Funções de nível de banco de dados
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../../includes/tsql-appliesto-ss2008-all-md.md)]

  Para gerenciar facilmente as permissões em seus bancos de dados, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece várias *funções* , que são entidades de segurança que agrupam outras entidades. Elas são como ***grupos*** no sistema operacional [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. As funções de nível de banco de dados são permitidas em todo banco de dados em seus escopos de permissões.  

Para adicionar e remover usuários de uma função de banco de dados, use as opções `ADD MEMBER` e `DROP MEMBER` da instrução [ALTER ROLE](../../../t-sql/statements/alter-role-transact-sql.md) . [!INCLUDE[ssPDW_md](../../../includes/sspdw-md.md)] não dá suporte ao uso de `ALTER ROLE`. Em vez disso, use os antigos procedimentos [sp_addrolemember](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) e [sp_droprolemember](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) .
  
 Há dois tipos de funções no nível do banco de dados: *funções de banco de dados fixas* , que são predefinidas no banco de dados, e *funções de banco de dados definidas por usuário* , que você pode criar.  
  
 As funções de banco de dados fixas são definidas no nível de banco de dados e existem em cada banco de dados. Os membros da função de banco de dados **db_owner** podem gerenciar a associação a funções de banco de dados fixas. Também há algumas funções de banco de dados com finalidade especial no banco de dados msdb.  
  
 Você pode adicionar qualquer conta de banco de dados e outras funções do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nas funções de nível de banco de dados. Cada membro de uma função de banco de dados fixa pode adicionar outros usuários a essa mesma função.  
  
> [!TIP]  
>  Não adicione funções de banco de dados definidas pelo usuário como membros de funções fixas. Isso poderia habilitar o escalonamento não intencional de privilégios.  

As permissões de funções de banco de dados definidas pelo usuário podem ser personalizadas com instruções GRANT, DENY e REVOKE. Para obter mais informações, consulte [Permissões (Mecanismo de Banco de Dados)](../../../relational-databases/security/permissions-database-engine.md).

Para obter uma lista de todas as permissões, consulte o cartaz [Permissões do Mecanismo de Banco de Dados](http://go.microsoft.com/fwlink/?LinkId=229142) . (As permissões em nível de servidor não podem ser concedidas às funções de banco de dados. Logons e outras entidades em nível de servidor – como funções de servidor – não podem ser adicionados às funções de banco de dados. Para a segurança em nível de servidor no [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)], use [funções de servidor](../../../relational-databases/security/authentication-access/server-level-roles.md) . As permissões em nível de servidor não podem ser concedidas por meio das funções no [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] e [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)].)

## <a name="fixed-database-roles"></a>funções de banco de dados fixas
  
 A tabela a seguir mostra as funções de banco de dados fixas e suas funcionalidades. Essas funções existem em todos os bancos de dados. Exceto para o **pública** função de banco de dados, as permissões atribuídas às funções de banco de dados fixa não pode ser alterada.   
  
|Nome da função de banco de dados fixa|Description|  
|-------------------------------|-----------------|  
|**db_owner**|Os membros da função de banco de dados fixa **db_owner** podem executar todas as atividades de configuração e manutenção no banco de dados, bem como remover o banco de dados no [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)]. (No [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] e [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)], algumas atividades de manutenção exigem permissões em nível de servidor e não podem ser executadas por **db_owners**.)|  
|**db_securityadmin**|Os membros da função de banco de dados fixa **db_securityadmin** podem modificar a associação de funções e gerenciar permissões. A adição de entidades nesta função pode habilitar o escalonamento não intencional de privilégios.|  
|**db_accessadmin**|Os membros da função de banco de dados fixa **db_accessadmin** podem adicionar ou remover o acesso ao banco de dados para logons do Windows, grupos do Windows e logons do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|**db_backupoperator**|Os membros da função de banco de dados fixa **db_backupoperator** podem fazer backup do banco de dados.|  
|**db_ddladmin**|Os membros da função de banco de dados fixa **db_ddladmin** podem executar qualquer comando Data Definition Language (DDL) em um banco de dados.|  
|**db_datawriter**|Os membros da função de banco de dados fixa **db_datawriter** podem adicionar, excluir ou alterar dados em todas as tabelas de usuário.|  
|**db_datareader**|Os membros da função de banco de dados fixa **db_datareader** podem ler todos os dados de todas as tabelas de usuário.|  
|**db_denydatawriter**|Os membros da função de banco de dados fixa **db_denydatawriter** não podem adicionar, modificar ou excluir nenhum dado nas tabelas de usuário de um banco de dados.|  
|**db_denydatareader**|Os membros da função de banco de dados fixa **db_denydatareader** não podem ler nenhum dado nas tabelas de usuário de um banco de dados.|  

As permissões atribuídas às funções de banco de dados fixas não podem ser alteradas. A seguinte figura mostra as permissões atribuídas às funções de banco de dados fixas:

![fixed_database_role_permissions](../../../relational-databases/security/authentication-access/media/permissions-of-database-roles.png)

## <a name="special-roles-for-includesssdsmdincludessssds-mdmd-and-includesssdwmdincludessssdw-mdmd"></a>Funções especiais para [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] e [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)]

Essas funções de banco de dados existem somente no banco de dados mestre virtual. As permissões são restritas às ações executadas no mestre. Somente os usuários de banco de dados no mestre podem ser adicionados a essas funções. Logons não podem ser adicionados a essas funções, mas é possível criar usuários com base nos logons e esses usuários podem ser adicionados às funções. Os usuários de banco de dados independente no mestre também podem ser adicionados a essas funções.

|Nome da função|Description|  
|--------------------|-----------------|
**dbmanager** | Pode criar e excluir bancos de dados. Um membro da função dbmanager que cria um banco de dados se torna o proprietário desse banco de dados, o que permite ao usuário se conectar ao banco de dados como o usuário dbo. O usuário dbo tem todas as permissões de banco de dados no banco de dados. Os membros da função dbmanager necessariamente não tem permissão para acessar bancos de dados que eles não possuem.
**loginmanager** | Pode criar e excluir logons no banco de dados mestre virtual.  

> [!NOTE]
> A entidade de segurança em nível de servidor e o Administrador do Azure Active Directory (se estiver configurado) têm todas as permissões no [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] e [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)] sem precisar ser membros das funções. Para obter mais informações, consulte [Autenticação e autorização do Banco de Dados SQL: Concedendo o acesso](https://azure.microsoft.com/documentation/articles/sql-database-manage-logins/). 
  
## <a name="msdb-roles"></a>Funções msdb  
 O banco de dados msdb contém as funções com finalidade especial que são mostradas na tabela a seguir.  
  
|Nome da função msdb|Description|  
|--------------------|-----------------|  
|**db_ssisadmin**<br /><br /> **db_ssisoperator**<br /><br /> **db_ssisltduser**|Os membros dessas funções de banco de dados podem administrar e usar o [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. As instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que são atualizadas de uma versão anterior podem conter uma versão mais antiga da função que foi nomeada com o DTS (Data Transformation Services), e não com o [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. Para obter mais informações, veja [Funções do Integration Services &#40;Serviço do SSIS&#41;](../../../integration-services/security/integration-services-roles-ssis-service.md).|  
|**dc_admin**<br /><br /> **dc_operator**<br /><br /> **dc_proxy**|Os membros dessas funções de banco de dados podem administrar e usar o coletor de dados. Para obter mais informações, consulte [Data Collection](../../../relational-databases/data-collection/data-collection.md).|  
|**PolicyAdministratorRole**|Os membros da função de banco de dados **db_ PolicyAdministratorRole** podem executar todas as atividades de configuração e manutenção nas políticas condições do Gerenciamento Baseado em Políticas. Para obter mais informações, veja [Administrar servidores usando o gerenciamento baseado em políticas](../../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md).|  
|**ServerGroupAdministratorRole**<br /><br /> **ServerGroupReaderRole**|Os membros dessas funções de banco de dados podem administrar e usar grupos de servidores registrados.|  
|**dbm_monitor**|Criada no banco de dados **msdb** quando o primeiro banco de dados é registrado no Monitor de Espelhamento de Banco de Dados. A função **dbm_monitor** não tem nenhum membro até que um administrador do sistema atribua usuários à função.|  
  
> [!IMPORTANT]  
>  Os membros das funções **db_ssisadmin** e **dc_admin** podem elevar seus privilégios para sysadmin. Essa elevação de privilégios pode ocorrer porque essas funções podem modificar os pacotes do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] e os pacotes do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] podem ser executados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o contexto de segurança sysadmin do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent. Para se proteger contra essa elevação de privilégio ao executar planos de manutenção, conjuntos de coletas de dados e outros pacotes do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , configure os trabalhos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent que executam pacotes para usar uma conta proxy com privilégios limitados ou apenas adicione membros **sysadmin** às funções **db_ssisadmin** e **dc_admin** .  

## <a name="working-with-r-services"></a>Trabalhando com serviços de R  

**Aplica-se a:** SQL Server a partir de [!INCLUDE[ssSQLv14_md](../../../includes/sssqlv14-md.md)]   

Quando o R Services está instalado, as funções adicionais de banco de dados ficam disponíveis para gerenciar pacotes. Para obter mais informações, consulte [Gerenciamento de pacotes de R para o SQL Server](../../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md).

|Nome da função |Description|  
|-------------|-----------------|
|**rpkgs-users** |Permite que usuários usem quaisquer pacotes compartilhados que foram instalados por membros da função rpkgs-shared.|
|**rpkgs-private** |Fornece acesso a pacotes compartilhados com as mesmas permissões que a função rpkgs-users. Os membros desta função também podem instalar, remover e usar pacotes com escopo definido como particular.|
|**rpkgs-shared** |Fornece as mesmas permissões que a função pkgs-private. Os usuários que são membros dessa função também podem instalar ou remover pacotes compartilhados.|
  
## <a name="working-with-database-level-roles"></a>Trabalhando com funções de nível de banco de dados  
 A tabela a seguir explica os comandos, exibições e funções para trabalhar com funções de nível de banco de dados.  
  
|Recurso|Tipo|Description|  
|-------------|----------|-----------------|  
|[sp_helpdbfixedrole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md)|Metadados|Retorna uma lista das funções de banco de dados fixas.|  
|[sp_dbfixedrolepermission &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql.md)|Metadados|Exibe as permissões de uma função de banco de dados fixa.|  
|[sp_helprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)|Metadados|Retorna informações sobre as funções no banco de dados atual.|  
|[sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)|Metadados|Retorna informações sobre os membros de uma função no banco de dados atual.|  
|[sys.database_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)|Metadados|Retorna uma linha para cada membro de cada função de banco de dados.|  
|[IS_MEMBER &#40;Transact-SQL&#41;](../../../t-sql/functions/is-member-transact-sql.md)|Metadados|Indica se o usuário atual é um membro do grupo Microsoft Windows especificado ou da função de banco de dados do Microsoft SQL Server.|  
|[CREATE ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-role-transact-sql.md)|Comando|Cria uma nova função de banco de dados no banco de dados atual.|  
|[ALTER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-role-transact-sql.md)|Comando|Altera o nome ou a associação de uma função de banco de dados.|  
|[DROP ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-role-transact-sql.md)|Comando|Remove uma função do banco de dados.|  
|[sp_addrole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)|Comando|Cria uma nova função de banco de dados no banco de dados atual.|  
|[sp_droprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)|Comando|Remove uma função de banco de dados do banco de dados atual.|  
|[sp_addrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)|Comando|Adiciona um usuário de banco de dados, uma função de banco de dados, o logon do Windows ou um grupo do Windows em uma função de banco de dados no banco de dados atual. Todas as plataformas, exceto [!INCLUDE[ssPDW_md](../../../includes/sspdw-md.md)], devem usar o `ALTER ROLE` em vez disso.|  
|[sp_droprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)|Comando|Remove uma conta de segurança de uma função do SQL Server no banco de dados atual. Todas as plataformas, exceto [!INCLUDE[ssPDW_md](../../../includes/sspdw-md.md)] , devem usar o `ALTER ROLE` em vez disso.|
|[GRANT](../../../t-sql/statements/grant-transact-sql.md)| Permissões | Adiciona a permissão a uma função.
|[DENY](../../../t-sql/statements/deny-transact-sql.md)| Permissões | Nega uma permissão a uma função.
|[REVOKE](../../../t-sql/statements/revoke-transact-sql.md)| Permissões | Remove uma permissão concedida ou negada anteriormente.
  
  
## <a name="public-database-role"></a>Função de banco de dados pública  
 Cada usuário do banco de dados pertence à função de banco de dados **pública** . Quando permissões específicas não são concedidas ou são negadas a um usuário em um objeto seguro, o usuário herda as permissões concedidas como **públicas** naquele objeto. Os usuários do banco de dados não podem ser removidos da função **pública** . 
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
 [Funções de segurança &#40;Transact-SQL&#41;](../../../t-sql/functions/security-functions-transact-sql.md)  
  
 [Protegendo o SQL Server](../../../relational-databases/security/securing-sql-server.md)  
  
 [sp_helprotect &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)  
  
  

