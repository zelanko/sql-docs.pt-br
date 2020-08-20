---
description: Migrando dados de ASE do Sybase para o SQL Server – banco de SybaseToSQL SQL
title: Migrar dados de ASE do Sybase para o SQL Server-banco de dado SQL do Azure | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migrating data,Client Side Data Migration
- Migrating data,Server Side Data Migration
ms.assetid: 54a39f5e-9250-4387-a3ae-eae47c799811
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 89603e61a51ebac9ccf8d834e493bbd463645a02
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497660"
---
# <a name="migrating-sybase-ase-data-into-sql-server---azure-sql-database--sybasetosql"></a>Migrando dados de ASE do Sybase para o SQL Server – banco de SybaseToSQL SQL
Depois de ter carregado com êxito os objetos de banco de dados do Sybase Adaptive Server Enterprise (ASE) no ou no banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL do Azure, você pode migrar os dados do ase para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do banco de dado SQL do Azure.  
  
> [!IMPORTANT]  
> Se o mecanismo que está sendo usado for o mecanismo de migração de dados do servidor, antes de migrar os dados, você deverá instalar o pacote de extensões do SSMA para Sybase ASE e os provedores de ASE do Sybase no computador que está executando o SSMA. O serviço de SQL Server Agent também deve estar em execução. Para obter mais informações sobre como instalar o pacote de extensões, consulte [instalando os componentes do SSMA no SQL Server (SybaseToSQL)](https://msdn.microsoft.com/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
## <a name="setting-migration-options"></a>Definindo opções de migração  
Antes de migrar dados para o ou para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL Database, examine as opções de migração de projeto na caixa de diálogo **configurações do projeto** .  
  
-   Usando essa caixa de diálogo, você pode definir opções como tamanho do lote de migração, bloqueio de tabela, verificação de restrição, tratamento de valor nulo e tratamento de valor de identidade. Para obter mais informações sobre as configurações de migração do projeto, consulte [configurações do projeto (migração) (Sybase)](https://msdn.microsoft.com/82f8857f-7ab1-4738-ab6e-b1e95ea94924).  
  
    Para obter mais informações sobre **as configurações de migração de dados estendidas**, consulte [configurações de migração de dados](data-migration-settings-sybasetosql.md)  
  
-   O **mecanismo de migração** na caixa de diálogo **configurações do projeto** permite que o usuário execute o processo de migração usando dois tipos de mecanismos de migração de dados, aula sobre visualização.:  
  
    1.  Mecanismo de migração de dados do lado do cliente  
  
    2.  Mecanismo de migração de dados do servidor  
  
**Migração de dados no lado do cliente:**  
  
-   Para iniciar a migração de dados no lado do cliente, selecione a opção **mecanismo de migração de dados do cliente** na caixa de diálogo Configurações do **projeto** .  
  
-   Em **configurações do projeto**, a opção **mecanismo de migração de dados do lado do cliente** é definida por padrão.  
  
    > [!NOTE]  
    > O mecanismo de migração de dados do lado do cliente reside dentro do aplicativo do SSMA e, portanto, não depende da disponibilidade do pacote de extensão.  
  
**Migração de dados no lado do servidor:**  
  
-   Durante a migração de dados no lado do servidor, o mecanismo reside no banco de dados de destino. Ele é instalado por meio do pacote de extensão. Para obter mais informações sobre como instalar o pacote de extensões, consulte [instalando os componentes do SSMA no SQL Server (SybaseToSQL)](https://msdn.microsoft.com/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
-   Para iniciar a migração no lado do servidor, selecione a opção **mecanismo de migração de dados do servidor** na caixa de diálogo Configurações do **projeto** .  
  
> [!NOTE]  
> Quando o banco de dados SQL do Azure é usado como o banco de dado de destino, somente a **migração de clientes no lado do cliente** é permitida e a migração de dados do lado do servidor não é  
  
## <a name="migrating-data-to-sql-server-or-azure-sql-database"></a>Migrando dados para o SQL Server ou para o Azure SQL Database  
A migração de dados é uma operação de carregamento em massa que move linhas de dados das tabelas do ASE para SQL Server tabelas em transações. O número de linhas carregadas no SQL Server ou no banco de dados SQL do Azure em cada transação é definido nas configurações do projeto.  
  
Para exibir as mensagens de migração, verifique se o painel de saída está visível. Caso contrário, selecione **saída** no menu **Exibir** .  
  
**Para migrar dados**  
  
1.  Verifique o seguinte:  
  
    -   Os provedores do ASE são instalados no computador que está executando o SSMA.  
  
    -   Você sincronizou os objetos convertidos com o banco de dados de destino (SQL Server ou banco de dados SQL do Azure).  
  
2.  No Gerenciador de metadados do Sybase, selecione os objetos que contêm os dados que você deseja migrar:  
  
    -   Para migrar dados para todos os esquemas, marque a caixa de seleção ao lado de **esquemas**.  
  
    -   Para migrar dados ou omitir tabelas individuais, primeiro expanda o esquema, expanda **tabelas**e marque ou desmarque a caixa de seleção ao lado da tabela.  
  
3.  Para migrar dados, surgem dois casos:  
  
    **Migração de dados no lado do cliente:**  
  
    Para executar a **migração de dados no lado do cliente**, selecione a opção mecanismo de migração de dados do **cliente** na caixa de diálogo Configurações do **projeto** .  
  
    **Migração de dados no lado do servidor:**  
  
    -   Antes de executar a migração de dados do servidor, verifique se:  
  
        1.  O pacote de extensão do SSMA para Sybase é instalado na instância do SQL Server.  
  
        2.  O serviço de SQL Server Agent está em execução na instância do SQL Server  
  
    -   Para executar a **migração de dados no servidor**, selecione a opção mecanismo de migração de dados do **servidor** na caixa de diálogo Configurações do **projeto** .  
  
4.  Clique com o botão direito do mouse em **esquemas** no Gerenciador de metadados Sybase e clique em **migrar dados**. Você também pode migrar dados para objetos individuais ou categorias de objetos: clique com o botão direito do mouse no objeto ou em sua pasta pai e selecione a opção **migrar dados** .  
  
    > [!NOTE]  
    > Se o pacote de extensão do SSMA para Sybase não estiver instalado na instância do SQL Server, e se o **mecanismo de migração de dados do servidor** for selecionado, ao migrar os dados para o banco de dado de destino, o seguinte erro será encontrado: ' componentes de migração de dados do SSMA não foram encontrados no SQL Server, a migração de dados no servidor não será possível. Verifique se o pacote de extensões está instalado corretamente '. Clique em **Cancelar** para encerrar a migração de dados.  
  
5.  Na caixa de diálogo **conectar-se ao Sybase ase** , insira as credenciais de conexão e clique em **conectar**. Para obter mais informações sobre como se conectar ao Sybase ASE, consulte [conectar-se ao sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)  
  
    Se o banco de dados de destino for SQL Server, insira as credenciais de conexão na caixa de diálogo **conectar a SQL Server** e clique em **conectar**. Para obter mais informações sobre como se conectar ao SQL Server, consulte [conectando-se ao SQL Server (SybaseToSQL)](https://msdn.microsoft.com/dd368a1a-45b0-40e9-b4d3-5cdb48c26606)  
  
    Se o banco de dados de destino for um banco de dados SQL do Azure, insira as credenciais de conexão na caixa de diálogo **conectar ao banco de dados SQL do Azure** e clique em **conectar**. Para obter mais informações sobre como se conectar ao banco de dados SQL do Azure, consulte [conectando ao banco de dados SQL do azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
    As mensagens serão exibidas no painel de **saída** . Quando a migração for concluída, o **relatório de migração de dados** será exibido. Se algum dado não for migrado, clique na linha que contém os erros e, em seguida, clique em **detalhes**. Ao concluir o relatório, clique em **fechar**. Para obter mais informações sobre o relatório de migração de dados, consulte [relatório de migração de dados (SSMA Common)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Quando o SQL Express Edition é usado como o banco de dados de destino, somente a migração de dado do lado do cliente é permitida e não há suporte para a migração de dados do lado do servidor.  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Sybase ASE para o SQL Server-banco de SybaseToSQL SQL do Azure &#40;o&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
