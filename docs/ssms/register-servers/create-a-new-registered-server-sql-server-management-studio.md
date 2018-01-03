---
title: Criar um novo servidor registrado (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-registration
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.registerserver.general.sqlce.f1
- sql13.swb.registerserver.general.sqlserver.f1
helpviewer_keywords: Registered Servers [SQL Server], creating new registered servers
ms.assetid: 716ea070-a3b5-4514-9de2-82ce8a96514b
caps.latest.revision: "31"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: eafb023f631824a41ba4e86ebb51f1ca392e6f45
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="create-a-new-registered-server-sql-server-management-studio"></a>Criar um novo servidor registrado (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Este tópico descreve como salvar as informações de conexão para os servidores que você acessa com frequência, registrando o servidor no componente Servidores Registrados do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Um servidor pode ser registrado antes de conectar ou ao conectar o Pesquisador de Objetos. Há uma opção de menu especial para registrar as instâncias de servidor no computador local.  
  
 Há dois tipos de servidores registrados:  
  
-   Grupos do servidor local  
  
     Use os grupos do servidor local para conectar-se facilmente aos servidores que você gerencia com frequência. Os servidores locais e não locais são registrados em grupos do servidor local. Os grupos do servidor local são exclusivos a cada usuário. Para obter informações sobre como compartilhar informações de servidor registrado, veja [Exportar informações de servidor registrado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/export-registered-server-information-sql-server-management-studio.md) e [Importar informações de servidor registrado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/import-registered-server-information-sql-server-management-studio.md).  
  
    > [!NOTE]  
    >  É recomendável usar a Autenticação do Windows sempre que possível.  
  
-   Servidores de Gerenciamento Central  
  
     Os Servidores de Gerenciamento Central armazenam registros de servidor no Servidor de Gerenciamento Central em vez de usar o sistema de arquivos. Os Servidores de Gerenciamento Central e os servidores registrados subordinados podem ser registrados somente com o uso da Autenticação do Windows. Após o registro de um Servidor de Gerenciamento Central, seus servidores registrados associados são exibidos automaticamente. Para obter mais informações sobre Servidores de Gerenciamento Central, veja [Administrar vários servidores usando os Servidores de Gerenciamento Central](../../relational-databases/administer-multiple-servers-using-central-management-servers.md). As versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] não podem ser designadas como um Servidor de Gerenciamento Central.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-automatically-register-the-local-server-instances"></a>Para registrar as instâncias de servidor local automaticamente  
  
-   Em Servidores Registrados, clique com o botão direito do mouse em qualquer nó dos Servidores Registrados e clique em **Atualizar Registro do Servidor Local**.  
  
#### <a name="to-create-a-new-registered-server"></a>Para criar um novo servidor registrado  
  
1.  Se Servidores Registrados não estiverem visíveis em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no menu **Exibir** , clique em **Servidores Registrados**.  
  
     **Tipo de servidor**  
     Quando um servidor é registrado em Servidores Registrados, a caixa **Tipo de servidor** é somente leitura e corresponde ao tipo de servidor exibido no painel Servidores Registrados. Para registrar outro tipo de servidor, clique em **Mecanismo de Banco de Dados**, **Analysis Server**, **Reporting Services**ou **Integration Services** na barra de ferramentas **Servidores Registrados** antes de começar a registrar um novo servidor.  
  
     **Nome do servidor**  
     Selecione a instância do servidor a ser registrada no formato: *\<servername>*[\\*\<instancename>*].  
  
     **Autenticação**  
     Dois modos de autenticação estão disponíveis quando se estabelece conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     **Autenticação do Windows**  
     O modo de Autenticação do Windows permite que um usuário se conecte por meio de uma conta de usuário do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
     **Autenticação do SQL Server**  
     Quando um usuário se conecta com um nome de logon e senha especificados em uma conexão não confiável, o próprio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] efetua a autenticação, verificando se foi definida uma conta de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se a senha especificada corresponde a uma senha registrada previamente. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tiver uma conta de logon definida, ocorrerá falha na autenticação e o usuário receberá uma mensagem de erro.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)] Para obter mais informações, veja [Escolher um modo de autenticação](../../relational-databases/security/choose-an-authentication-mode.md).  
  
     **User name**  
     Mostra o nome de usuário atual com o que você está se conectando. Essa opção somente leitura só estará disponível se você tiver optado por conectar-se usando a Autenticação do Windows. Para alterar **Nomes de usuários**, faça logon no computador como um usuário diferente.  
  
     **Logon**  
     Insira o logon com o qual se conectar. Esta opção só estará disponível se você tiver optado por conectar-se usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Senha**  
     Digite a senha do logon. Esta opção poderá ser editada somente se você tiver optado por conectar-se usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Lembrar senha**  
     Selecione para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criptografe e armazene a senha que você acabou de digitar. Esta opção só será exibida se você tiver optado por conectar-se usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    > [!NOTE]  
    >  Caso você tenha armazenado a senha e não queira mais fazê-lo, desmarque essa caixa de seleção e clique em **Salvar**.  
  
     **Nome do servidor registrado**  
     O nome que você deseja exibir em Servidores Registrados. Esse nome não precisa corresponder à caixa **Nome do servidor** .  
  
     **Descrição do servidor registrado**  
     Digite uma descrição opcional do servidor.  
  
     **Teste**  
     Clique para testar a conexão com o servidor selecionado em **Nome do servidor**.  
  
     **Salvar**  
     Clique para salvar as configurações do servidor registrado.  
  
## <a name="multiserver-queries"></a>Consultas multisservidor  
 A janela de Editor de Consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] pode conectar e consultar várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao mesmo tempo. Os resultados retornados pela consulta podem ser mesclados em um único painel de resultados ou em painéis de resultados separados. Opcionalmente, o Editor de Consultas pode incluir colunas que fornecem o nome do servidor que produziu cada linha, e também o logon usado para conexão com o servidor que forneceu cada linha. Para obter mais informações sobre como executar consultas multisservidor, veja [Executar instruções em vários servidores simultaneamente &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/execute-statements-against-multiple-servers-simultaneously.md).  
  
 Para executar consultas em todos os servidores de um grupo do servidor local, clique com o botão direito do mouse no grupo de servidores, aponte para **Conectar** e clique em **Nova Consulta**. Quando as consultas forem executadas na nova janela do Editor de Consultas, serão executadas em todos os servidores do grupo, usando as informações de conexão armazenadas, inclusive o contexto de autenticação do usuário. Os servidores registrados com o uso da Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mas sem salvar a senha apresentarão falha na conexão.  
  
 Para executar consultas em todos os servidores registrados em um Servidor de Gerenciamento Central, expanda o Servidor de Gerenciamento Central, clique com o botão direito do mouse no grupo de servidores, aponte para clicar em **Conectar**e em **Nova Consulta**. Quando as consultas são executadas na nova janela do Editor de Consultas, elas serão executadas em todos os servidores do grupo, usando as informações de conexão armazenadas e usando o contexto de Autenticação do Windows do usuário.  
  
## <a name="see-also"></a>Consulte Também  
 [Ocultar objetos do sistema no Pesquisador de Objetos](http://msdn.microsoft.com/library/c01d8804-838c-4f75-b78c-80e41e4fffdc)   
 [Exportar informações de servidor registrado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/export-registered-server-information-sql-server-management-studio.md)   
 [Importar informações de servidor registrado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/import-registered-server-information-sql-server-management-studio.md)  
  
  
