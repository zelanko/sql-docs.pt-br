---
title: Conectando-se ao banco de dados SQL do Azure (MySQLToSQL) | Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 8e288b91c92d8d086d5b066f95868fa0fa733bb9
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935926"
---
# <a name="connecting-to-azure-sql-database-mysqltosql"></a>Conectando-se ao banco de dados SQL do Azure (MySQLToSQL)
Para migrar bancos de dados MySQL para SQL Azure, você deve se conectar à instância de destino do SQL Azure. Quando você se conecta, o SSMA obtém metadados sobre todos os bancos de dados na instância do SQL Azure e exibe os metadados do banco de dados no SQL Azure Gerenciador de metadados. O SSMA armazena informações da instância do SQL Azure ao qual você está conectado, mas não armazena senhas.  
  
Sua conexão com SQL Azure permanece ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao SQL Azure se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até carregar os objetos de banco de dados em SQL Azure e migrar.  
  
Os metadados sobre a instância do SQL Azure não são sincronizados automaticamente. Em vez disso, para atualizar os metadados no SQL Azure Gerenciador de metadados, você deve atualizar manualmente os metadados de SQL Azure. Para obter mais informações, consulte a seção "sincronizando metadados de SQL Azure" mais adiante neste tópico.  
  
## <a name="required-sql-azure-permissions"></a>Permissões de SQL Azure necessárias  
A conta usada para se conectar ao SQL Azure requer permissões diferentes dependendo das ações que a conta executa:  
  
-   Para converter objetos MySQL em [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, para atualizar metadados de SQL Azure ou para salvar a sintaxe convertida em scripts, a conta deve ter permissão para fazer logon na instância do SQL Azure.  
  
-   Para carregar objetos de banco de dados em SQL Azure, o requisito mínimo de permissão é a associação na função de banco de dados **db_owner** no banco de dados de destino.  
  
## <a name="establishing-a-sql-azure-connection"></a>Estabelecendo uma conexão SQL Azure  
Antes de converter objetos de banco de dados MySQL para SQL Azure sintaxe, você deve estabelecer uma conexão com a instância do SQL Azure em que você deseja migrar o banco de dados MySQL ou bancos.  
  
Ao definir as propriedades de conexão, você também especifica o banco de dados em que os objetos e data serão migrados. Você pode personalizar esse mapeamento no nível de esquema do MySQL depois de se conectar ao SQL Azure. Para obter mais informações, consulte [mapeando bancos de dados MySQL para esquemas de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> Antes de tentar se conectar ao SQL Azure, verifique se a instância do SQL Azure está em execução e pode aceitar conexões.  
  
**Para se conectar ao SQL Azure**  
  
1.  No menu **arquivo** , selecione **conectar-se a SQL Azure** (essa opção é habilitada após a criação de um projeto).  
  
    Se você tiver se conectado anteriormente ao SQL Azure, o nome do comando será **reconectado ao SQL Azure**.  
  
2.  Na caixa de diálogo conexão, insira ou selecione o nome do servidor de SQL Azure.  
  
3.  Insira, selecione ou **procure** o nome do banco de dados.  
  
4.  Insira ou selecione o **nome de usuário**.  
  
5.  Insira a **senha**.  
  
6.  O SSMA recomenda a conexão criptografada com SQL Azure.  
  
7.  Clique em **Conectar**.  
  
> [!IMPORTANT]  
> O SSMA para MySQL não dá suporte à conexão com o banco de dados **mestre** no SQL Azure.  
  
## <a name="synchronizing-sql-azure-metadata"></a>Sincronizando metadados de SQL Azure  
Os metadados sobre os bancos de dados no Azure SQL Database não são atualizados automaticamente. Os metadados no SQL Azure Gerenciador de metadados é um instantâneo dos metadados quando você se conecta pela primeira vez ao SQL Azure, ou a última vez que você atualizou os metadados manualmente. Você pode atualizar os metadados manualmente para todos os bancos de dados ou para qualquer banco de dados ou objeto de banco de dados individual.  
  
**Para sincronizar metadados**  
  
1.  Verifique se você está conectado a SQL Azure.  
  
2.  No SQL Azure Gerenciador de metadados, marque a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.  
  
    Por exemplo, para atualizar os metadados de todos os bancos de dados, selecione a caixa ao lado de bancos de dados.  
  
3.  Clique com o botão direito do mouse em bancos de dados ou em um esquema ou banco de dados individual e selecione **sincronizar com Banco de dados**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa na migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento entre os esquemas do MySQL e o banco de dados SQL do Azure, consulte [mapeando bancos de dados MySQL para esquemas de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   Para personalizar as opções de configuração para os projetos, consulte [definir opções de projeto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeando MySQL e SQL Server tipos de dados &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Se você não precisar executar nenhuma dessas tarefas, poderá converter as definições do objeto de banco de dados MySQL em SQL Azure definições de objeto. Para obter mais informações, consulte [convertendo bancos de dados MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados MySQL para SQL Server-banco de MySQLToSql SQL do Azure &#40;&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
