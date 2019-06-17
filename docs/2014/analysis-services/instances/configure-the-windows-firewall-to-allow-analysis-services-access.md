---
title: Configurar o Firewall do Windows para permitir o acesso ao Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ports [Analysis Services]
- Windows Firewall [Analysis Services]
- firewall systems [Analysis Services]
ms.assetid: 7673acc5-75f0-4703-9ce2-87425ea39d49
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac7570550cd256a5c65c82c9585b2baf7713c878
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080266"
---
# <a name="configure-the-windows-firewall-to-allow-analysis-services-access"></a>Configurar o Firewall do Windows para permitir o acesso ao Analysis Services
  Uma primeira etapa essencial para tornar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] disponível na rede é determinar se você precisa desbloquear portas em um firewall A maioria das instalações exigirão que você crie, pelo menos, uma regra de firewall de entrada que permita conexões com o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Os requisitos de configuração de firewall variam de acordo com a maneira como você instalou o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Abra a porta TCP 2383 ao instalar uma instância padrão ou criar um cluster de failover do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
-   Abra a porta TCP 2382 ao instalar uma instância nomeada. Instâncias nomeadas usam atribuições de porta dinâmica. Da mesma maneira que o serviço de descoberta para o Analysis Services, o serviço SQL Server Browser escuta na porta TCP 2382 e redireciona a solicitação de conexão para a porta usada no momento pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Abra a porta TCP 2382 ao instalar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint para oferecer suporte ao [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013. No [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013, a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é externa ao SharePoint. As solicitações de entrada para a instância 'PowerPivot' nomeada originam-se de aplicativos Web do SharePoint em uma conexão de rede, exigindo uma porta aberta. Da mesma maneira que ocorre com outras instâncias nomeadas do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , crie uma regra de entrada para o serviço SQL Server Browser na porta TCP 2382 para permitir o acesso ao [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
-   Para o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010, não abra portas no Firewall do Windows. Da mesma maneira que ocorre com um suplemento do SharePoint, o serviço usa as portas configuradas para SharePoint e faz apenas conexões locais à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que carrega e consulta os modelos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
-   Para as instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] executadas em máquinas virtuais do Windows Azure, use instruções alternativas para configurar o acesso ao servidor. Consulte [SQL Server Business Intelligence em máquinas virtuais do Windows Azure](https://msdn.microsoft.com/library/windowsazure/jj992719.aspx).  
  
 Embora a instância padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] escuta na porta TCP 2383, você pode configurar o servidor para escutar em uma porta fixa diferente, conectando ao servidor neste formato: \<servername >:\<portnumber >.  
  
 Somente uma porta TCP pode ser usada por uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Em computadores com várias placas de rede ou vários endereços IP, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] escuta em uma porta TCP para todos os endereços IP atribuídos ou com alias para o computador. Se você tiver requisitos de várias portas específicas, é recomendável configurar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para acesso HTTP. Em seguida, você poderá configurar vários pontos de extremidade HTTP em qualquer porta escolhida. Consulte [Configurar o acesso HTTP ao Analysis Services no Serviços de Informações da Internet &#40;IIS&#41; 8.0](configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
 Este tópico contém as seguintes seções:  
  
-   [Verificar as configurações de porta e de firewall do Analysis Services](#bkmk_checkport)  
  
-   [Configurar o Firewall do Windows para uma instância padrão do Analysis Services](#bkmk_default)  
  
-   [Configurar o acesso ao Firewall do Windows para uma instância nomeada do Analysis Services](#bkmk_named)  
  
-   [Configuração de porta para um cluster do Analysis Services](#bkmk_cluster)  
  
-   [Configuração de porta do PowerPivot para SharePoint](#bkmk_powerpivot)  
  
-   [Usar uma porta fixa para uma instância padrão ou nomeada do Analysis Services](#bkmk_fixed)  
  
 Para obter mais informações sobre as configurações padrão do Firewall do Windows e uma descrição das portas TCP que afetam o Mecanismo de Banco de Dados, o Analysis Services, o Reporting Services e o Integration Services, veja [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
##  <a name="bkmk_checkport"></a> Verificar as configurações de porta e de firewall do Analysis Services  
 Nos sistemas operacionais Microsoft Windows com suporte pelo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o Windows Firewall fica ativo por padrão e bloqueia conexões remotas. Abra uma porta manualmente no firewall para permitir solicitações de entrada para o Analysis Services. A instalação do SQL Server não executa essa etapa para você.  
  
 As configurações de porta são especificadas no arquivo msmdsrv.ini e na página de propriedades Geral de uma instância do Analysis Services no SQL Server Management Studio. Se `Port` for definido como um inteiro positivo, o serviço estará escutando em uma porta fixa. Se `Port` for definido como 0, o serviço estará escutando na porta 2383 se for a instância padrão, ou em uma porta atribuída dinamicamente se for uma instância nomeada.  
  
 Atribuições de porta dinâmica só são usadas por instâncias nomeadas. O serviço `MSOLAP$InstanceName` determina a porta a ser usada quando inicia. Você pode determinar o número de porta real em uso por uma instância nomeada da seguinte forma:  
  
-   Inicie o Gerenciador de tarefas e, em seguida, clique em **Services** para obter o PID do `MSOLAP$InstanceName`.  
  
-   Execute `netstat -ao -p TCP` da linha de comando para exibir as informações de porta TCP para esse PID.  
  
-   Verifique se a porta usando o SQL Server Management Studio e conecte-se a um servidor do Analysis Services neste formato: \<Endereço IP >:\<portnumber >.  
  
 Embora um aplicativo possa escutar em uma porta específica, as conexões não terão êxito se um firewall estiver bloqueando o acesso. Para que conexões alcancem uma instância nomeada do Analysis Services, desbloqueie o acesso ao msmdsrv.exe ou à porta fixa na qual ele está escutando no firewall. As seções restantes neste tópico fornecem instruções para fazer isso.  
  
 Para verificar se as configurações de firewall já estão definidas para o Analysis Services, use o Firewall do Windows com a Segurança Avançada no Painel de controle. A página Firewall na pasta Monitoramento mostra uma lista completa das regras definidas para o servidor local.  
  
 Observe que para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], todas as regras de firewall devem ser definidas manualmente. Embora o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] and SQL Server Browser reservem as portas 2382 e 2383, o programa de instalação do SQL Server e as ferramentas de configuração não definem regras de firewall que permitam o acesso às portas ou aos arquivos executáveis de programa.  
  
##  <a name="bkmk_default"></a> Configurar o Firewall do Windows para uma instância padrão do Analysis Services  
 A instância padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] escuta na porta TCP 2383. Se você instalou a instância padrão e deseja usar esta porta, basta desbloquear o acesso de entrada à porta TCP 2383 no Firewall do Windows para habilitar o acesso remoto à instância padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Se você instalou a instância padrão mas deseja configurar o serviço para escutar em uma porta fixa, consulte [Usar uma porta fixa para uma instância padrão ou nomeada do Analysis Services](#bkmk_fixed) neste tópico.  
  
 Para verificar se o serviço está sendo executado como a instância padrão (MSSQLServerOLAPService), verifique o nome do serviço no Gerenciador de Configuração do SQL Server. Uma instância padrão do Analysis Services sempre é listada como o **SQL Server Analysis Services (MSSQLSERVER)** .  
  
> [!NOTE]  
>  Diferentes sistemas operacionais Windows oferecem ferramentas alternativas para configurar o Firewall do Windows. A maioria dessas ferramentas permitem optar entre abrir uma porta específica ou o programa executável. A menos que você tenha um motivo para especificar o programa executável, recomendamos que especifique a porta.  
  
 Ao especificar uma regra de entrada, procure adotar uma convenção de nomenclatura que lhe permita localizar facilmente as regras posteriormente (por exemplo, **SQL Server Analysis Services (TCP-in) 2383**).  
  
#### <a name="windows-firewall-with-advanced-security"></a>Firewall do Windows com Advanced Security  
  
1.  No Windows 7 ou Windows Vista, no Painel de Controle, clique em **Sistema e Segurança**, selecione **Firewall do Windows**e clique em **Configurações avançadas**. No Windows Server 2008 ou 2008 R2, abra Ferramentas do Administrador e clique em **Firewall do Windows com Segurança Avançada**. No Windows Server 2012, abra a página de aplicativos e digite **Windows Firewall**.  
  
2.  Clique com o botão direito do mouse em **Regras de Entrada** e selecione **Nova Regra**.  
  
3.  No tipo de regra, clique em `Port` e, em seguida, clique em **próxima**.  
  
4.  Em protocolo e portas, selecione **TCP** e, em seguida, digite `2383` na **portas locais específicas**.  
  
5.  Em Ação, clique em **Permitir a conexão** e em **Avançar**.  
  
6.  Em Perfil, desmarque os locais de rede que não se apliquem e clique em **Avançar**.  
  
7.  Em nome, digite um nome descritivo para esta regra (por exemplo, `SQL Server Analysis Services (tcp-in) 2383`) e, em seguida, clique em **concluir**.  
  
8.  Para verificar que conexões remotas são habilitadas, abra o SQL Server Management Studio ou o Excel em outro computador e conecte-se ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , especificando o nome de rede do servidor em **Nome do servidor**.  
  
    > [!NOTE]  
    >  Outros usuários não terão acesso a esse servidor até você conceder as devidas permissões. Para saber mais, veja [Autorizar o acesso a objetos e operações &#40;Analysis Services 41](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md).  
  
#### <a name="netsh-advfirewall-syntax"></a>Sintaxe de Netsh AdvFirewall  
  
-   O comando a seguir cria uma regra de entrada que permite solicitações de entrada na porta TCP 2383.  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Analysis Services inbound on TCP 2383" dir=in action=allow protocol=TCP localport=2383 profile=domain  
    ```  
  
##  <a name="bkmk_named"></a> Configurar o acesso ao Firewall do Windows para uma instância nomeada do Analysis Services  
 As instâncias nomeadas do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] podem escutar em uma porta fixa ou em uma porta dinamicamente atribuída, onde o serviço SQL Server Browser fornece as informações atuais de conexão ao serviço no momento da conexão.  
  
 O serviço SQL Server Browser escuta na porta TCP 2382. O UDP não é usado. O TCP é o único protocolo de transmissão usado pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Escolha uma das seguintes abordagens para habilitar o acesso remoto a uma instância nomeada do Analysis Services:  
  
-   Use as atribuições de porta dinâmica e o serviço SQL Server Browser. Desbloqueie a porta usada pelo serviço SQL Server Browser no Firewall do Windows. Conectar ao servidor neste formato: \<servername >\\< instancename\>.  
  
-   Use uma porta fixa e o serviço SQL Server Browser juntos. Essa abordagem permite que você se conectar usando este formato: \<servername >\\< instancename\>, idêntico à abordagem de atribuição de porta dinâmica, exceto que, nesse caso, o servidor escuta em uma porta fixa. Neste cenário, o serviço SQL Server Browser fornece a resolução de nome à instância do Analysis Services que escuta na porta fixa. Para usar esta abordagem, configure o servidor para escutar em uma porta fixa, desbloqueie o acesso a essa porta e desbloqueie o acesso à porta usada pelo serviço SQL Server Browser.  
  
 O serviço SQL Server Browser só é usado com instâncias nomeadas, nunca com a instância padrão. O serviço é instalado e habilitado automaticamente sempre que você instala qualquer recurso do SQL Server como uma instância nomeada. Se você optar por uma abordagem que exija o serviço SQL Server Browser, mantenha-o habilitado e iniciado no seu servidor.  
  
 Se você não puder usar o serviço SQL Server Browser, deverá atribuir uma porta fixa na cadeia de conexão, ignorando a resolução do nome de domínio. Sem o serviço SQL Server Browser, todas as conexões de cliente devem incluir o número da porta na cadeia de conexão (por exemplo, AW-SRV01: 54321).  
  
 **Opção 1: Use as atribuições de porta dinâmica e desbloqueie o acesso ao serviço navegador do SQL Server**  
  
 As atribuições de porta dinâmica para instâncias nomeadas do Analysis Services são estabelecidas pelo `MSOLAP$InstanceName` quando o serviço inicia. Por padrão, o serviço reivindica o primeiro número de porta disponível encontrado, usando um número de porta diferente cada vez que o serviço é reiniciado.  
  
 A resolução de nome de instância é tratada pelo serviço de SQL Server Browser. O desbloqueio da porta TCP 2382 para o serviço SQL Server Browser é sempre necessário quando você usa atribuições de porta dinâmica com uma instância nomeada.  
  
> [!NOTE]  
>  O serviço SQL Server Browser escuta na porta UDP 1434 e na porta TCP 2382 para o Mecanismo de Banco de Dados e o Analysis Services, respectivamente. Mesmo que você já tenha desbloqueado a porta UDP 1434 para o serviço SQL Server Browser, ainda precisará desbloquear a porta TCP 2382 para o Analysis Services.  
  
#### <a name="windows-firewall-with-advanced-security"></a>Firewall do Windows com Advanced Security  
  
1.  No Windows 7 ou Windows Vista, no Painel de Controle, clique em **Sistema e Segurança**, selecione **Firewall do Windows**e clique em **Configurações avançadas**. No Windows Server 2008 ou 2008 R2, abra Ferramentas do Administrador e clique em **Firewall do Windows com Segurança Avançada**. No Windows Server 2012, abra a página de aplicativos e digite **Windows Firewall**.  
  
2.  Para desbloquear o acesso ao serviço SQL Server Browser, clique com o botão direito do mouse em **Regras de Entrada** e selecione **Nova Regra**.  
  
3.  No tipo de regra, clique em `Port` e, em seguida, clique em **próxima**.  
  
4.  Em protocolo e portas, selecione **TCP** e, em seguida, digite `2382` na **portas locais específicas**.  
  
5.  Em Ação, clique em **Permitir a conexão** e em **Avançar**.  
  
6.  Em Perfil, desmarque os locais de rede que não se apliquem e clique em **Avançar**.  
  
7.  Em nome, digite um nome descritivo para esta regra (por exemplo, `SQL Server Browser Service (tcp-in) 2382`) e, em seguida, clique em **concluir**.  
  
8.  Para verificar que conexões remotas são habilitadas, abra o SQL Server Management Studio ou o Excel em outro computador e conecte-se ao Analysis Services, especificando o nome de rede do servidor e o nome da instância neste formato: \<servername > \\< instancename\>. Por exemplo, em um servidor nomeado **AW-SRV01** com uma instância nomeada de **Finanças**, o nome do servidor é **AW-SRV01\Finance**.  
  
 **Opção 2: Usar uma porta fixa para uma instância nomeada**  
  
 Outra alternativa é atribuir uma porta fixa e desbloquear o acesso a essa porta. Esta abordagem oferece um recurso melhor de auditoria quando você permite o acesso ao executável do programa. Por isso, o uso de uma porta fixa é a abordagem recomendada para acessar qualquer instância do Analysis Services.  
  
 Para atribuir uma porta fixa, siga as instruções em [Usar uma porta fixa para uma instância padrão ou nomeada do Analysis Services](#bkmk_fixed) neste tópico e, depois, volte a esta seção para desbloquear a porta.  
  
#### <a name="windows-firewall-with-advanced-security"></a>Firewall do Windows com Advanced Security  
  
1.  No Windows 7 ou Windows Vista, no Painel de Controle, clique em **Sistema e Segurança**, selecione **Firewall do Windows**e clique em **Configurações avançadas**. No Windows Server 2008 ou 2008 R2, abra Ferramentas do Administrador e clique em **Firewall do Windows com Segurança Avançada**. No Windows Server 2012, abra a página de aplicativos e digite **Windows Firewall**.  
  
2.  Para desbloquear o acesso ao Analysis Services, clique com o botão direito do mouse em **Regras de Entrada** e selecione **Nova Regra**.  
  
3.  No tipo de regra, clique em `Port` e, em seguida, clique em **próxima**.  
  
4.  Em Protocolo e Portas, selecione **TCP** e digite a porta fixa em **Portas locais específicas**.  
  
5.  Em Ação, clique em **Permitir a conexão** e em **Avançar**.  
  
6.  Em Perfil, desmarque os locais de rede que não se apliquem e clique em **Avançar**.  
  
7.  Em nome, digite um nome descritivo para esta regra (por exemplo, `SQL Server Analysis Services on port 54321`) e, em seguida, clique em **concluir**.  
  
8.  Para verificar que conexões remotas são habilitadas, abra o SQL Server Management Studio ou o Excel em outro computador e conecte-se ao Analysis Services, especificando o nome de rede do servidor e o número da porta neste formato: \<servername >: \<portnumber >.  
  
#### <a name="netsh-advfirewall-syntax"></a>Sintaxe de Netsh AdvFirewall  
  
-   Os comandos a seguir criam as regras de entrada que desbloqueiam o TCP 2382 para o serviço SQL Server Browser e desbloqueiam a porta fixa especificada para a instância do Analysis Services. Você pode executar qualquer um dos dois para permitir o acesso a uma instância do Analysis Services nomeada.  
  
     Neste comando de exemplo, a porta 54321 é a porta fixa. Substitua-a pela porta real em uso no seu sistema.  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Analysis Services (tcp-in) on 54321" dir=in action=allow protocol=TCP localport=54321 profile=domain  
    ```  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Browser Services inbound on TCP 2382" dir=in action=allow protocol=TCP localport=2382 profile=domain  
    ```  
  
##  <a name="bkmk_fixed"></a> Usar uma porta fixa para uma instância padrão ou nomeada do Analysis Services  
 Esta seção explica como configurar o Analysis Services para escutar em uma porta fixa. O uso de uma porta fixa é comum quando você instala o Analysis Services como uma instância nomeada, mas você também pode usar esta abordagem quando os requisitos de negócios ou de segurança especificam o uso de atribuições de porta não padrão.  
  
 Observe que o uso de uma porta fixa alterará a sintaxe de conexão para a instância padrão, exigindo o acréscimo do número de porta ao nome de servidor. Por exemplo, a conexão a uma instância padrão local do Analysis Services que escuta na porta 54321 no SQL Server Management Studio exigiria que você digitasse localhost:54321 como o nome de servidor na caixa de diálogo Conectar ao Servidor no Management Studio.  
  
 Se você estiver usando uma instância nomeada, você pode atribuir uma porta fixa sem alterações sobre como especificar o nome do servidor (especificamente, você pode usar \<nome_do_servidor \ nome_da_instância > para se conectar a uma instância nomeada escuta em uma porta fixa). Isso só funcionará se o serviço SQL Server Browser estiver em execução e você tiver desbloqueado a porta na qual ele esteja escutando. Serviço SQL Server Browser fornecerá redirecionamento à porta fixa com base em \<nome_do_servidor \ nome_da_instância >. Contanto que você abra portas para o serviço SQL Server Browser e a instância nomeada do Analysis Services que escuta na porta fixa, o serviço SQL Server Browser resolverá a conexão a uma instância nomeada.  
  
1.  Determine uma porta TCP/IP disponível a ser usada.  
  
     Para exibir uma lista de portas reservadas e registradas que você deve evitar usar, consulte [Port Numbers (IANA)](https://go.microsoft.com/fwlink/?LinkID=198469)(página em inglês). Para exibir uma lista de portas que já estão em uso em seu sistema, abra uma janela de prompt de comando e digite `netstat -a -p TCP` para exibir uma lista de portas TCP que estão abertas no sistema.  
  
2.  Após determinar a porta a ser usada, especifique a porta editando a configuração de `Port` no arquivo msmdsrv.ini ou na página de propriedades Geral de uma instância do Analysis Services no SQL Server Management Studio.  
  
3.  Reinicie o serviço.  
  
4.  Configure o Firewall do Windows para desbloquear a porta TCP especificada. Ou, se você estiver usando uma porta fixa para uma instância nomeada, desbloqueie a porta TCP especificada para essa instância e a porta TCP 2382 para o serviço SQL Server Browser.  
  
5.  Verifique isso conectando-se localmente (no Management Studio) e, em seguida, remotamente, de um aplicativo cliente em outro computador. Para usar o Management Studio, conecte-se à instância padrão do Analysis Services especificando um nome de servidor neste formato: \<servername >:\<portnumber >. Para uma instância nomeada, especifique o nome do servidor como \<servername >\\< instancename\>.  
  
##  <a name="bkmk_cluster"></a> Configuração de porta para um cluster do Analysis Services  
 Um cluster de failover do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sempre realiza a escuta na porta TCP 2383, independentemente de você ter feito a instalação como uma instância padrão ou nomeada. As atribuições de porta dinâmica não são usadas pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quando ele é instalado em um cluster de failover do Windows. Abra a TCP 2383 em todos os nós que estão executando o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no cluster. Para obter mais informações sobre o clustering do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Como clusterizar o SQL Server Analysis Services](https://go.microsoft.com/fwlink/p/?LinkId=396548).  
  
##  <a name="bkmk_powerpivot"></a> Configuração de porta do PowerPivot para SharePoint  
 A arquitetura de servidor para o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] é bem diferente dependendo da versão do SharePoint que você está usando.  
  
 **SharePoint 2013**  
  
 No SharePoint 2013, os Serviços do Excel redirecionam solicitações para modelos de dados do PowerPivot, que são carregados subsequentemente em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fora do ambiente do SharePoint. As conexões seguem o padrão comum, onde uma biblioteca de cliente do Analysis Services em um computador local envia uma solicitação de conexão a uma instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na mesma rede.  
  
 Como o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] sempre instala o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como uma instância nomeada, você deverá supor o serviço SQL Server Browser e as atribuições de porta dinâmica. Como observado anteriormente, o serviço SQL Server Browser escuta na porta TCP 2382 para as solicitações de conexão enviadas às instâncias nomeadas do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , redirecionando a solicitação para a porta atual.  
  
 Observe que os Serviços do Excel no SharePoint 2013 não oferecem suporte à sintaxe de conexão de porta fixa, portanto, verifique se o serviço SQL Server Browser está acessível.  
  
 **SharePoint 2010**  
  
 Se você estiver usando o SharePoint 2010, não precisa abrir portas no Firewall do Windows. O SharePoint abre as portas necessárias e os suplementos como o PowerPivot para SharePoint funcionam no ambiente do SharePoint. Em uma instalação do PowerPivot para SharePoint 2010, o Serviço de Sistema PowerPivot tem uso exclusivo da instância de serviço local do SQL Server Analysis Services (PowerPivot) que é instalada com ele no mesmo computador. Ele usa conexões locais, e não de rede, para acessar o serviço de mecanismo local Analysis Services que carrega, consulta e processa dados PowerPivot no servidor do SharePoint. Para solicitar dados do PowerPivot de aplicativos cliente, as solicitações são roteadas por meio de portas que são abertas pela instalação do SharePoint (especificamente, as regras de entrada são definidas para permitir o acesso ao SharePoint - 80, Administração Central do SharePoint v4, serviços Web do SharePoint e SPUserCodeV4). Como os serviços Web PowerPivot são executados em um farm do SharePoint, as regras de firewall do SharePoint são suficientes para o acesso remoto a dados PowerPivot em um farm do SharePoint.  
  
## <a name="see-also"></a>Consulte também  
 [Serviço SQL Server Browser &#40;Mecanismo de Banco de Dados e SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)   
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)   
 [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
  
