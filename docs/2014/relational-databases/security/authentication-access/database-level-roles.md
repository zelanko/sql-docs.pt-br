---
title: Funções de nível de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 09/22/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server 2014
f1_keywords:
- sql12.swb.roleproperties.database.f1
- sql12.swb.roleproperties.general.f1
- sql12.swb.roleproperties.object.f1
- SQL12.SWB.DBROLEPROPERTIES.GENERAL.F1
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
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 337252b4b5203003bc6bec6b44b12d86183ab343
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37188053"
---
# <a name="database-level-roles"></a>Funções de nível de banco de dados
  Para gerenciar facilmente as permissões em seus bancos de dados, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece várias *funções* , que são entidades de segurança que agrupam outras entidades. Elas são como ***grupos*** no sistema operacional [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. As funções de nível de banco de dados são permitidas em todo banco de dados em seus escopos de permissões.  
  
 Há dois tipos de funções no nível do banco de dados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: *funções de banco de dados fixas* , que são predefinidas no banco de dados, e *funções de banco de dados flexíveis* , que você cria.  
  
 As funções de banco de dados fixas são definidas no nível de banco de dados e existem em cada banco de dados. Os membros da função de banco de dados **db_owner** podem gerenciar a associação de funções de banco de dados fixas. Também há algumas funções de banco de dados fixas com finalidade especial no banco de dados msdb.  
  
 Você pode adicionar qualquer conta de banco de dados e outras funções do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nas funções de nível de banco de dados. Cada membro de uma função de banco de dados fixa pode adicionar outros logons a essa mesma função.  
  
> [!IMPORTANT]  
>  Não adicione funções de banco de dados flexíveis como membros de funções fixas. Isso poderia habilitar o escalonamento não intencional de privilégios.  
  
 A tabela a seguir mostra as funções de nível de banco de dados fixas e seus recursos. Essas funções existem em todos os bancos de dados.  
  
|Nome da função no nível do banco de dados|Description|  
|-------------------------------|-----------------|  
|**db_owner**|Os membros da função de banco de dados fixa **db_owner** podem executar todas as atividades de configuração e manutenção no banco de dados, bem como descartar o banco de dados.|  
|**db_securityadmin**|Os membros da função de banco de dados fixa **db_securityadmin** podem modificar a associação de funções e gerenciar permissões. A adição de entidades nesta função pode habilitar o escalonamento não intencional de privilégios.|  
|**db_accessadmin**|Os membros da função de banco de dados fixa **db_accessadmin** podem adicionar ou remover o acesso ao banco de dados para logons do Windows, grupos do Windows e logons do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|**db_backupoperator**|Os membros da função de banco de dados fixa **db_backupoperator** podem fazer backup do banco de dados.|  
|**db_ddladmin**|Os membros da função de banco de dados fixa **db_ddladmin** podem executar qualquer comando Data Definition Language (DDL) em um banco de dados.|  
|**db_datawriter**|Os membros da função de banco de dados fixa **db_datawriter** podem adicionar, excluir ou alterar dados em todas as tabelas de usuário.|  
|**db_datareader**|Os membros da função de banco de dados fixa **db_datareader** podem ler todos os dados de todas as tabelas de usuário.|  
|**db_denydatawriter**|Os membros da função de banco de dados fixa **db_denydatawriter** não podem adicionar, modificar ou excluir nenhum dado nas tabelas de usuário de um banco de dados.|  
|**db_denydatareader**|Os membros da função de banco de dados fixa **db_denydatareader** não podem ler nenhum dado nas tabelas de usuário de um banco de dados.|  
  
## <a name="msdb-roles"></a>Funções msdb  
 O banco de dados msdb contém as funções com finalidade especial que são mostradas na tabela a seguir.  
  
|Nome da função msdb|Description|  
|--------------------|-----------------|  
|`db_ssisadmin`<br /><br /> **db_ssisoperator**<br /><br /> **db_ssisltduser**|Os membros dessas funções de banco de dados podem administrar e usar o [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. As instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que são atualizadas de uma versão anterior podem conter uma versão mais antiga da função que foi nomeada com o DTS (Data Transformation Services), e não com o [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. Para obter mais informações, veja [Funções do Integration Services &#40;Serviço do SSIS&#41;](../../../integration-services/security/integration-services-roles-ssis-service.md).|  
|`dc_admin`<br /><br /> **dc_operator**<br /><br /> **dc_proxy**|Os membros dessas funções de banco de dados podem administrar e usar o coletor de dados. Para obter mais informações, consulte [Data Collection](../../data-collection/data-collection.md).|  
|**PolicyAdministratorRole**|Os membros da função de banco de dados **db_ PolicyAdministratorRole** podem executar todas as atividades de configuração e manutenção nas políticas condições do Gerenciamento Baseado em Políticas. Para obter mais informações, veja [Administrar servidores usando o gerenciamento baseado em políticas](../../policy-based-management/administer-servers-by-using-policy-based-management.md).|  
|**ServerGroupAdministratorRole**<br /><br /> **ServerGroupReaderRole**|Os membros dessas funções de banco de dados podem administrar e usar grupos de servidores registrados.|  
|**dbm_monitor**|Criado no `msdb` quando o primeiro banco de dados é registrado no Monitor de espelhamento de banco de dados do banco de dados. A função **dbm_monitor** não tem nenhum membro até que um administrador do sistema atribua usuários à função.|  
  
> [!IMPORTANT]  
>  Os membros das funções db_ssisadmin e dc_admin podem elevar seus privilégios para sysadmin. Essa elevação de privilégios pode ocorrer porque essas funções podem modificar os pacotes do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] e os pacotes do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] podem ser executados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o contexto de segurança sysadmin do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent. Para se proteger contra essa elevação de privilégios ao executar planos de manutenção, conjuntos de coletas de dados e outros pacotes do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], configure os trabalhos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent que executam pacotes para usar uma conta proxy com privilégios limitados ou apenas adicione membros sysadmin às funções db_ssisadmin e dc_admin.  
  
## <a name="working-with-database-level-roles"></a>Trabalhando com funções de nível de banco de dados  
 A tabela a seguir explica os comandos, exibições e funções para trabalhar com funções de nível de banco de dados.  
  
|Recurso|Tipo|Description|  
|-------------|----------|-----------------|  
|[sp_helpdbfixedrole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql)|Metadados|Retorna uma lista das funções de banco de dados fixas.|  
|[sp_dbfixedrolepermission &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql)|Metadados|Exibe as permissões de uma função de banco de dados fixa.|  
|[sp_helprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprole-transact-sql)|Metadados|Retorna informações sobre as funções no banco de dados atual.|  
|[sp_helprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql)|Metadados|Retorna informações sobre os membros de uma função no banco de dados atual.|  
|[sys.database_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-role-members-transact-sql)|Metadados|Retorna uma linha para cada membro de cada função de banco de dados.|  
|[IS_MEMBER &#40;Transact-SQL&#41;](/sql/t-sql/functions/is-member-transact-sql)|Metadados|Indica se o usuário atual é um membro do grupo Microsoft Windows especificado ou da função de banco de dados do Microsoft SQL Server.|  
|[CREATE ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-role-transact-sql)|Comando|Cria uma nova função de banco de dados no banco de dados atual.|  
|[ALTER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-role-transact-sql)|Comando|Altera o nome de uma função de banco de dados.|  
|[DROP ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-role-transact-sql)|Comando|Remove uma função do banco de dados.|  
|[sp_addrole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrole-transact-sql)|Comando|Cria uma nova função de banco de dados no banco de dados atual.|  
|[sp_droprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droprole-transact-sql)|Comando|Remove uma função de banco de dados do banco de dados atual.|  
|[sp_addrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)|Comando|Adiciona um usuário de banco de dados, uma função de banco de dados, o logon do Windows ou um grupo do Windows em uma função de banco de dados no banco de dados atual.|  
|[sp_droprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)|Comando|Remove uma conta de segurança de uma função do SQL Server no banco de dados atual.|  
  
## <a name="public-database-role"></a>Função de banco de dados pública  
 Cada usuário do banco de dados pertence à função de banco de dados **pública** . Quando permissões específicas não são concedidas ou são negadas a um usuário em um objeto seguro, o usuário herda as permissões concedidas como **públicas** naquele objeto.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/security-catalog-views-transact-sql)  
  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/security-stored-procedures-transact-sql)  
  
 [Funções de segurança &#40;Transact-SQL&#41;](/sql/t-sql/functions/security-functions-transact-sql)  
  
 [Protegendo o SQL Server](../securing-sql-server.md)  
  
 [sp_helprotect &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprotect-transact-sql)  
  
  
