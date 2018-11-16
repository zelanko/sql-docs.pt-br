---
title: Migrar dados do MySQL para o SQL Server – BD SQL do Azure (MySQLToSQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: a366f9ff19099ba640a02aecfe00a944e0fa6299
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51681264"
---
# <a name="migrating-mysql-data-into-sql-server---azure-sql-db-mysqltosql"></a>Migrar dados do MySQL para o SQL Server – BD SQL do Azure (MySQLToSQL)
Depois de ter sincronizado com êxito com objetos convertidos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure, você pode migrar os dados do MySQL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
> [!IMPORTANT]  
> Se o mecanismo que está sendo usado é o mecanismo para migração de dados do lado do servidor, em seguida, antes de migrar dados, você deve instalar o SSMA para MySQL pacote de extensão e os provedores de MySQL no computador que está executando o SSMA. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também deve estar executando o serviço de agente. Para obter mais informações sobre como instalar o pacote de extensão, consulte [instalando os componentes do SSMA no SQL Server (MySQL para o SQL)](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
## <a name="setting-migration-options"></a>Definindo opções de migração  
Antes de migrar dados a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure, examine as opções de migração de projeto na **configurações do projeto** caixa de diálogo.  
  
-   Usando essa caixa de diálogo, você pode definir opções de como o tamanho do lote de migração, bloqueio de tabela, verificação de restrição, manipulação de valor nulo e manipulação de valor de identidade. Para obter mais informações sobre as configurações de projeto de migração, consulte [configurações do projeto (migração)](https://msdn.microsoft.com/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9).  
  
    Para obter mais informações sobre **configurações de migração de dados estendido**, consulte [configurações de migração de dados](data-migration-settings-mysqltosql.md)  
  
-   O **mecanismo de migração** na **configurações do projeto** caixa de diálogo permite que o usuário execute o processo de migração usando dois tipos de mecanismos de migração de dados:  
  
    1.  Mecanismo de migração de dados do lado cliente  
  
    2.  Mecanismo de migração de dados do lado servidor  
  
**Migração de dados do lado do cliente:**  
  
-   Para iniciar a migração de dados no lado do cliente, selecione a **mecanismo de migração de dados do lado do cliente** opção a **configurações do projeto** caixa de diálogo.  
  
-   Na **configurações do projeto**, o **mecanismo de migração de dados do lado do cliente** opção está definida.  
  
    > [!NOTE]  
    > O **mecanismo de migração de dados do lado do cliente** reside dentro do aplicativo do SSMA e, portanto, não depende da disponibilidade do pacote de extensão.  
  
**Migração de dados do lado do servidor:**  
  
-   Durante a migração de dados do lado do servidor, o mecanismo no qual reside o banco de dados de destino. Ele é instalado pelo pacote de extensão. Para obter mais informações sobre como instalar o pacote de extensão, consulte [instalando os componentes do SSMA no SQL Server (MySQL para o SQL)](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
-   Para iniciar a migração no lado do servidor, selecione a **mecanismo de migração de dados do lado do servidor** opção a **configurações do projeto** caixa de diálogo.  
  
> [!IMPORTANT]  
> **Migração de dados do lado do cliente** opção só está disponível para o SQL Azure.  
  
## <a name="migrating-data-to-sql-server-or-sql-azure"></a>Migrando dados para o SQL Server ou SQL Azure  
Migração de dados são uma operação de carregamento em massa que move as linhas de dados de tabelas do MySQL em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou tabelas do SQL Azure em transações. O número de linhas carregado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em cada transação é configurado nas configurações do projeto.  
  
Para exibir mensagens de migração, certifique-se de que o painel de saída está visível. Caso contrário, do **modo de exibição** menu, selecione **saída**.  
  
**Para migrar dados**  
  
1.  Verifique o seguinte:  
  
    -   Os provedores de MySQL são instalados no computador que está executando o SSMA.  
  
    -   Você sincronizou os objetos convertidos com o banco de dados de destino (SQL Server / SQL Azure).  
  
2.  No Gerenciador de metadados do MySQL, selecione os objetos que contêm os dados que você deseja migrar:  
  
    -   Para migrar dados para todos os esquemas, marque a caixa de seleção ao lado **esquemas**.  
  
    -   Para migrar os dados ou omitir tabelas individuais, primeiro expanda o esquema, expanda **tabelas**e, em seguida, selecione ou desmarque a caixa de seleção ao lado da tabela.  
  
3.  Para migrar dados, podem surgir dois casos:  
  
    **Migração de dados do lado do cliente:**  
  
    -   Para realizar **migração de dados do lado do cliente**, selecione o **mecanismo de migração de dados do lado do cliente** opção o **configurações de projeto** caixa de diálogo.  
  
    **Migração de dados do lado do servidor:**  
  
    -   Antes de executar a migração de dados no lado do servidor, verifique se:  
  
        1.  O SSMA para o pacote de extensão do MySQL é instalado na instância do SQL Server.  
  
        2.  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço de agente está em execução na instância do SQL Server  
  
    -   Para realizar **migração de dados do lado do servidor**, selecione o **mecanismo de migração de dados do lado do servidor** opção o **configurações de projeto** caixa de diálogo.  
  
4.  Clique com botão direito **esquemas** no Gerenciador de metadados do MySQL e clique **migrar dados**. Também é possível migrar dados para objetos individuais ou categorias de objetos: clique com botão direito do objeto ou sua pasta pai; Selecione o **migrar dados** opção.  
  
    > [!NOTE]  
    > Se o SSMA para o pacote de extensão MySQL não está instalado na instância do SQL Server e se **mecanismo de migração de dados do lado do servidor** estiver selecionada, ao migrar os dados para o banco de dados de destino, o seguinte erro é encontrado: ' SSMA Componentes de migração de dados não foram encontrados no SQL Server, não será possível realizar a migração de dados do lado do servidor. Verifique se o pacote de extensão está instalado corretamente '. Clique em **Cancelar** para finalizar a migração de dados.  
  
5.  No **conectar-se ao MySQL** caixa de diálogo, insira as credenciais de conexão e, em seguida, clique em **Connect**. Para obter mais informações sobre como se conectar ao MySQL, consulte [conectar-se ao MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
    Se o banco de dados de destino for SQL Server, em seguida, insira as credenciais de conexão na **conectar-se ao SQL Server** caixa de diálogo e clique em **Connect**. Para obter mais informações sobre como se conectar ao SQL Server, consulte [conectar-se ao SQL Server](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    Se o banco de dados de destino do SQL Azure, em seguida, insira as credenciais de conexão na **conectar-se ao SQL Azure** caixa de diálogo e clique em **Connect**. Para obter mais informações sobre como se conectar ao SQL Azure, consulte [conectar-se ao BD SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-azure-sql-db-mysqltosql.md)  
  
    Mensagens serão exibidas as **saída** painel. Quando a migração for concluída, o **relatório de migração de dados** é exibida. Se todos os dados não migrou, clique na linha que contém os erros e, em seguida, clique em **detalhes**. Quando tiver terminado com o relatório, clique em **fechar**. Para obter mais informações sobre o relatório de migração de dados, consulte [relatório de migração de dados (SSMA comum)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Quando o SQL Express edition é usado como o banco de dados de destino, somente cliente lado migração de dados é permitida e não há suporte para a migração de dados do lado servidor.  
  
## <a name="see-also"></a>Consulte também  
[Migrando MySQL bancos de dados para o SQL Server – BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
