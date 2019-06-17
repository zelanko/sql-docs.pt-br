---
title: Migrando dados do DB2 para o SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 86cbd39f-6dac-409a-9ce1-7dd54403f84b
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c64b1ea3ecc283cdea92a5722c7a1dad120ecb50
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63272783"
---
# <a name="migrating-db2-data-into-sql-server-db2tosql"></a>Migrar dados do DB2 para o SQL Server (DB2ToSQL)
Depois de ter sincronizado com êxito com objetos convertidos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode migrar dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
> Se o mecanismo que está sendo usado é o mecanismo de migração de dados do lado do servidor, em seguida, antes de migrar dados, você deve instalar o SSMA para DB2 pacote de extensão e os provedores de DB2 no computador que está executando o SSMA. Também deve estar executando o serviço SQL Server Agent. Para obter mais informações sobre como instalar o pacote de extensão, consulte [instalando os componentes do SSMA no SQL Server](https://msdn.microsoft.com/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
## <a name="setting-migration-options"></a>Definindo opções de migração  
Antes de migrar dados a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], examine as opções de migração de projeto na **configurações do projeto** caixa de diálogo.  
  
-   Usando essa caixa de diálogo, você pode definir opções de como o tamanho do lote de migração, bloqueio de tabela, verificação de restrição, manipulação de valor nulo e lidar com valor de identidade. Para obter mais informações sobre as configurações de projeto de migração, consulte [configurações do projeto (migração)](https://msdn.microsoft.com/48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae).  
  
-   O **mecanismo de migração** na **configurações do projeto** caixa de diálogo permite que o usuário execute o processo de migração usando dois tipos de mecanismos de migração de dados:  
  
    1.  Mecanismo de migração de dados do lado cliente  
  
    2.  Mecanismo de migração de dados do lado servidor  
  
**Migração de dados do lado do cliente:**  
  
-   Para iniciar a migração de dados no lado do cliente, selecione a **mecanismo de migração de dados do lado do cliente** opção a **configurações do projeto** caixa de diálogo.  
  
-   Na **configurações do projeto**, o **mecanismo de migração de dados do lado do cliente** opção está definida.  
  
    > [!NOTE]  
    > O **mecanismo de migração de dados do lado do cliente** reside dentro do aplicativo do SSMA e, portanto, não depende da disponibilidade do pacote de extensão.  
  
**Migração de dados do lado do servidor:**  
  
-   Durante a migração de dados do lado do servidor, o mecanismo no qual reside o banco de dados de destino. Ele é instalado pelo pacote de extensão. Para obter mais informações sobre como instalar o pacote de extensão, consulte [instalando os componentes do SSMA no SQL Server](https://msdn.microsoft.com/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
-   Para iniciar a migração no lado do servidor, selecione a **mecanismo de migração de dados do lado do servidor** opção a **configurações do projeto** caixa de diálogo.  
  
## <a name="migrating-data-to-sql-server"></a>Migrando dados para o SQL Server  
Migração de dados são uma operação de carregamento em massa que move as linhas de dados de tabelas do DB2 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas em transações. O número de linhas carregado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em cada transação é configurado nas configurações do projeto.  
  
Para exibir mensagens de migração, certifique-se de que o painel de saída está visível. Caso contrário, do **modo de exibição** menu, selecione **saída**.  
  
**Para migrar dados**  
  
1.  Verifique o seguinte:  
  
    -   Os provedores do DB2 são instalados no computador que está executando o SSMA.  
  
    -   Você sincronizou os objetos convertidos com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados.  
  
2.  No Gerenciador de metadados do DB2, selecione os objetos que contêm os dados que você deseja migrar:  
  
    -   Para migrar dados para todos os esquemas, marque a caixa de seleção ao lado **esquemas**.  
  
    -   Para migrar os dados ou omitir tabelas individuais, primeiro expanda o esquema, expanda **tabelas**e, em seguida, selecione ou desmarque a caixa de seleção ao lado da tabela.  
  
3.  Para migrar dados, podem surgir dois casos:  
  
    **Migração de dados do lado do cliente:**  
  
    -   Para realizar **migração de dados do lado do cliente**, selecione o **mecanismo de migração de dados do lado do cliente** opção o **configurações de projeto** caixa de diálogo.  
  
    **Migração de dados do lado do servidor:**  
  
    -   Antes de executar a migração de dados no lado do servidor, verifique se:  
  
        1.  O SSMA para DB2 extensão Pack está instalado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
        2.  O serviço SQL Server Agent está em execução na instância do SQL Server.  
  
    -   Para realizar **migração de dados do lado do servidor**, selecione o **mecanismo de migração de dados do lado do servidor** opção o **configurações de projeto** caixa de diálogo.  
  
4.  Clique com botão direito **esquemas** no Gerenciador de metadados do DB2 e clique **migrar dados**. Também é possível migrar dados para objetos individuais ou categorias de objetos: Clique com botão direito do objeto ou sua pasta pai; Selecione o **migrar dados** opção.  
  
    > [!NOTE]  
    > Se o SSMA para DB2 pacote de extensão não está instalado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e se **mecanismo de migração de dados do lado do servidor** estiver selecionada, ao migrar os dados para o banco de dados de destino, o seguinte erro é encontrado: ' Componentes SSMA de migração de dados não foram encontrados no SQL Server, não será possível realizar a migração de dados do lado do servidor. Verifique se o pacote de extensão está instalado corretamente '. Clique em **Cancelar** para finalizar a migração de dados.  
  
5.  No **conectar-se ao DB2** caixa de diálogo, insira as credenciais de conexão e, em seguida, clique em **Connect**. Para obter mais informações sobre como se conectar ao DB2, consulte [conectar-se ao banco de dados DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
  
    Para conectar-se ao banco de dados de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], insira as credenciais de conexão na **conectar ao SQL Server** caixa de diálogo e clique em **Connect**. Para obter mais informações sobre como se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [conectando ao SQL Server](https://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e)  
  
    Mensagens serão exibidas as **saída** painel. Quando a migração for concluída, o **relatório de migração de dados** é exibida. Se todos os dados não migrou, clique na linha que contém os erros e, em seguida, clique em **detalhes**. Quando tiver terminado com o relatório, clique em **fechar**. Para obter mais informações sobre o relatório de migração de dados, consulte [relatório de migração de dados (SSMA comum)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Quando o SQL Express edition é usado como o banco de dados de destino, somente cliente lado migração de dados é permitida e não há suporte para a migração de dados do lado servidor.  
  
## <a name="see-also"></a>Consulte também  
[Migrando dados do DB2 para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
