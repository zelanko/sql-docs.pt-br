---
title: Migrar dados do Sybase ASE para o SQL Server - banco de dados SQL do Azure | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Migrating data,Client Side Data Migration
- Migrating data,Server Side Data Migration
ms.assetid: 54a39f5e-9250-4387-a3ae-eae47c799811
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3491ebb2eab0933aad75dd234e3f1d6909e5571f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="migrating-sybase-ase-data-into-sql-server---azure-sql-db--sybasetosql"></a>Migração de dados Sybase ASE para o SQL Server - banco de dados do SQL Azure (SybaseToSQL)
Depois que você carregou com êxito os objetos de banco de dados do Sybase Adaptive Server Enterprise (ASE) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure, você pode migrar dados de ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure.  
  
> [!IMPORTANT]  
> Se o mecanismo que está sendo usado é o mecanismo de migração de dados do lado do servidor, em seguida, antes de migrar dados, você deve instalar o SSMA para Sybase ASE extensão do pacote e os provedores de Sybase ASE no computador que está executando o SSMA. Também deve estar executando o serviço SQL Server Agent. Para obter mais informações sobre como instalar o pacote de extensão, consulte [instalar componentes do SSMA no SQL Server (SybaseToSQL)](http://msdn.microsoft.com/en-us/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
## <a name="setting-migration-options"></a>Definindo opções de migração  
Antes de migrar dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou DB do SQL Azure, examine as opções de migração de projeto no **configurações de projeto** caixa de diálogo.  
  
-   Usando essa caixa de diálogo, você pode definir opções, como tamanho de lote de migração, o bloqueio da tabela, verificação de restrição, manipulação de valor nulo e lidar com valor de identidade. Para obter mais informações sobre as configurações de projeto de migração, consulte [configurações do projeto (migração) (Sybase)](http://msdn.microsoft.com/en-us/82f8857f-7ab1-4738-ab6e-b1e95ea94924).  
  
    Para obter mais informações sobre **configurações de migração de dados estendido**, consulte [configurações de migração de dados](http://msdn.microsoft.com/en-us/94d7a083-2dbc-4e3d-94dd-92b7ff9d0c2d)  
  
-   O **mecanismo de migração** no **configurações de projeto** caixa de diálogo permite que o usuário execute o processo de migração usando dois tipos de mecanismos de migração de dados, viz.:  
  
    1.  Mecanismo de migração de dados do lado cliente  
  
    2.  Mecanismo de migração de dados do lado servidor  
  
**Migração de dados do lado do cliente:**  
  
-   Para iniciar a migração de dados no lado do cliente, selecione a opção **mecanismo de migração de dados do lado do cliente** no **configurações de projeto** caixa de diálogo.  
  
-   Em **configurações de projeto**, o **mecanismo de migração de dados do lado do cliente** opção é definida por padrão.  
  
    > [!NOTE]  
    > O mecanismo de migração de dados do lado do cliente residir dentro do aplicativo do SSMA e, portanto, não é dependente da disponibilidade do pacote de extensão.  
  
**Migração de dados do lado do servidor:**  
  
-   Durante a migração de dados do lado do servidor, o mecanismo reside no banco de dados de destino. Ele é instalado por meio do pacote de extensão. Para obter mais informações sobre como instalar o pacote de extensão, consulte [instalar componentes do SSMA no SQL Server (SybaseToSQL)](http://msdn.microsoft.com/en-us/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
-   Para iniciar a migração no lado do servidor, selecione o **mecanismo de migração de dados do lado do servidor** opção o **configurações de projeto** caixa de diálogo.  
  
> [!NOTE]  
> Quando o banco de dados do Azure SQL é usado como dados de destino, apenas **migração de dados do lado cliente** é permitida e não há suporte para a migração de dados do lado de servidor.  
  
## <a name="migrating-data-to-sql-server-or-azure-sql-db"></a>Migrando dados para o SQL Server ou banco de dados SQL do Azure  
Migração de dados são uma operação de carregamento em massa que move linhas de dados das tabelas ASE em tabelas do SQL Server em transações. O número de linhas carregado no SQL Server ou banco de dados do Azure SQL em cada transação é configurado nas configurações do projeto.  
  
Para exibir as mensagens de migração, certifique-se de que o painel de saída está visível. Caso contrário, selecione **saída** do **exibição** menu.  
  
**Para migrar dados**  
  
1.  Verifique o seguinte:  
  
    -   Os provedores de ASE estão instalados no computador que está executando o SSMA.  
  
    -   Você sincronizou objetos convertidos no banco de dados de destino (SQL Server ou banco de dados de SQL Azure).  
  
2.  No Gerenciador de metadados do Sybase, selecione os objetos que contêm os dados que você deseja migrar:  
  
    -   Para migrar dados para todos os esquemas, selecione a caixa de seleção ao lado de **esquemas**.  
  
    -   Para migrar dados ou omitir tabelas individuais, primeiro expanda o esquema, **tabelas**e, em seguida, marque ou desmarque a caixa de seleção ao lado da tabela.  
  
3.  Para migrar dados, podem surgir dois casos:  
  
    **Migração de dados do lado do cliente:**  
  
    Para executar **a migração de dados do lado do cliente**, selecione o **mecanismo de migração de dados do lado do cliente** opção o **configurações de projeto** caixa de diálogo.  
  
    **Migração de dados do lado do servidor:**  
  
    -   Antes de executar a migração de dados do lado de servidor, certifique-se:  
  
        1.  O SSMA para Sybase extensão Pack está instalado na instância do SQL Server.  
  
        2.  O serviço SQL Server Agent está em execução na instância do SQL Server  
  
    -   Para executar **migração de dados do lado do servidor**, selecione o **mecanismo de migração de dados do lado do servidor** opção o **configurações de projeto** caixa de diálogo.  
  
4.  Clique com botão direito **esquemas** no Gerenciador de metadados do Sybase e clique **migrar dados**. Também é possível migrar dados para objetos individuais ou as categorias de objetos: o objeto ou a pasta pai e selecione o **migrar dados** opção.  
  
    > [!NOTE]  
    > Se o SSMA para Sybase pacote de extensão não está instalado na instância do SQL Server e se **mecanismo de migração de dados do lado do servidor** for selecionado, em seguida, ao migrar os dados para o banco de dados de destino, o seguinte erro: ' componentes de migração de dados do SSMA não foram encontrados no SQL Server, não será possível realizar a migração de dados do servidor. Verifique se o pacote de extensão está instalado corretamente '. Clique em **Cancelar** para finalizar a migração de dados.  
  
5.  No **conectar para Sybase ASE** caixa de diálogo, insira as credenciais de conexão e, em seguida, clique em **conectar**. Para obter mais informações sobre como se conectar para Sybase ASE, consulte [conectar-se ao Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)  
  
    Se o banco de dados de destino for SQL Server, em seguida, insira as credenciais de conexão no **conectar ao SQL Server** caixa de diálogo e clique em **conectar**. Para obter mais informações sobre como se conectar ao SQL Server, consulte [se conectar ao SQL Server(SybaseToSQL)](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606)  
  
    Se o banco de dados de destino é o banco de dados do Azure SQL, em seguida, insira as credenciais de conexão no **conectar-se ao banco de dados do Azure SQL** caixa de diálogo e clique em **conectar**. Para obter mais informações sobre como se conectar ao banco de dados de SQL do Azure, consulte [se conectar ao banco de dados do Azure SQL &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
    As mensagens serão exibidas no **saída** painel. Quando a migração for concluída, o **relatório de migração de dados** é exibida. Se todos os dados não migrar, clique na linha que contém os erros e, em seguida, clique em **detalhes**. Quando tiver terminado com o relatório, clique em **fechar**. Para obter mais informações sobre o relatório de migração de dados, consulte [o relatório de dados de migração (SSMA comuns)](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Quando o SQL Express edition é usado como o banco de dados de destino, é permitida somente cliente lado migração de dados e não há suporte para a migração de dados do lado de servidor.  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados Sybase ASE para o SQL Server - banco de dados SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
