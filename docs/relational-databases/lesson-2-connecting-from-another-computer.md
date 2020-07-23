---
title: 'Lição 2: Conectando em outro computador | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: fd4ddeb8-0cb6-441b-9704-03575c07020f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0022e0e740e9c4268ddf08340029c2e74a101437
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922844"
---
# <a name="lesson-2-connecting-from-another-computer"></a>Lição 2: conexão usando outro computador
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]
Para aumentar a segurança, o [!INCLUDE[ssDE](../includes/ssde-md.md)] das edições Developer, Express e Evaluation do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não pode ser acessado de outro computador quando inicialmente instalado. Esta lição mostra a você como habilitar os protocolos, configurar as portas e configurar o Firewall do Windows para se conectar de outros computadores.  
  
Esta lição contém as seguintes tarefas:  
  
-   [Habilitando protocolos](#protocols)  
  
-   [Configurando uma porta fixa](#port)  
  
-   [Abrindo portas no Firewall](#firewall)  
  
-   [Conectando-se ao Mecanismo de Banco de dados de outro computador](#otherComp)  
  
-   [Conectando-se usando o SQL Server Browser Service](#browser)  
  
## <a name="enabling-protocols"></a><a name="protocols"></a>Habilitando protocolos  
Para aumentar a segurança, o [!INCLUDE[ssExpress](../includes/ssexpress-md.md)], Developer, e Evaluation são instalados apenas com conectividade de rede limitada. Conexões com o [!INCLUDE[ssDE](../includes/ssde-md.md)] podem ser feitas de ferramentas que estão sendo executadas no mesmo computador, mas não de outros computadores. Se você estiver planejando realizar o trabalho de desenvolvimento no mesmo computador que o [!INCLUDE[ssDE](../includes/ssde-md.md)], não precisa habilitar protocolos adicionais. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] se conectará ao [!INCLUDE[ssDE](../includes/ssde-md.md)] usando o protocolo de memória compartilhada. Esse protocolo já está habilitado.  
  
Se você planejar conectar-se ao [!INCLUDE[ssDE](../includes/ssde-md.md)] de outro computador, deverá habilitar um protocolo, como TCP/IP.  
  
#### <a name="how-to-enable-tcpip-connections-from-another-computer"></a>Como habilitar conexões TCP/IP de outro computador  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
    > [!NOTE]  
    > Você pode ter opções de 32 bits e de 64 bits disponíveis.  
  
    > [!NOTE]  
    > Como o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa Console de Gerenciamento [!INCLUDE[msCoName](../includes/msconame-md.md)] e não um programa autônomo, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo nas versões mais recentes do Windows. O nome do arquivo contém um número que representa o número de versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para abrir o Gerenciador de Configuração no comando Executar, veja abaixo os caminhos para as últimas quatro versões quando o Windows é instalado na unidade C.  
  
    |||  
    |-|-|
    |[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]|C:\Windows\SysWOW64\SQLServerManager14.msc|
    |[!INCLUDE[ssSQL16](../includes/sssql16-md.md)]|C:\Windows\SysWOW64\SQLServerManager13.msc|  
    |[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]|C:\Windows\SysWOW64\SQLServerManager12.msc|  
    |[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]|C:\Windows\SysWOW64\SQLServerManager11.msc|
  
2.  No **SQL Server Configuration Manager**, expanda **Configuração de Rede do SQL Server** e, em seguida, clique em **Protocolos para** _<InstanceName>_ .  
  
    A instância padrão (uma instância sem nome) é listada como **MSSQLSERVER**. Se você instalou uma instância nomeada, o nome fornecido será listado. [!INCLUDE[ssExpressEd11](../includes/ssexpressed11-md.md)] é instalado como **SQLEXPRESS**, a menos que o nome seja alterado durante a instalação.  
  
3.  Na lista de protocolos, clique com o botão direito do mouse no protocolo que deseja habilitar (**TCP/IP**) e clique em **Habilitar**.  
  
    > [!NOTE]  
    > E necessário reiniciar o serviço [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] após fazer alterações nos protocolos de rede. No entanto, isso é executado na próxima tarefa.  

## <a name="configuring-a-fixed-port"></a><a name="port"></a>Configurando uma porta fixa  
Para aprimorar a segurança, o Windows Server 2008, o [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)]e o Windows 7 ativam o Firewall do Windows. Para se conectar à esta instância a partir de outro computador, abra uma porta de comunicação no firewall. A instância padrão do [!INCLUDE[ssDE](../includes/ssde-md.md)] escuta na porta 1433; portanto, não é preciso configurar uma porta fixa. No entanto, instâncias nomeadas incluindo [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] escutam em portas dinâmicas. Antes de abrir uma porta no firewall, você deve primeiro configurar o [!INCLUDE[ssDE](../includes/ssde-md.md)] para escutar em uma porta específica conhecida como fixa ou estática; caso contrário, o [!INCLUDE[ssDE](../includes/ssde-md.md)] poderia escutar em uma porta diferente toda vez que fosse iniciado. Para obter mais informações sobre firewalls, as configurações padrão do Firewall do Windows e uma descrição das portas TCP que afetam o Mecanismo de Banco de Dados, o Analysis Services, o Reporting Services e o Integration Services, veja [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
> [!NOTE]  
> As atribuições de número da porta são gerenciadas pela Internet Assigned Numbers Authority e são listadas em [https://www.iana.org](https://go.microsoft.com/fwlink/?LinkId=48844). Os números de porta devem ser atribuídos de 49152 a 65535.  
  
#### <a name="configure-sql-server-to-listen-on-a-specific-port"></a>Configure o SQL Server para escutar em uma porta específica  
  
1.  No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager, expanda a **Configuração de Rede do SQL Server**e clique na instância de servidor que deseja configurar.  
  
2.  No painel direito, clique duas vezes em **TCP/IP**.  
  
3.  Na caixa de diálogo **Propriedades de TCP/IP** , clique na guia **Endereços IP** .  
  
4.  Na caixa **Porta TCP** da seção **IPAll** , digite um número de porta disponível. Para este tutorial, nós usaremos **49172**.  
  
5.  Clique em **OK** para fechar a caixa de diálogo e clique em **OK** no aviso de que o serviço deve ser reiniciado.  
  
6.  No painel esquerdo, clique em **Serviços do SQL Server**.  
  
7.  No painel direito, clique com o botão direito do mouse na instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]e clique em **Reiniciar**. Quando o [!INCLUDE[ssDE](../includes/ssde-md.md)] reiniciar, ele escutará na porta **49172**.  
  
## <a name="opening-ports-in-the-firewall"></a><a name="firewall"></a>Abrindo portas no Firewall  
Os sistemas de Firewall ajudam a impedir o acesso não autorizado aos recursos do computador. Para conectar-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a partir de outro computador quando um firewall estiver ativo, abra uma porta no firewall.  
  
> [!IMPORTANT]  
> A abertura de portas no firewall pode deixar o servidor exposto a ataques mal-intencionados. Certifique-se de que compreende os sistemas de firewall antes de abrir portas. Para obter mais informações, consulte [Security Considerations for a SQL Server Installation](../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
Após configurar o [!INCLUDE[ssDE](../includes/ssde-md.md)] para usar uma porta fixa, siga as instruções a seguir para abrir aquela porta em seu Firewall do Windows. (Não é necessário configurar uma porta fixa para a instância padrão, pois ela já é fixa na porta TCP 1433).  
  
#### <a name="to-open-a-port-in-the-windows-firewall-for-tcp-access-windows-7"></a>Para abrir uma porta no firewall do Windows para o acesso TCP (Windows 7)  
  
1.  No menu **Iniciar** , clique em **Executar**, digite **WF.msc**e clique em **OK**.  
  
2.  No painel esquerdo do **Firewall do Windows com Segurança Avançada**, clique com o botão direito do mouse em **Regras de Entrada**e clique em **Nova Regra** no painel de ação.  
  
3.  Na caixa de diálogo **Tipo de Regra** , selecione **Porta**e clique em **Avançar**.  
  
4.  Na caixa de diálogo **Protocolo e Portas** , selecione **TCP**. Selecione **Portas locais específicas**e digite o número da porta da instância do [!INCLUDE[ssDE](../includes/ssde-md.md)]. Digite 1433 para a instância padrão. Digite **49172** se você estiver configurando uma instância nomeada e tiver configurado uma porta fixa na tarefa anterior. Clique em **Próximo**.  
  
5.  Na caixa de diálogo **Ação**, selecione **Permitir a conexão** e clique em **Avançar**.  
  
6.  Na caixa de diálogo **Perfil** , selecione quaisquer perfis que descrevam o ambiente de conexão do computador quando você deseja se conectar ao [!INCLUDE[ssDE](../includes/ssde-md.md)]e clique em **Avançar**.  
  
7.  Na caixa de diálogo **Nome**, digite um nome e uma descrição para essa regra, e clique em **Concluir**.  
  
Para obter mais informações sobre como configurar o firewall incluindo instruções para o [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)], consulte [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md). Para obter mais informações sobre as configurações padrão do Firewall do Windows e uma descrição das portas TCP que afetam o Mecanismo de Banco de Dados, o Analysis Services, o Reporting Services e o Integration Services, veja [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
## <a name="connecting-to-the-database-engine-from-another-computer"></a><a name="otherComp"></a>Conectando-se ao Mecanismo de Banco de dados de outro computador  
Agora que você configurou o [!INCLUDE[ssDE](../includes/ssde-md.md)] para escutar em uma porta fixa, e abriu aquela porta no firewall, é possível se conectar ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de outro computador.  
  
Quando o serviço [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser estiver sendo executado no computador servidor, e quando o firewall abrir a porta 1434 do UDP , a conexão poderá ser feita com o nome do computador e o nome da instância. Para aumentar a segurança, nosso exemplo não usa o serviço [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser.  
  
#### <a name="to-connect-to-the-database-engine-from-another-computer"></a>Para conectar-se ao Mecanismo de Banco de Dados de outro computador  
  
1.  Em um segundo computador que contenha as ferramentas cliente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , faça o logon com uma conta autorizada para se conectar ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]e abra [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
2.  Na caixa de diálogo **Conectar ao Servidor** , confirme **Mecanismo de Banco de Dados** na caixa **Tipo de Servidor** .  
  
3.  Na caixa **Nome do Servidor** , digite **tcp:** para especificar o protocolo, seguido do nome do computador, uma vírgula e o número da porta. Para se conectar à instância padrão, a porta 1433 está implícita e pode ser omitida; portanto, digite **tcp:** _<computer_name>_ . Em nosso exemplo de uma instância nomeada, digite **tcp:** _<computer_name>_ **,49172**.  
  
    > [!NOTE]  
    > Se você omitir **tcp:** da caixa **Nome do servidor** , o cliente tentará todos os protocolos que estiverem habilitados, na ordem especificada na configuração do cliente.  
  
4.  Na caixa **Autenticação** , confirme **Autenticação do Windows**e clique em **Conectar**.  
  
## <a name="connecting-using-the-sql-server-browser-service"></a><a name="browser"></a>Conectando-se usando o SQL Server Browser Service  
O serviço Navegador do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reconhece solicitações de entrada dos recursos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e fornece informações sobre as instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instaladas no computador. Quando o serviço Navegador do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] estiver sendo executado, os usuários poderão se conectar a instâncias nomeadas fornecendo o nome do computador e o nome de instância, em vez do nome do computador e o número da porta. Como o Navegador do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] recebe solicitações UDP não autenticadas, ele não é sempre ativado durante a instalação. Para obter uma descrição do serviço e uma explicação de quando ele é ativado, consulte [Serviço SQL Server Browser &#40;Mecanismo de Banco de Dados e SSAS&#41;](../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md).  
  
Para usar o Navegador do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , siga as mesmas etapas anteriores e abra a porta UDP 1434 no firewall.  
  
Isso conclui esse breve tutorial em conectividade básica.  
  
## <a name="return-to-tutorials-portal"></a>Retorne ao portal Tutoriais  
[Tutorial: Introdução ao Mecanismo de Banco de Dados](../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
  

