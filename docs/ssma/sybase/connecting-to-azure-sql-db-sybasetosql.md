---
title: Conectar-se ao banco de dados SQL do Azure (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3c7cd958002cd0df7002c13eda3cdcf8bfd870a8
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2018
ms.locfileid: "40395618"
---
# <a name="connecting-to-azure-sql-db-sybasetosql"></a>Conectar-se ao BD SQL do Azure (SybaseToSQL)
Para migrar bancos de dados Sybase para BD SQL do Azure, você deve se conectar à instância de destino de BD SQL do Azure. Quando você se conectar, o SSMA obtém metadados sobre todos os bancos de dados na instância do SQL do Azure e exibe metadados de banco de dados no Gerenciador de metadados de banco de dados do Azure SQL. O SSMA armazena as informações da instância do BD SQL do Azure estão conectados ao, mas não armazena as senhas.  
  
Sua conexão ao Azure SQL DB permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve se reconectar ao BD SQL do Azure se você quiser que uma conexão ativa com o servidor. Você pode trabalhar offline até que você carregar objetos de banco de dados no BD SQL do Azure e migra os dados.  
  
Metadados sobre a instância do SQL do Azure não será sincronizado automaticamente. Em vez disso, para atualizar os metadados no Gerenciador de metadados de banco de dados de SQL do Azure, você deve atualizar manualmente os metadados de BD SQL do Azure. Para obter mais informações, consulte a seção "Sincronização de metadados do Azure SQL DB" mais adiante neste tópico.  
  
## <a name="required-azure-sql-db-permissions"></a>Permissões de banco de dados SQL do Azure necessárias  
A conta que é usada para se conectar ao BD SQL do Azure requer permissões diferentes, dependendo das ações que executa a conta:  
  
1.  Para converter objetos do Sybase para [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts de sintaxe, para atualizar os metadados de BD SQL do Azure ou para salvar a sintaxe a ser convertido, a conta deve ter permissão para fazer logon na instância do SQL do Azure.  
  
2.  Para carregar objetos de banco de dados no BD SQL do Azure, o requisito mínimo de permissão é a associação à **db_owner** função de banco de dados no banco de dados de destino.  
  
## <a name="establishing-a-azure-sql-db-connection"></a>Estabelecer uma Conexão de banco de dados SQL do Azure  
Antes de converter objetos de banco de dados Sybase à sintaxe SQL do Azure, você deve estabelecer uma conexão à instância do banco de dados do SQL Azure em que você deseja migrar os bancos de dados ou banco de dados Sybase.  
  
Quando você define as propriedades de conexão, você também especificar o banco de dados onde objetos e dados serão migrados. Depois de conectar ao BD SQL do Azure, você pode personalizar esse mapeamento no nível de esquema do Sybase. Para obter mais informações, consulte [mapear esquemas ASE do Sybase para esquemas SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> Antes de tentar se conectar ao BD SQL do Azure, certifique-se de que a instância de BD SQL do Azure está em execução e pode aceitar conexões.  
  
**Para se conectar ao BD SQL do Azure**  
  
1.  Sobre o **arquivo** menu, selecione **conectar-se ao BD SQL do Azure**(essa opção é habilitada após a criação de um projeto).  
  
    Se você tiver se conectado anteriormente para BD SQL do Azure, o nome do comando será **reconectar-se ao BD SQL do Azure**  
  
2.  Na caixa de diálogo de conexão, insira ou selecione o nome do servidor de BD SQL do Azure.  
  
3.  Insira, selecione ou **procurar** o nome do banco de dados.  
  
4.  Insira ou selecione **nome de usuário**.  
  
5.  Insira o **senha**.  
  
6.  O SSMA recomenda conexão criptografada ao BD SQL do Azure.  
  
7.  Clique em **Conectar**.  
  
> [!IMPORTANT]  
> O SSMA para Sybase não oferece suporte a conexão ao **mestre** banco de dados no BD SQL do Azure.  
  
## <a name="synchronizing-azure-sql-db-metadata"></a>Sincronizar metadados de banco de dados SQL do Azure  
Metadados sobre bancos de dados SQL do Azure não é atualizado automaticamente. Os metadados no Gerenciador de metadados de banco de dados de SQL do Azure são um instantâneo dos metadados quando conectado pela primeira vez para BD SQL do Azure ou a última vez em que você atualizou manualmente os metadados. Você pode atualizar manualmente os metadados para todos os bancos de dados ou para qualquer banco de dados individual ou um objeto de banco de dados.  
  
**Para sincronizar os metadados**  
  
1.  Certifique-se de que você está conectado ao Azure SQL DB.  
  
2.  No Gerenciador de metadados do banco de dados do SQL Azure, selecione a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.  
  
    Por exemplo, para atualizar os metadados para todos os bancos de dados, marque a caixa ao lado de bancos de dados.  
  
3.  Bancos de dados, ou o banco de dados individual ou o esquema de banco de dados e, em seguida, selecione **sincronizar com o banco de dados**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento entre esquemas Sybase e bancos de dados SQL do Azure e esquemas, consulte [mapeamento de esquemas de ASE do Sybase para esquemas SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   Para personalizar opções de configuração para os projetos, consulte [definir opções do projeto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   Para personalizar o mapeamento de tipos de dados de origem e destino, consulte [mapeamento Sybase ASE e tipos de dados do SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   Se você não precisa executar qualquer uma dessas tarefas, você pode converter as definições de objeto de banco de dados do Sybase em definições de objeto de BD SQL do Azure. Para obter mais informações, consulte [converter objetos de banco de dados do Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Sybase ASE para o SQL Server – BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
