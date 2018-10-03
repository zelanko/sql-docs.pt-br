---
title: Conectar-se ao banco de dados SQL do Azure (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Azure, SQL Azure permissions
- Connecting to SQL Azure, synchronization
ms.assetid: d0b6f16a-1880-459d-a0c7-28b7ef15c56a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 23d018a8d551a5c3a7f2978339b6cf7612f378fd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47741864"
---
# <a name="connecting-to-azure-sql-db-mysqltosql"></a>Conectar-se ao BD SQL do Azure (MySQLToSQL)
Para migrar bancos de dados MySQL para o SQL Azure, você deve se conectar à instância de destino do SQL Azure. Quando você se conectar, o SSMA obtém metadados sobre todos os bancos de dados na instância do SQL Azure e exibe os metadados de banco de dados no Gerenciador de metadados do SQL Azure. O SSMA armazena as informações da instância do SQL Azure, você está conectado ao, mas não armazena as senhas.  
  
Sua conexão ao SQL Azure permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve se reconectar ao SQL Azure se você quiser que uma conexão ativa com o servidor. Você pode trabalhar offline até que você carregar objetos de banco de dados no SQL Azure e migra dados.  
  
Metadados sobre a instância do SQL Azure não será sincronizado automaticamente. Em vez disso, para atualizar os metadados no Gerenciador de metadados do SQL Azure, você deve atualizar manualmente os metadados do SQL Azure. Para obter mais informações, consulte a seção "Sincronizar metadados de SQL Azure" mais adiante neste tópico.  
  
## <a name="required-sql-azure-permissions"></a>Exigido do SQL Azure permissões  
A conta que é usada para se conectar ao SQL Azure exige permissões diferentes, dependendo das ações que executa a conta:  
  
-   Para converter objetos do MySQL para [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts de sintaxe, para atualizar os metadados do SQL Azure ou para salvar a sintaxe a ser convertido, a conta deve ter permissão para fazer logon na instância do SQL Azure.  
  
-   Para carregar objetos de banco de dados no SQL Azure, o requisito mínimo de permissão é a associação à **db_owner** função de banco de dados no banco de dados de destino.  
  
## <a name="establishing-a-sql-azure-connection"></a>Estabelecendo um SQL Azure Conexão  
Antes de converter objetos de banco de dados MySQL à sintaxe do SQL Azure, você deve estabelecer uma conexão à instância do SQL Azure em que você deseja migrar o banco de dados MySQL ou bancos de dados.  
  
Quando você define as propriedades de conexão, você também especificar o banco de dados onde objetos e dados serão migrados. Depois de conectar ao SQL Azure, você pode personalizar esse mapeamento no nível de esquema do MySQL. Para obter mais informações, consulte [mapeamento de bancos de dados MySQL para esquemas SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> Antes de tentar se conectar ao SQL Azure, certifique-se de que a instância do SQL Azure está em execução e pode aceitar conexões.  
  
**Para se conectar ao SQL Azure**  
  
1.  Sobre o **arquivo** menu, selecione **conectar-se ao SQL Azure** (essa opção é habilitada após a criação de um projeto).  
  
    Se você tiver se conectado anteriormente ao SQL Azure, o nome do comando será **reconectar-se ao SQL Azure**.  
  
2.  Na caixa de diálogo de conexão, insira ou selecione o nome do servidor do SQL Azure.  
  
3.  Insira, selecione ou **procurar** o nome do banco de dados.  
  
4.  Insira ou selecione **nome de usuário**.  
  
5.  Insira o **senha**.  
  
6.  O SSMA recomenda conexão criptografada para o SQL Azure.  
  
7.  Clique em **Conectar**.  
  
> [!IMPORTANT]  
> SSMA para MySQL não oferece suporte a conexão ao **mestre** banco de dados no SQL Azure.  
  
## <a name="synchronizing-sql-azure-metadata"></a>Sincronizando o SQL Azure metadados  
Metadados sobre bancos de dados do SQL Azure não é atualizado automaticamente. Os metadados no Gerenciador de metadados do SQL Azure são um instantâneo dos metadados quando você primeiro conectado ao SQL Azure ou a última vez que você manualmente atualizado metadados. Você pode atualizar manualmente os metadados para todos os bancos de dados ou para qualquer banco de dados individual ou um objeto de banco de dados.  
  
**Para sincronizar os metadados**  
  
1.  Certifique-se de que você está conectado ao SQL Azure.  
  
2.  No Gerenciador de metadados do SQL Azure, selecione a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.  
  
    Por exemplo, para atualizar os metadados para todos os bancos de dados, marque a caixa ao lado de bancos de dados.  
  
3.  Bancos de dados, ou o banco de dados individual ou o esquema de banco de dados e, em seguida, selecione **sincronizar com o banco de dados**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento entre esquemas de MySQL e bancos de dados do SQL Azure e esquemas, consulte [mapeamento de bancos de dados MySQL para esquemas SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   Para personalizar opções de configuração para os projetos, consulte [definir opções do projeto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   Para personalizar o mapeamento de tipos de dados de origem e destino, consulte [MySQL de mapeamento e tipos de dados do SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Se você não precisa executar qualquer uma dessas tarefas, você pode converter as definições de objeto de banco de dados MySQL em definições de objeto do SQL Azure. Para obter mais informações, consulte [conversão de bancos de dados MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando MySQL bancos de dados para o SQL Server – BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
