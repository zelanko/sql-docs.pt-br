---
title: Migração de dados Oracle para o SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Oracle Data Migration, Client-Side Migration
- Oracle Data Migration,Server-Side Migration
ms.assetid: e23c5268-41ed-4e55-9fe7-a11376202a13
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: ad944432b2a00acb923732863624a69dcbaf227f
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52418287"
---
# <a name="migrating-oracle-data-into-sql-server-oracletosql"></a>Migração de dados do Oracle para o SQL Server (OracleToSQL)
Depois de ter sincronizado com êxito com objetos convertidos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode migrar dados do Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
> Se o mecanismo que está sendo usado é o mecanismo de migração de dados do lado do servidor, em seguida, antes de migrar dados, você deve instalar o SSMA para Oracle pacote de extensão e os provedores da Oracle no computador que está executando o SSMA. Também deve estar executando o serviço SQL Server Agent. Para obter mais informações sobre como instalar o pacote de extensão, consulte [instalando os componentes do servidor (OracleToSQL)](https://msdn.microsoft.com/33070e5f-4e39-4b70-ae81-b8af6e4983c5)  
  
## <a name="setting-migration-options"></a>Definindo opções de migração  
Antes de migrar dados a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], examine as opções de migração de projeto na **configurações do projeto** caixa de diálogo.  
  
-   Usando essa caixa de diálogo, você pode definir opções de como o tamanho do lote de migração, bloqueio de tabela, verificação de restrição, manipulação de valor nulo e lidar com valor de identidade. Para obter mais informações sobre as configurações de projeto de migração, consulte [configurações do projeto (migração) (OracleToSQL)](https://msdn.microsoft.com/fcd6b988-633b-4b2b-9f36-6368b5e86b60).  
  
-   O **mecanismo de migração** na **configurações do projeto** caixa de diálogo permite que o usuário execute o processo de migração usando dois tipos de mecanismos de migração de dados:  
  
    1.  Mecanismo de migração de dados do lado cliente  
  
    2.  Mecanismo de migração de dados do lado servidor  
  
**Migração de dados do lado do cliente:**  
  
-   Para iniciar a migração de dados no lado do cliente, selecione a **mecanismo de migração de dados do lado do cliente** opção a **configurações do projeto** caixa de diálogo.  
  
-   Na **configurações do projeto**, o **mecanismo de migração de dados do lado do cliente** opção está definida.  
  
    > [!NOTE]  
    > O **mecanismo de migração de dados do lado do cliente** reside dentro do aplicativo do SSMA e, portanto, não depende da disponibilidade do pacote de extensão.  
  
**Migração de dados do lado do servidor:**  
  
-   Durante a migração de dados do lado do servidor, o mecanismo no qual reside o banco de dados de destino. Ele é instalado pelo pacote de extensão. Para obter mais informações sobre como instalar o pacote de extensão, consulte [instalando os componentes do servidor no SQL Server](installing-ssma-components-on-sql-server-oracletosql.md)  
  
-   Para iniciar a migração no lado do servidor, selecione a **mecanismo de migração de dados do lado do servidor** opção a **configurações do projeto** caixa de diálogo.  
  
## <a name="migrating-data-to-sql-server"></a>Migrando dados para o SQL Server  
Migração de dados são uma operação de carregamento em massa que move as linhas de dados de tabelas do Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas em transações. O número de linhas carregado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em cada transação é configurado nas configurações do projeto.  
  
Para exibir mensagens de migração, certifique-se de que o painel de saída está visível. Caso contrário, do **modo de exibição** menu, selecione **saída**.  
  
**Para migrar dados**  
  
1.  Verifique o seguinte:  
  
    -   Os provedores da Oracle são instalados no computador que está executando o SSMA.  
  
    -   Você sincronizou os objetos convertidos com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados.  
  
2.  No Gerenciador de metadados do Oracle, selecione os objetos que contêm os dados que você deseja migrar:  
  
    -   Para migrar dados para todos os esquemas, marque a caixa de seleção ao lado **esquemas**.  
  
    -   Para migrar os dados ou omitir tabelas individuais, primeiro expanda o esquema, expanda **tabelas**e, em seguida, selecione ou desmarque a caixa de seleção ao lado da tabela.  
  
3.  Para migrar dados, podem surgir dois casos:  
  
    **Migração de dados do lado do cliente:**  
  
    -   Para realizar **migração de dados do lado do cliente**, selecione o **mecanismo de migração de dados do lado do cliente** opção o **configurações de projeto** caixa de diálogo.  
  
    **Migração de dados do lado do servidor:**  
  
    -   Antes de executar a migração de dados no lado do servidor, verifique se:  
  
        1.  O SSMA para Oracle extensão Pack está instalado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
        2.  O serviço SQL Server Agent está em execução na instância do SQL Server.  
  
    -   Para realizar **migração de dados do lado do servidor**, selecione o **mecanismo de migração de dados do lado do servidor** opção o **configurações de projeto** caixa de diálogo.  
  
4.  Clique com botão direito **esquemas** no Gerenciador de metadados do Oracle e clique **migrar dados**. Também é possível migrar dados para objetos individuais ou categorias de objetos: Clique com botão direito do objeto ou sua pasta pai; Selecione o **migrar dados** opção.  
  
    > [!NOTE]  
    > Se o SSMA para Oracle pacote de extensão não está instalado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e se **mecanismo de migração de dados do lado do servidor** estiver selecionada, ao migrar os dados para o banco de dados de destino, o seguinte erro é encontrado: ' Componentes SSMA de migração de dados não foram encontrados no SQL Server, não será possível realizar a migração de dados do lado do servidor. Verifique se o pacote de extensão está instalado corretamente '. Clique em **Cancelar** para finalizar a migração de dados.  
  
5.  No **conectar-se ao Oracle** caixa de diálogo, insira as credenciais de conexão e, em seguida, clique em **Connect**. Para obter mais informações sobre como se conectar ao Oracle, consulte [conectar-se ao Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)  
  
    Para conectar-se ao banco de dados de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], insira as credenciais de conexão na **conectar ao SQL Server** caixa de diálogo e clique em **Connect**. Para obter mais informações sobre como se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [conectar-se ao SQL Server](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    Mensagens serão exibidas as **saída** painel. Quando a migração for concluída, o **relatório de migração de dados** é exibida. Se todos os dados não migrou, clique na linha que contém os erros e, em seguida, clique em **detalhes**. Quando tiver terminado com o relatório, clique em **fechar**. Para obter mais informações sobre o relatório de migração de dados, consulte [relatório de migração de dados (SSMA comum)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Quando o SQL Express edition é usado como o banco de dados de destino, somente cliente lado migração de dados é permitida e não há suporte para a migração de dados do lado servidor.  
  
## <a name="see-also"></a>Consulte também  
[Migrando do Oracle bancos de dados para o SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
