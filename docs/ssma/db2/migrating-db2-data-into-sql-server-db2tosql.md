---
title: Migrando dados do DB2 para o SQL Server (DB2ToSQL) | Microsoft Docs
description: Saiba como migrar dados de um banco de dados DB2 para o SQL Server ou o banco de dados SQL do Azure, depois de sincronizar os objetos convertidos.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 86cbd39f-6dac-409a-9ce1-7dd54403f84b
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 408bf80b8c8a6f70488333f476422dedb9db1887
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293963"
---
# <a name="migrating-db2-data-into-sql-server-db2tosql"></a>Migrando dados do DB2 para o SQL Server (DB2ToSQL)
Depois de sincronizar com êxito os objetos convertidos com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você pode migrar dados do DB2 para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
> Se o mecanismo que está sendo usado for o mecanismo de migração de dados do servidor, antes de poder migrar os dados, você deverá instalar o pacote de extensão do SSMA para DB2 e os provedores do DB2 no computador que está executando o SSMA. O serviço de SQL Server Agent também deve estar em execução. Para obter mais informações sobre como instalar o pacote de extensão, consulte [instalando componentes do SSMA no SQL Server](https://msdn.microsoft.com/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
## <a name="setting-migration-options"></a>Definindo opções de migração  
Antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, examine as opções de migração do projeto na caixa de diálogo **configurações do projeto** .  
  
-   Usando essa caixa de diálogo, você pode definir opções como tamanho do lote de migração, bloqueio de tabela, verificação de restrição, manipulação de valor nulo e tratamento de valor de identidade. Para obter mais informações sobre as configurações de migração do projeto, consulte [configurações do projeto (migração)](https://msdn.microsoft.com/48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae).  
  
-   O **mecanismo de migração** na caixa de diálogo **configurações do projeto** permite que o usuário execute o processo de migração usando dois tipos de mecanismos de migração de dados:  
  
    1.  Mecanismo de migração de dados do lado do cliente  
  
    2.  Mecanismo de migração de dados do servidor  
  
**Migração de dados no lado do cliente:**  
  
-   Para iniciar a migração de dados no lado do cliente, selecione a opção **mecanismo de migração de dados do cliente** na caixa de diálogo Configurações do **projeto** .  
  
-   Em **configurações do projeto**, a opção **mecanismo de migração de dados do lado do cliente** é definida.  
  
    > [!NOTE]  
    > O **mecanismo de migração de dados do lado do cliente** reside dentro do aplicativo SSMA e, portanto, não depende da disponibilidade do pacote de extensão.  
  
**Migração de dados no lado do servidor:**  
  
-   Durante a migração de dados do lado do servidor, o mecanismo reside no banco de dados de destino. Ele é instalado por meio do pacote de extensão. Para obter mais informações sobre como instalar o pacote de extensões, consulte [instalando componentes do SSMA no SQL Server](https://msdn.microsoft.com/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
-   Para iniciar a migração no lado do servidor, selecione a opção **mecanismo de migração de dados do servidor** na caixa de diálogo Configurações do **projeto** .  
  
## <a name="migrating-data-to-sql-server"></a>Migrando dados para SQL Server  
A migração de dados é uma operação de carregamento em massa que move linhas de dados de tabelas do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas em transações. O número de linhas carregadas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em cada transação é configurado nas configurações do projeto.  
  
Para exibir as mensagens de migração, verifique se o painel de saída está visível. Caso contrário, no menu **Exibir** , selecione **saída**.  
  
**Para migrar dados**  
  
1.  Verifique o seguinte:  
  
    -   Os provedores do DB2 são instalados no computador que está executando o SSMA.  
  
    -   Você sincronizou os objetos convertidos com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados.  
  
2.  No Gerenciador de metadados do DB2, selecione os objetos que contêm os dados que você deseja migrar:  
  
    -   Para migrar dados para todos os esquemas, marque a caixa de seleção ao lado de **esquemas**.  
  
    -   Para migrar dados ou omitir tabelas individuais, primeiro expanda o esquema, expanda **tabelas**e marque ou desmarque a caixa de seleção ao lado da tabela.  
  
3.  Para migrar dados, surgem dois casos:  
  
    **Migração de dados no lado do cliente:**  
  
    -   Para executar a **migração de dados no lado do cliente**, selecione a opção mecanismo de migração de dados do **cliente** na caixa de diálogo Configurações do **projeto** .  
  
    **Migração de dados no lado do servidor:**  
  
    -   Antes de executar a migração de dados no lado do servidor, verifique se:  
  
        1.  O pacote de extensão do SSMA para DB2 é instalado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
        2.  O serviço de SQL Server Agent está em execução na instância do SQL Server.  
  
    -   Para executar a **migração de dados no servidor**, selecione a opção mecanismo de migração de dados do **servidor** na caixa de diálogo Configurações do **projeto** .  
  
4.  Clique com o botão direito do mouse em **esquemas** no Gerenciador de metadados do DB2 e clique em **migrar dados**. Você também pode migrar dados para objetos individuais ou categorias de objetos: clique com o botão direito do mouse no objeto ou em sua pasta pai; Selecione a opção **migrar dados** .  
  
    > [!NOTE]  
    > Se o pacote de extensão do SSMA para DB2 não estiver instalado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se o **mecanismo de migração de dados do servidor** for selecionado, ao migrar os dados para o banco de dado de destino, o seguinte erro será encontrado: ' componentes de migração de dados do SSMA não foram encontrados no SQL Server, a migração de dados do servidor não será possível. Verifique se o pacote de extensões está instalado corretamente '. Clique em **Cancelar** para encerrar a migração de dados.  
  
5.  Na caixa de diálogo **conectar ao DB2** , insira as credenciais de conexão e clique em **conectar**. Para obter mais informações sobre como se conectar ao DB2, consulte [conectando-se ao banco de dados DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
  
    Para se conectar ao banco de dados de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , insira as credenciais de conexão na caixa de diálogo **conectar a SQL Server** e clique em **conectar**. Para obter mais informações sobre como se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [conectando-se ao SQL Server](https://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e)  
  
    As mensagens serão exibidas no painel de **saída** . Quando a migração for concluída, o **relatório de migração de dados** será exibido. Se algum dado não for migrado, clique na linha que contém os erros e, em seguida, clique em **detalhes**. Ao concluir o relatório, clique em **fechar**. Para obter mais informações sobre o relatório de migração de dados, consulte [relatório de migração de dados (SSMA Common)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Quando o SQL Express Edition é usado como o banco de dados de destino, somente a migração de dado do lado do cliente é permitida e não há suporte para a migração de dados do lado do servidor.  
  
## <a name="see-also"></a>Consulte Também  
[Migrar dados do DB2 para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
