---
title: Migrar dados ASE do Sybase para o SQL Server – BD SQL do Azure | Microsoft Docs
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e9751dcfe8ee708731dbad54860a978f0e498df7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47604764"
---
# <a name="migrating-sybase-ase-data-into-sql-server---azure-sql-db--sybasetosql"></a>Migrar dados ASE do Sybase para o SQL Server – BD SQL do Azure (SybaseToSQL)
Depois que você carregou com êxito os objetos de banco de dados do Sybase Adaptive Server Enterprise (ASE) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL do Azure, você pode migrar dados do ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure.  
  
> [!IMPORTANT]  
> Se o mecanismo que está sendo usado é o mecanismo de migração de dados do lado do servidor, em seguida, antes de migrar dados, você deve instalar o SSMA para Sybase ASE extensão Pack e os provedores de Sybase ASE no computador que está executando o SSMA. Também deve estar executando o serviço SQL Server Agent. Para obter mais informações sobre como instalar o pacote de extensão, consulte [instalando os componentes do SSMA no SQL Server (SybaseToSQL)](http://msdn.microsoft.com/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
## <a name="setting-migration-options"></a>Definindo opções de migração  
Antes de migrar dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL do Azure, examine as opções de migração de projeto na **configurações do projeto** caixa de diálogo.  
  
-   Usando essa caixa de diálogo, você pode definir opções de como o tamanho do lote de migração, bloqueio de tabela, verificação de restrição, manipulação de valor nulo e lidar com valor de identidade. Para obter mais informações sobre as configurações de projeto de migração, consulte [configurações do projeto (migração) (Sybasetosql)](http://msdn.microsoft.com/82f8857f-7ab1-4738-ab6e-b1e95ea94924).  
  
    Para obter mais informações sobre **configurações de migração de dados estendido**, consulte [configurações de migração de dados](data-migration-settings-sybasetosql.md)  
  
-   O **mecanismo de migração** na **configurações do projeto** caixa de diálogo permite que o usuário execute o processo de migração usando dois tipos de mecanismos de migração de dados, visualização.:  
  
    1.  Mecanismo de migração de dados do lado cliente  
  
    2.  Mecanismo de migração de dados do lado servidor  
  
**Migração de dados do lado do cliente:**  
  
-   Para iniciar a migração de dados no lado do cliente, selecione a opção **mecanismo de migração de dados do lado do cliente** na **configurações do projeto** caixa de diálogo.  
  
-   Na **configurações do projeto**, o **mecanismo de migração de dados do lado do cliente** opção é definida por padrão.  
  
    > [!NOTE]  
    > O mecanismo de migração de dados do lado do cliente reside dentro do aplicativo do SSMA e, portanto, não é dependente da disponibilidade do pacote de extensão.  
  
**Migração de dados do lado do servidor:**  
  
-   Durante a migração de dados do lado do servidor, o mecanismo no qual reside o banco de dados de destino. Ele é instalado pelo pacote de extensão. Para obter mais informações sobre como instalar o pacote de extensão, consulte [instalando os componentes do SSMA no SQL Server (SybaseToSQL)](http://msdn.microsoft.com/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
-   Para iniciar a migração no lado do servidor, selecione a **mecanismo de migração de dados do lado do servidor** opção a **configurações do projeto** caixa de diálogo.  
  
> [!NOTE]  
> Quando o BD SQL do Azure é usado como destino banco de dados, apenas **migração de dados do lado cliente** é permitida e não há suporte para a migração de dados do lado servidor.  
  
## <a name="migrating-data-to-sql-server-or-azure-sql-db"></a>Migrando dados para o SQL Server ou banco de dados SQL do Azure  
Migração de dados são uma operação de carregamento em massa que move linhas de dados das tabelas do ASE para tabelas do SQL Server em transações. O número de linhas carregado no SQL Server ou SQL do Azure em cada transação é configurado nas configurações do projeto.  
  
Para exibir as mensagens de migração, certifique-se de que o painel de saída está visível. Caso contrário, selecione **saída** da **exibição** menu.  
  
**Para migrar dados**  
  
1.  Verifique o seguinte:  
  
    -   Os provedores de ASE são instalados no computador que está executando o SSMA.  
  
    -   Você sincronizou os objetos convertidos com o banco de dados de destino (SQL Server ou SQL do Azure).  
  
2.  No Gerenciador de metadados do Sybase, selecione os objetos que contêm os dados que você deseja migrar:  
  
    -   Para migrar dados para todos os esquemas, marque a caixa de seleção ao lado **esquemas**.  
  
    -   Para migrar os dados ou omitir tabelas individuais, primeiro expanda o esquema, expanda **tabelas**e, em seguida, selecione ou desmarque a caixa de seleção ao lado da tabela.  
  
3.  Para migrar dados, podem surgir dois casos:  
  
    **Migração de dados do lado do cliente:**  
  
    Para realizar **migração de dados do lado do cliente**, selecione o **mecanismo de migração de dados do lado do cliente** opção o **configurações de projeto** caixa de diálogo.  
  
    **Migração de dados do lado do servidor:**  
  
    -   Antes de executar a migração de dados do servidor, verifique se:  
  
        1.  O SSMA para Sybase extensão Pack está instalado na instância do SQL Server.  
  
        2.  O serviço SQL Server Agent está em execução na instância do SQL Server  
  
    -   Para realizar **migração de dados do lado do servidor**, selecione o **mecanismo de migração de dados do lado do servidor** opção o **configurações de projeto** caixa de diálogo.  
  
4.  Clique com botão direito **esquemas** no Gerenciador de metadados do Sybase e clique **migrar dados**. Também é possível migrar dados para objetos individuais ou categorias de objetos: o objeto ou a pasta pai e selecione o **migrar dados** opção.  
  
    > [!NOTE]  
    > Se o SSMA para Sybase pacote de extensão não está instalado na instância do SQL Server e se **mecanismo de migração de dados do lado do servidor** estiver selecionada, ao migrar os dados para o banco de dados de destino, o seguinte erro é encontrado: ' SSMA Componentes de migração de dados não foram encontrados no SQL Server, não será possível realizar a migração de dados do lado do servidor. Verifique se o pacote de extensão está instalado corretamente '. Clique em **Cancelar** para finalizar a migração de dados.  
  
5.  No **conectar-se ao Sybase ASE** caixa de diálogo, insira as credenciais de conexão e, em seguida, clique em **Connect**. Para obter mais informações sobre como se conectar ao Sybase ASE, consulte [conectar-se ao Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)  
  
    Se o banco de dados de destino for SQL Server, em seguida, insira as credenciais de conexão na **conectar-se ao SQL Server** caixa de diálogo e clique em **Connect**. Para obter mais informações sobre como se conectar ao SQL Server, consulte [conectar-se ao SQL Server(SybaseToSQL)](http://msdn.microsoft.com/dd368a1a-45b0-40e9-b4d3-5cdb48c26606)  
  
    Se o banco de dados de destino for o BD SQL do Azure, em seguida, insira as credenciais de conexão na **conectar-se ao BD SQL do Azure** caixa de diálogo e clique em **Connect**. Para obter mais informações sobre como se conectar ao BD SQL do Azure, consulte [conectar-se ao BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
    Mensagens serão exibidas as **saída** painel. Quando a migração for concluída, o **relatório de migração de dados** é exibida. Se todos os dados não migrou, clique na linha que contém os erros e, em seguida, clique em **detalhes**. Quando tiver terminado com o relatório, clique em **fechar**. Para obter mais informações sobre o relatório de migração de dados, consulte [relatório de migração de dados (SSMA comum)](http://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Quando o SQL Express edition é usado como o banco de dados de destino, somente cliente lado migração de dados é permitida e não há suporte para a migração de dados do lado servidor.  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Sybase ASE para o SQL Server – BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
