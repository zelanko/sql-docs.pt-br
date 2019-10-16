---
title: 'Lição 1: Conectando ao Mecanismo de Banco de Dados | Microsoft Docs'
ms.custom: ''
ms.date: 02/05/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: quickstart
ms.assetid: e8db82f0-50ed-4531-9209-940006ed34cb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1ab78eab73526568736dea8c4aef1525b2607c93
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2019
ms.locfileid: "72162561"
---
# <a name="lesson-1-connecting-to-the-database-engine"></a>Lição 1: conexão ao mecanismo de banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Quando você instala o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)], as ferramentas instaladas dependem da edição e de suas opções de instalação. Esta lição analisa as principais ferramentas e mostra como conectar e executar uma função básica (autorizar mais usuários).  

Esta lição contém as seguintes tarefas:  
- [Ferramentas para introdução](#tools)  
- [Conectando-se ao Management Studio](#connect)  
- [Autorizando conexões adicionais](#additional) 

## <a name="tools">Ferramentas para introdução</a> 
- O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] transporta com uma variedade de ferramentas. Este tópico descreve as primeiras ferramentas das que você precisará e o ajuda a selecionar a ferramenta certa para o trabalho. Todas as ferramentas podem ser acessadas no menu **Iniciar** . Algumas ferramentas, como [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], não são instaladas por padrão. Você deve selecionar as ferramentas como parte dos componentes de cliente durante a instalação. Para obter uma descrição completa das ferramentas descritas abaixo, pesquise-as nos Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] contém somente um subconjunto das ferramentas.  

### <a name="basic-tools"></a>Ferramentas básicas
- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) é a principal ferramenta para administrar o [!INCLUDE[ssDE](../includes/ssde-md.md)] e gravar o código [!INCLUDE[tsql](../includes/tsql-md.md)] . Fica hospedado no shell [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] . O SSMS está disponível como download gratuito no [Centro de Download da Microsoft](https://msdn.microsoft.com/library/mt238290.aspx). A versão mais recente pode ser usada com versões mais antigas do [!INCLUDE[ssDE_md](../includes/ssde-md.md)].  

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager é instalado com [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e as ferramentas de cliente. Ela permite que você habilite protocolos de servidor, configure opções de protocolo como portas de TCP, configure serviços de servidor para iniciar automaticamente e configure computadores de cliente para conectar de sua maneira preferida. Esta ferramenta configura os mais avançados elementos de conectividade mas não habilita recursos.  

### <a name="sample-database"></a>Banco de dados de exemplos
Os bancos de dados de exemplo e os exemplos não estão incluídos no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A maioria dos exemplos descritos nos Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa o banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] .  

##### <a name="to-start-sql-server-management-studio"></a>Para iniciar o SQL Server Management Studio
- Nas versões atuais do Windows, na página **Inicial** , digite SSMS e clique em **Microsoft SQL Server Management Studio**.  
- Quando estiver usando versões mais antigas do Windows, no menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]e clique em **SQL Server Management Studio**.  

##### <a name="to-start-sql-server-configuration-manager"></a>Para iniciar o SQL Server Configuration Manager  
- Nas versões atuais do Windows, na página **Iniciar** , digite **Configuration Manager**e clique em **SQL Server *versão* Configuration Manager**.   
- Quando estiver usando versões mais antigas do Windows, no menu **Iniciar** , aponte para **Todos os Programas**, para [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  

## <a name="connect"></a>Conectando-se ao Management Studio  
- É fácil se conectar ao [!INCLUDE[ssDE](../includes/ssde-md.md)] por meio de ferramentas executadas no mesmo computador se você sabe o nome da instância e está se conectando como um membro do grupo de Administradores local no computador. Os procedimentos seguintes devem ser executados no mesmo computador que hospeda o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  

> [!NOTE]  
> Este tópico aborda a conexão a um SQL Server local. Para se conectar ao Banco de Dados SQL do Azure, consulte [Conectar-se ao banco de dados SQL com o SQL Server Management Studio e executar uma consulta T-SQL de exemplo](https://azure.microsoft.com/documentation/articles/sql-database-connect-query-ssms/).  

##### <a name="to-determine-the-name-of-the-instance-of-the-database-engine"></a>Para determinar o nome da instância do Mecanismo de Banco de Dados.  

1.  Faça logon no Windows como membro do grupo Administradores e abra o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
2.  Na caixa de diálogo **Conectar ao Servidor** , clique em **Cancelar**.  
3.  Se Servidores Registrados não aparecer, no menu **Exibir** , clique em **Servidores Registrados**.
4.  Com **Mecanismo de Banco de Dados** selecionado na barra de ferramentas Servidores Registrados, expanda **Mecanismo do Banco de Dados**, clique com o botão direito do mouse em **Grupos do Servidor Local**, aponte para **Tarefas**e clique em **Registrar Servidores Locais**. Expanda **Grupos de Servidores Locais** para ver todas as instâncias do [!INCLUDE[ssDE](../includes/ssde-md.md)] instaladas no computador exibido. A instância padrão é sem-nome e é mostrada como o nome do computador. Uma instância nomeada é exibida como o nome do computador seguido de uma barra invertida (\\) e do nome da instância. Para o [!INCLUDE[ssExpress](../includes/ssexpress-md.md)], a instância é chamada *<computer_name>* \sqlexpress, exceto se o nome for alterado durante a instalação.  

[!INCLUDE[fresh-note-steps-feedback](../includes/paragraph-content/fresh-note-steps-feedback.md)]

##### <a name="to-verify-that-the-database-engine-is-running"></a>Para verificar se o Mecanismo de Banco de Dados está sendo executado

1.  Em Servidores Registrados, se o nome de sua instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiver um ponto verde, com uma seta branca próximo ao nome, o [!INCLUDE[ssDE](../includes/ssde-md.md)] está sendo executado e nenhuma ação adicional é necessária.  

2.  Se o nome de sua instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiver um ponto vermelho, com um quadrado branco próximo ao nome, o [!INCLUDE[ssDE](../includes/ssde-md.md)] foi interrompido. Clique com o botão direito do mouse no nome do [!INCLUDE[ssDE](../includes/ssde-md.md)], clique em **Controle de Serviços**e em **Iniciar**. Depois de uma caixa de diálogo de confirmação, o [!INCLUDE[ssDE](../includes/ssde-md.md)] deverá iniciar e o círculo deverá ficar verde com uma seta branca.  

##### <a name="to-connect-to-the-database-engine"></a>Para conectar-se ao Mecanismo de Banco de Dados  

Pelo menos uma conta de administrador foi selecionada quando o [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] estava sendo instalado. Execute o procedimento a seguir enquanto estiver conectado no Windows como administrador.

1.  No [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], no menu **Arquivo** , clique em **Conectar Pesquisador de Objetos**. 
- A caixa de diálogo **Conectar ao Servidor** é exibida. A caixa **Tipo de servidor** exibe o tipo de componente que foi usado por último.  

2.  Selecione **Mecanismo de Banco de Dados**.

![object-explorer](../relational-databases/media/object-explorer.png)

3.  Na caixa **Nome do servidor** , digite o nome da instância do [!INCLUDE[ssDE](../includes/ssde-md.md)]. Para a instância padrão do SQL Server, o nome do servidor é o nome do computador. Para uma instância nomeada do SQL Server, o nome do servidor é o _\<computer_name\>_ **\\** _\<instance_name\>_ , como **ACCTG_SRVR\SQLEXPRESS**. A captura de tela a seguir mostra a conexão à instância padrão (sem nome) do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] em um computador chamado “PracticeComputer”. O usuário conectado no Windows é Marina do domínio Contoso. Ao usar a Autenticação do Windows, não é possível alterar o nome de usuário. 

![connect-to-server](../relational-databases/media/connect-to-server.png)

4.  Clique em **Conectar**.

> [!NOTE]
> Este tutorial presume que você não esteja familiarizado com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e que não tenha problemas especiais em estabelecer a conexão. Isso deve ser suficiente para a maioria das pessoas e mantém este tutorial simples. Para obter as etapas de solução de problemas, consulte [Solucionando problemas de conexão com o Mecanismo de Banco de Dados do SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md). 

## <a name="additional"></a>Autorizando conexões adicionais  
Agora que você se conectou ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como um administrador, uma de suas primeiras tarefas é autorizar que outros usuários se conectem. Você faz isso criando um logon e autorizando esse logon para acessar um banco de dados como um usuário. Logons podem ser de autenticação do Windows, que usam credenciais do Windows ou logons de autenticação do SQL Server, que armazenam informações de autenticação no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e são independentes de suas credenciais do Windows. Use a autenticação do Windows sempre que possível.

> [!TIP]
> A maioria das organizações tem usuários de domínio e usará a Autenticação do Windows. Você pode experimentar por conta própria, criando usuários locais adicionais no computador. Os usuários locais serão autenticados pelo seu computador e, portanto, o domínio é o nome do computador. Por exemplo, se o cálculo é chamado `MyComputer` e você cria um usuário chamado `Test`, a descrição do Windows sobre o usuário é `Mycomputer\Test`.  

##### <a name="create-a-windows-authentication-login"></a>Crie um logon de autenticação do Windows 

1.  Na tarefa anterior, você se conectou ao [!INCLUDE[ssDE](../includes/ssde-md.md)] usando o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. No Pesquisador de Objetos, expanda sua instância de servidor, expanda **Segurança**, clique com o botão direito do mouse em **Logons**e clique em **Novo Logon**. A caixa de diálogo **Logon – Novo** é exibida.  

2.  Na página **Geral** , na caixa **Nome de logon** , digite um logon de Windows no formato: `<domain>\\<login>`

![new-login](../relational-databases/media/new-login.png)

3.  Na caixa **Banco de dados padrão** , selecione [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] , caso esteja disponível. Caso contrário, selecione **mestre**.  
4.  Na página **Funções do Servidor** , se o novo logon for um administrador, clique em **sysadmin**; caso contrário, deixe este espaço em branco.  
5.  Na página **Mapeamento de Usuário** , selecione **Mapa** para o banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] , caso ele esteja disponível. Caso contrário, selecione **mestre**. Observe que a caixa **Usuário** é populada com o logon. Depois de fechada, a caixa de diálogo criará esse usuário no banco de dados.  
6.  Na caixa **Esquema Padrão** , digite **dbo** para mapear o logon para o esquema de proprietário de banco de dados.   
7.  Aceite as configurações padrão nas caixas **Protegíveis** e **Status** e clique em **OK** para criar o logon.  

> [!IMPORTANT]  
> Essas são as informações básicas para começar. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornece um ambiente de segurança avançado e a segurança é obviamente um aspecto importante das operações de banco de dados.  

## <a name="next-lesson"></a>Próxima lição  
[Lição 2: Conectando de outro computador](../relational-databases/lesson-2-connecting-from-another-computer.md)    
  
