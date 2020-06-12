---
title: Migrando dados do Oracle para o SQL Server (OracleToSQL) | Microsoft Docs
description: Saiba como migrar dados de um Oracle Database para SQL Server, depois de sincronizar os objetos convertidos, usando o aplicativo SSMA para Oracle.
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
manager: shamikg
ms.openlocfilehash: f617b850482383400d599d7608644f27da58f17e
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293813"
---
# <a name="migrating-oracle-data-into-sql-server-oracletosql"></a>Migração de dados do Oracle para o SQL Server (OracleToSQL)
Depois de sincronizar com êxito os objetos convertidos com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você pode migrar dados do Oracle para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
> Se o mecanismo que está sendo usado for o mecanismo de migração de dados do servidor, então, antes de poder migrar dados, você deverá instalar o pacote de extensão do SSMA para Oracle e os provedores Oracle no computador que está executando o SSMA. O serviço de SQL Server Agent também deve estar em execução. Para obter mais informações sobre como instalar o pacote de extensão, consulte [Installing Server Components (OracleToSQL)](https://msdn.microsoft.com/33070e5f-4e39-4b70-ae81-b8af6e4983c5)  
  
## <a name="setting-migration-options"></a>Definindo opções de migração  
Antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, examine as opções de migração do projeto na caixa de diálogo **configurações do projeto** .  
  
-   Usando essa caixa de diálogo, você pode definir opções como tamanho do lote de migração, bloqueio de tabela, verificação de restrição, manipulação de valor nulo e tratamento de valor de identidade. Para obter mais informações sobre as configurações de migração do projeto, consulte [configurações do projeto (migração) (OracleToSQL)](https://msdn.microsoft.com/fcd6b988-633b-4b2b-9f36-6368b5e86b60).  
  
-   O **mecanismo de migração** na caixa de diálogo **configurações do projeto** permite que o usuário execute o processo de migração usando dois tipos de mecanismos de migração de dados:  
  
    1.  Mecanismo de migração de dados do lado do cliente  
  
    2.  Mecanismo de migração de dados do servidor  
  
**Migração de dados no lado do cliente:**  
  
-   Para iniciar a migração de dados no lado do cliente, selecione a opção **mecanismo de migração de dados do cliente** na caixa de diálogo Configurações do **projeto** .  
  
-   Em **configurações do projeto**, a opção **mecanismo de migração de dados do lado do cliente** é definida.  
  
    > [!NOTE]  
    > O **mecanismo de migração de dados do lado do cliente** reside dentro do aplicativo SSMA e, portanto, não depende da disponibilidade do pacote de extensão.  
  
**Migração de dados no lado do servidor:**  
  
-   Durante a migração de dados do lado do servidor, o mecanismo reside no banco de dados de destino. Ele é instalado por meio do pacote de extensão. Para obter mais informações sobre como instalar o pacote de extensão, consulte [Installing Server Components on SQL Server](installing-ssma-components-on-sql-server-oracletosql.md)  
  
-   Para iniciar a migração no lado do servidor, selecione a opção **mecanismo de migração de dados do servidor** na caixa de diálogo Configurações do **projeto** .  
  
## <a name="migrating-data-to-sql-server"></a>Migrando dados para SQL Server  
A migração de dados é uma operação de carregamento em massa que move linhas de dados de tabelas do Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas em transações. O número de linhas carregadas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em cada transação é configurado nas configurações do projeto.  
  
Para exibir as mensagens de migração, verifique se o painel de saída está visível. Caso contrário, no menu **Exibir** , selecione **saída**.  
  
**Para migrar dados**  
  
1.  Verifique o seguinte:  
  
    -   Os provedores Oracle são instalados no computador que está executando o SSMA.  
  
    -   Você sincronizou os objetos convertidos com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados.  
  
2.  No Gerenciador de metadados Oracle, selecione os objetos que contêm os dados que você deseja migrar:  
  
    -   Para migrar dados para todos os esquemas, marque a caixa de seleção ao lado de **esquemas**.  
  
    -   Para migrar dados ou omitir tabelas individuais, primeiro expanda o esquema, expanda **tabelas**e marque ou desmarque a caixa de seleção ao lado da tabela.  
  
3.  Para migrar dados, surgem dois casos:  
  
    **Migração de dados no lado do cliente:**  
  
    -   Para executar a **migração de dados no lado do cliente**, selecione a opção mecanismo de migração de dados do **cliente** na caixa de diálogo Configurações do **projeto** .  
  
    **Migração de dados no lado do servidor:**  
  
    -   Antes de executar a migração de dados no lado do servidor, verifique se:  
  
        1.  O pacote de extensão do SSMA para Oracle é instalado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
        2.  O serviço de SQL Server Agent está em execução na instância do SQL Server.  
  
    -   Para executar a **migração de dados no servidor**, selecione a opção mecanismo de migração de dados do **servidor** na caixa de diálogo Configurações do **projeto** .  
  
4.  Clique com o botão direito do mouse em **esquemas** no Gerenciador de metadados Oracle e clique em **migrar dados**. Você também pode migrar dados para objetos individuais ou categorias de objetos: clique com o botão direito do mouse no objeto ou em sua pasta pai; Selecione a opção **migrar dados** .  
  
    > [!NOTE]  
    > Se o pacote de extensão do SSMA para Oracle não estiver instalado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se o **mecanismo de migração de dados do servidor** for selecionado, ao migrar os dados para o banco de dado de destino, o seguinte erro será encontrado: ' componentes de migração de dados do SSMA não foram encontrados no SQL Server, a migração de dados do servidor não será possível. Verifique se o pacote de extensões está instalado corretamente '. Clique em **Cancelar** para encerrar a migração de dados.  
  
5.  Na caixa de diálogo **conectar ao Oracle** , insira as credenciais de conexão e clique em **conectar**. Para obter mais informações sobre como se conectar ao Oracle, consulte [conectar-se ao oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)  
  
    Para se conectar ao banco de dados de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , insira as credenciais de conexão na caixa de diálogo **conectar a SQL Server** e clique em **conectar**. Para obter mais informações sobre como se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [conectar-se ao SQL Server](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    As mensagens serão exibidas no painel de **saída** . Quando a migração for concluída, o **relatório de migração de dados** será exibido. Se algum dado não for migrado, clique na linha que contém os erros e, em seguida, clique em **detalhes**. Ao concluir o relatório, clique em **fechar**. Para obter mais informações sobre o relatório de migração de dados, consulte [relatório de migração de dados (SSMA Common)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Quando o SQL Express Edition é usado como o banco de dados de destino, somente a migração de dado do lado do cliente é permitida e não há suporte para a migração de dados do lado do servidor.  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados Oracle para SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
