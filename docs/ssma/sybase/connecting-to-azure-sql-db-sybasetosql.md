---
title: Conectar-se ao banco de dados do SQL Azure (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 823532a0107db9bcbc6781f25466fb135ffeeefe
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="connecting-to-azure-sql-db-sybasetosql"></a>Conectar-se ao banco de dados do SQL Azure (SybaseToSQL)
Para migrar bancos de dados Sybase para o banco de dados de SQL do Azure, você deve se conectar à instância de destino de banco de dados de SQL do Azure. Quando você se conectar, SSMA obtém metadados sobre todos os bancos de dados na instância do banco de dados de SQL do Azure e exibe os metadados de banco de dados no Gerenciador de metadados de banco de dados do Azure SQL. O SSMA armazena informações da instância do Azure SQL DB está conectado, mas não armazena as senhas.  
  
Sua conexão ao banco de dados de SQL do Azure permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve reconectar ao banco de dados de SQL Azure se você quiser uma conexão ativa com o servidor. Você pode trabalhar offline até que você carregar objetos de banco de dados no banco de dados de SQL do Azure e migrar dados.  
  
Metadados sobre a instância do banco de dados do Azure SQL não está sincronizado automaticamente. Em vez disso, para atualizar os metadados no Gerenciador de metadados de banco de dados de SQL do Azure, você deve atualizar manualmente os metadados do banco de dados de SQL do Azure. Para obter mais informações, consulte a seção "Sincronização de metadados do Azure SQL DB" mais adiante neste tópico.  
  
## <a name="required-azure-sql-db-permissions"></a>Permissões de banco de dados SQL do Azure necessárias  
A conta que é usada para se conectar ao banco de dados de SQL do Azure requer permissões diferentes dependendo de ações que realiza a conta:  
  
1.  Para converter objetos Sybase para [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxe, para atualizar os metadados do banco de dados de SQL do Azure, ou salvar sintaxe convertido para scripts, a conta deve ter permissão para fazer logon na instância do banco de dados de SQL do Azure.  
  
2.  Para carregar objetos de banco de dados no banco de dados de SQL do Azure, o requisito mínimo de permissão é a associação de **db_owner** função de banco de dados no banco de dados de destino.  
  
## <a name="establishing-a-azure-sql-db-connection"></a>Estabelecer uma Conexão de banco de dados SQL do Azure  
Antes de converter objetos de banco de dados Sybase a sintaxe do banco de dados de SQL do Azure, você deve estabelecer uma conexão com a instância do banco de dados do SQL Azure em que você deseja migrar os bancos de dados ou o banco de dados Sybase.  
  
Quando você define as propriedades de conexão, você também especificar o banco de dados onde objetos e dados serão migrados. Você pode personalizar esse mapeamento no nível do esquema Sybase depois que você se conectar ao banco de dados de SQL do Azure. Para obter mais informações, consulte [mapeamento Sybase ASE esquemas para esquemas SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> Antes de tentar se conectar ao banco de dados do Azure SQL, certifique-se de que a instância do banco de dados do Azure SQL está em execução e pode aceitar conexões.  
  
**Para se conectar ao banco de dados de SQL do Azure**  
  
1.  Sobre o **arquivo** menu, selecione **conectar-se ao banco de dados do Azure SQL**(essa opção é habilitada após a criação de um projeto).  
  
    Se você se conectou anteriormente para o banco de dados do Azure SQL, o nome do comando será **reconectar-se ao banco de dados de SQL do Azure**  
  
2.  Na caixa de diálogo de conexão, digite ou selecione o nome do servidor de banco de dados de SQL do Azure.  
  
3.  Insira, selecione ou **procurar** o nome do banco de dados.  
  
4.  Insira ou selecione **nome de usuário**.  
  
5.  Insira o **senha**.  
  
6.  O SSMA recomenda conexão criptografada para o banco de dados do Azure SQL.  
  
7.  Clique em **Conectar**.  
  
> [!IMPORTANT]  
> SSMA para Sybase não oferece suporte a conexão para **mestre** banco de dados no banco de dados de SQL do Azure.  
  
## <a name="synchronizing-azure-sql-db-metadata"></a>Sincronizar metadados de banco de dados SQL do Azure  
Metadados sobre bancos de dados do banco de dados do Azure SQL não é atualizado automaticamente. Os metadados no Gerenciador de metadados de banco de dados de SQL Azure são um instantâneo dos metadados quando você primeiro conectado ao banco de dados de SQL do Azure, ou a última vez que você atualizou manualmente os metadados. Você pode atualizar manualmente os metadados para todos os bancos de dados ou para qualquer banco de dados ou objeto de banco de dados.  
  
**Para sincronizar os metadados**  
  
1.  Certifique-se de que você está conectado ao banco de dados de SQL do Azure.  
  
2.  No Gerenciador de metadados do banco de dados do SQL Azure, selecione a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.  
  
    Por exemplo, para atualizar os metadados para todos os bancos de dados, marque a caixa ao lado de bancos de dados.  
  
3.  Bancos de dados, ou o banco de dados individual ou o esquema de banco de dados e, em seguida, selecione **sincronizar com o banco de dados**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento entre esquemas Sybase e bancos de dados do banco de dados de SQL do Azure e esquemas, consulte [mapeamento Sybase ASE esquemas para esquemas SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   Para personalizar opções de configuração para os projetos, consulte [definindo opções de projeto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeamento Sybase ASE e tipos de dados do SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   Se você não precisa executar qualquer uma dessas tarefas, você pode converter as definições de objeto de banco de dados Sybase em definições de objeto de banco de dados de SQL do Azure. Para obter mais informações, consulte [converter objetos de banco de dados do Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados Sybase ASE para o SQL Server - banco de dados SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
