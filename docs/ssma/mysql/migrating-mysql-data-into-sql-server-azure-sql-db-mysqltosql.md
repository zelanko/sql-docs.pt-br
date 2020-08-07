---
title: Migrando dados do MySQL para o SQL Server – banco de MySQLToSQL (Azure SQL Database) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Data Migration, server side data migration
- Data Migration,client side data migration
ms.assetid: a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 9679651e80e036fce923daac76130be01cb5a07a
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87862671"
---
# <a name="migrating-mysql-data-into-sql-server---azure-sql-database-mysqltosql"></a>Migrando dados do MySQL para o SQL Server – banco de MySQLToSQL (Azure SQL Database)
Depois de sincronizar com êxito os objetos convertidos com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, você pode migrar dados de MySQL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
> [!IMPORTANT]  
> Se o mecanismo que está sendo usado for o mecanismo de migração de dados do servidor, antes de migrar os dados, você deverá instalar o pacote de extensão do SSMA para MySQL e os provedores do MySQL no computador que está executando o SSMA. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço do Agent também deve estar em execução. Para obter mais informações sobre como instalar o pacote de extensões, consulte [instalando componentes do SSMA em SQL Server (MySQL para SQL)](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
## <a name="setting-migration-options"></a>Definindo opções de migração  
Antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o ou SQL Azure, examine as opções de migração do projeto na caixa de diálogo **configurações do projeto** .  
  
-   Usando essa caixa de diálogo, você pode definir opções como tamanho do lote de migração, bloqueio de tabela, verificação de restrição, tratamento de valor nulo e tratamento de valor de identidade. Para obter mais informações sobre as configurações de migração do projeto, consulte [configurações do projeto (migração)](https://msdn.microsoft.com/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9).  
  
    Para obter mais informações sobre **as configurações de migração de dados estendidas**, consulte [configurações de migração de dados](data-migration-settings-mysqltosql.md)  
  
-   O **mecanismo de migração** na caixa de diálogo **configurações do projeto** permite que o usuário execute o processo de migração usando dois tipos de mecanismos de migração de dados:  
  
    1.  Mecanismo de migração de dados do lado do cliente  
  
    2.  Mecanismo de migração de dados do servidor  
  
**Migração de dados no lado do cliente:**  
  
-   Para iniciar a migração de dados no lado do cliente, selecione a opção **mecanismo de migração de dados do cliente** na caixa de diálogo Configurações do **projeto** .  
  
-   Em **configurações do projeto**, a opção **mecanismo de migração de dados do lado do cliente** é definida.  
  
    > [!NOTE]  
    > O **mecanismo de migração de dados do lado do cliente** reside dentro do aplicativo SSMA e, portanto, não depende da disponibilidade do pacote de extensão.  
  
**Migração de dados no lado do servidor:**  
  
-   Durante a migração de dados do lado do servidor, o mecanismo reside no banco de dados de destino. Ele é instalado por meio do pacote de extensão. Para obter mais informações sobre como instalar o pacote de extensões, consulte [instalando componentes do SSMA em SQL Server (MySQL para SQL)](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
-   Para iniciar a migração no lado do servidor, selecione a opção **mecanismo de migração de dados do servidor** na caixa de diálogo Configurações do **projeto** .  
  
> [!IMPORTANT]  
> A opção de **migração de dados do lado do cliente** está disponível somente para SQL Azure.  
  
## <a name="migrating-data-to-sql-server-or-sql-azure"></a>Migrando dados para SQL Server ou SQL Azure  
A migração de dados é uma operação de carregamento em massa que move linhas de dados de tabelas do MySQL para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure tabelas em transações. O número de linhas carregadas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em cada transação é configurado nas configurações do projeto.  
  
Para exibir as mensagens de migração, verifique se o painel de saída está visível. Caso contrário, no menu **Exibir** , selecione **saída**.  
  
**Para migrar dados**  
  
1.  Verifique o seguinte:  
  
    -   Os provedores do MySQL são instalados no computador que está executando o SSMA.  
  
    -   Você sincronizou os objetos convertidos com o banco de dados de destino (SQL Server/SQL Azure).  
  
2.  No Gerenciador de metadados do MySQL, selecione os objetos que contêm os dados que você deseja migrar:  
  
    -   Para migrar dados para todos os esquemas, marque a caixa de seleção ao lado de **esquemas**.  
  
    -   Para migrar dados ou omitir tabelas individuais, primeiro expanda o esquema, expanda **tabelas**e marque ou desmarque a caixa de seleção ao lado da tabela.  
  
3.  Para migrar dados, surgem dois casos:  
  
    **Migração de dados no lado do cliente:**  
  
    -   Para executar a **migração de dados no lado do cliente**, selecione a opção mecanismo de migração de dados do **cliente** na caixa de diálogo Configurações do **projeto** .  
  
    **Migração de dados no lado do servidor:**  
  
    -   Antes de executar a migração de dados no lado do servidor, verifique se:  
  
        1.  O pacote de extensão do SSMA para MySQL é instalado na instância do SQL Server.  
  
        2.  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço Agent está em execução na instância do SQL Server  
  
    -   Para executar a **migração de dados no servidor**, selecione a opção mecanismo de migração de dados do **servidor** na caixa de diálogo Configurações do **projeto** .  
  
4.  Clique com o botão direito do mouse em **esquemas** no Gerenciador de metadados do MySQL e clique em **migrar dados**. Você também pode migrar dados para objetos individuais ou categorias de objetos: clique com o botão direito do mouse no objeto ou em sua pasta pai; Selecione a opção **migrar dados** .  
  
    > [!NOTE]  
    > Se o pacote de extensão do SSMA para MySQL não estiver instalado na instância do SQL Server, e se o **mecanismo de migração de dados do servidor** for selecionado, ao migrar os dados para o banco de dado de destino, o seguinte erro será encontrado: ' componentes de migração de dados do SSMA não foram encontrados no SQL Server, a migração de dados no servidor não será possível. Verifique se o pacote de extensões está instalado corretamente '. Clique em **Cancelar** para encerrar a migração de dados.  
  
5.  Na caixa de diálogo **conectar-se ao MySQL** , insira as credenciais de conexão e clique em **conectar**. Para obter mais informações sobre como se conectar ao MySQL, consulte [conectar-se ao mysql &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
    Se o banco de dados de destino for SQL Server, insira as credenciais de conexão na caixa de diálogo **conectar a SQL Server** e clique em **conectar**. Para obter mais informações sobre como se conectar ao SQL Server, consulte [conectar-se ao SQL Server](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    Se o banco de dados de destino for SQL Azure, insira as credenciais de conexão na caixa de diálogo **conectar a SQL Azure** e clique em **conectar**. Para obter mais informações sobre como se conectar a SQL Azure, consulte [conectar-se ao banco de dados SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-azure-sql-db-mysqltosql.md)  
  
    As mensagens serão exibidas no painel de **saída** . Quando a migração for concluída, o **relatório de migração de dados** será exibido. Se algum dado não for migrado, clique na linha que contém os erros e, em seguida, clique em **detalhes**. Ao concluir o relatório, clique em **fechar**. Para obter mais informações sobre o relatório de migração de dados, consulte [relatório de migração de dados (SSMA Common)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Quando o SQL Express Edition é usado como o banco de dados de destino, somente a migração de dado do lado do cliente é permitida e não há suporte para a migração de dados do lado do servidor.  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados MySQL para SQL Server-banco de MySQLToSql SQL do Azure &#40;&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
