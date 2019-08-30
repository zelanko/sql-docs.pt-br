---
title: Bancos de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 7de13f529dc0aab0c897ebe3dc1cb19220b13fd7
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154579"
---
# <a name="databases"></a>Bancos de dados
  Um banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é composto de uma coleção de tabelas que armazena um conjunto específico de dados estruturados. Uma tabela contém uma coleção de linhas, também chamadas de registros ou tuplas, e colunas, também chamadas de atributos. Cada coluna da tabela é projetada para armazenar um determinado tipo de informação, por exemplo, datas, nomes, valores em dinheiro e números.  
  
## <a name="basic-information-about-databases"></a>Informações básicas sobre bancos de dados  
 Um computador pode ter uma ou mais de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada. Cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode conter um ou mais bancos de dados.  Dentro de um banco de dados, há um ou vários grupos de propriedade de objeto denominados esquemas. Em cada esquema, há objetos de banco de dados como tabelas, exibições e procedimentos armazenados. Alguns objetos, como certificados e chaves assimétricas, estão contidos no banco de dados, mas não estão contidos em um esquema. Para obter mais informações sobre como criar tabelas, consulte [Tabelas](../tables/tables.md).  
  
 Os bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são armazenados em arquivos do sistema de arquivos. Os arquivos podem ser agrupados em grupos de arquivos. Para obter mais informações sobre como os arquivos e grupos de arquivos, consulte [Arquivos e grupos de arquivos do banco de dados](database-files-and-filegroups.md).  
  
 Quando as pessoas obtiverem acesso a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , elas serão identificadas como um logon. Quando as pessoas obtiverem acesso a um banco de dados, elas serão identificadas como um usuário de banco de dados. Um usuário de banco de dados pode ser baseado em um logon. Se forem habilitados bancos de dados independentes, um usuário de banco de dados não baseado em logon poderá ser criado. Para obter mais informações sobre usuários, consulte [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql).  
  
 Um usuário que tem acesso a um banco de dados pode receber permissão para acessar os objetos no banco de dados. Embora possam ser concedidas permissões a usuários individuais, é recomendável criar funções de banco de dados, adicionando os usuários de banco de dados às funções, e conceder permissão de acesso às funções. A concessão de permissões a funções, e não a usuários, faz com que seja mais fácil manter as permissões consistentes e compreensíveis à medida que o número de usuários aumenta e muda continuamente. Para obter mais informações sobre permissões de funções, consulte [CREATE ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-role-transact-sql) e [Entidades &#40;Mecanismo de Banco de Dados&#41;](../security/authentication-access/principals-database-engine.md).  
  
## <a name="working-with-databases"></a>Trabalhando com bancos de dados  
 A maioria das pessoas que trabalha com bancos de dados usa a ferramenta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . A ferramenta [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] tem uma interface gráfica do usuário para criar bancos de dados e objetos nos bancos de dados. O [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] também tem um editor de consultas para interagir com bancos de dados gravando instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. O [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] pode ser instalado no disco de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou baixado do MSDN.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|||  
|-|-|  
|[Bancos de dados do sistema](system-databases.md)|[Excluir arquivos de dados ou de log de um banco de dados](delete-data-or-log-files-from-a-database.md)|  
|[Bancos de dados independentes](contained-databases.md)|[Exibir dados e informações de espaço de log para um banco de dados](display-data-and-log-space-information-for-a-database.md)|  
|[SQL Server arquivos de dados no Azure](sql-server-data-files-in-microsoft-azure.md)|[Aumentar o tamanho de um banco de dados](increase-the-size-of-a-database.md)|  
|[Arquivos e grupos de arquivos do banco de dados](database-files-and-filegroups.md)|[Renomear um banco de dados](rename-a-database.md)|  
|[Estados de banco de dados](database-states.md)|[Definir um banco de dados como modo de usuário único](set-a-database-to-single-user-mode.md)|  
|[Estados de arquivo](file-states.md)|[Reduzir um banco de dados](shrink-a-database.md)|  
|[Estimar o tamanho de um banco de dados](estimate-the-size-of-a-database.md)|[Reduzir um arquivo](shrink-a-file.md)|  
|[Copiar bancos de dados para outros servidores](copy-databases-to-other-servers.md)|[Exibir ou alterar as propriedades de um banco de dados](view-or-change-the-properties-of-a-database.md)|  
|[Anexar e desanexar bancos de dados &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)|[Exibir uma lista de bancos de dados em uma instância do SQL Server](view-a-list-of-databases-on-an-instance-of-sql-server.md)|  
|[Adicionar arquivos de dados ou de log a um banco de dados](add-data-or-log-files-to-a-database.md)|[Exibir ou alterar o nível de compatibilidade de um banco de dados](view-or-change-the-compatibility-level-of-a-database.md)|  
|[Alterar as definições de configuração de um banco de dados](change-the-configuration-settings-for-a-database.md)|[Usar o Assistente de Plano de Manutenção](../maintenance-plans/use-the-maintenance-plan-wizard.md)|  
|[Criar um banco de dados](create-a-database.md)|[Criar um alias de tipo de dados definido pelo usuário](create-a-user-defined-data-type-alias.md)|  
|[Excluir um banco de dados](delete-a-database.md)|[Instantâneos de banco de dados &#40;SQL Server&#41;](database-snapshots-sql-server.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Índices](../indexes/indexes.md)  
  
 [Exibições](../views/views.md)  
  
 [Procedimentos armazenados &#40;Mecanismo de Banco de Dados&#41;](../stored-procedures/stored-procedures-database-engine.md)  
  
  
