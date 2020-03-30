---
title: Bancos de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- data warehouse [SQL Server]
- OLTP databases [SQL Server]
- databases [SQL Server], about databases
ms.assetid: 316eea58-81b8-4bf3-a1fc-801946740e94
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2763a57a55a65d049be595d2286343eb5ba323ba
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68109716"
---
# <a name="databases"></a>Bancos de dados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Um banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é composto de uma coleção de tabelas que armazena um conjunto específico de dados estruturados. Uma tabela contém uma coleção de linhas, também chamadas de registros ou tuplas, e colunas, também chamadas de atributos. Cada coluna da tabela é projetada para armazenar um determinado tipo de informação, por exemplo, datas, nomes, valores em dinheiro e números.  
  
## <a name="basic-information-about-databases"></a>Informações básicas sobre bancos de dados  
 Um computador pode ter uma ou mais de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada. Cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode conter um ou mais bancos de dados.  Dentro de um banco de dados, há um ou vários grupos de propriedade de objeto denominados esquemas. Em cada esquema, há objetos de banco de dados como tabelas, exibições e procedimentos armazenados. Alguns objetos, como certificados e chaves assimétricas, estão contidos no banco de dados, mas não estão contidos em um esquema. Para obter mais informações sobre como criar tabelas, consulte [Tabelas](../../relational-databases/tables/tables.md).  
  
 Os bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são armazenados em arquivos do sistema de arquivos. Os arquivos podem ser agrupados em grupos de arquivos. Para obter mais informações sobre como os arquivos e grupos de arquivos, consulte [Arquivos e grupos de arquivos do banco de dados](../../relational-databases/databases/database-files-and-filegroups.md).  
  
 Quando as pessoas obtiverem acesso a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , elas serão identificadas como um logon. Quando as pessoas obtiverem acesso a um banco de dados, elas serão identificadas como um usuário de banco de dados. Um usuário de banco de dados pode ser baseado em um logon. Se forem habilitados bancos de dados independentes, um usuário de banco de dados não baseado em logon poderá ser criado. Para obter mais informações sobre usuários, consulte [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md).  
  
 Um usuário que tem acesso a um banco de dados pode receber permissão para acessar os objetos no banco de dados. Embora possam ser concedidas permissões a usuários individuais, é recomendável criar funções de banco de dados, adicionando os usuários de banco de dados às funções, e conceder permissão de acesso às funções. A concessão de permissões a funções, e não a usuários, faz com que seja mais fácil manter as permissões consistentes e compreensíveis à medida que o número de usuários aumenta e muda continuamente. Para obter mais informações sobre permissões de funções, consulte [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md) e [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md).  
  
## <a name="working-with-databases"></a>Trabalhando com bancos de dados  
 A maioria das pessoas que trabalha com bancos de dados usa a ferramenta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . A ferramenta [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] tem uma interface gráfica do usuário para criar bancos de dados e objetos nos bancos de dados. O [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] também tem um editor de consultas para interagir com bancos de dados gravando instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. O [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] pode ser instalado no disco de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou baixado do MSDN. Para saber mais sobre a ferramenta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], consulte [SQL Server Management Studio (SSMS)](../../ssms/sql-server-management-studio-ssms.md).
  
## <a name="in-this-section"></a>Nesta seção  
  
|||  
|-|-|  
|[Bancos de dados do sistema](../../relational-databases/databases/system-databases.md)|[Excluir arquivos de dados ou de log de um banco de dados](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)|  
|[Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)|[Exibir dados e informações de espaço de log para um banco de dados](../../relational-databases/databases/display-data-and-log-space-information-for-a-database.md)|  
|[Arquivos de dados do SQL Server no Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)|[Aumentar o tamanho de um banco de dados](../../relational-databases/databases/increase-the-size-of-a-database.md)|  
|[Arquivos e grupos de arquivos do banco de dados](../../relational-databases/databases/database-files-and-filegroups.md)|[Renomear um banco de dados](../../relational-databases/databases/rename-a-database.md)|  
|[Estados de banco de dados](../../relational-databases/databases/database-states.md)|[Definir um banco de dados como modo de usuário único](../../relational-databases/databases/set-a-database-to-single-user-mode.md)|  
|[Estados de arquivo](../../relational-databases/databases/file-states.md)|[Reduzir um banco de dados](../../relational-databases/databases/shrink-a-database.md)|  
|[Estimar o tamanho de um banco de dados](../../relational-databases/databases/estimate-the-size-of-a-database.md)|[Reduzir um arquivo](../../relational-databases/databases/shrink-a-file.md)|  
|[Copiar bancos de dados para outros servidores](../../relational-databases/databases/copy-databases-to-other-servers.md)|[Exibir ou alterar as propriedades de um banco de dados](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md)|  
|[Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)|[Exibir uma lista de bancos de dados em uma instância do SQL Server](../../relational-databases/databases/view-a-list-of-databases-on-an-instance-of-sql-server.md)|  
|[Adicionar arquivos de dados ou de log a um banco de dados](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)|[Exibir ou alterar o nível de compatibilidade de um banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)|  
|[Alterar as definições de configuração de um banco de dados](../../relational-databases/databases/change-the-configuration-settings-for-a-database.md)|[Usar o Assistente de Plano de Manutenção](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)|  
|[Criar um banco de dados](../../relational-databases/databases/create-a-database.md)|[Criar um alias de tipo de dados definido pelo usuário](../../relational-databases/databases/create-a-user-defined-data-type-alias.md)|  
|[Excluir um banco de dados](../../relational-databases/databases/delete-a-database.md)|[Instantâneos de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Índices](../../relational-databases/indexes/indexes.md)  
  
 [Exibições](../../relational-databases/views/views.md)  
  
 [Procedimentos armazenados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)  
  
  
