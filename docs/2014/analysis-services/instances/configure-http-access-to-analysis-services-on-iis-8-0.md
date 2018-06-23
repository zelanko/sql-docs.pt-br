---
title: Configurar o acesso HTTP ao Analysis Services nos serviços de informações da Internet (IIS) 8.0 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cf2e2c84-0a69-4cdd-90a1-fb4021936513
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b394ce90c7629da5f52034570b2cc71451db036d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117548"
---
# <a name="configure-http-access-to-analysis-services-on-internet-information-services-iis-80"></a>Configurar o acesso HTTP ao Analysis Services no IIS (Serviços de Informações da Internet) 8.0
  Este artigo explica como configurar um ponto de extremidade HTTP para acessar uma instância do Analysis Services. É possível habilitar o acesso HTTP configurando o MSMDPUMP.dll, uma extensão de ISAPI que é executada no IIS (Serviços de Informações da Internet) e que bombeia dados entre os aplicativos cliente e um servidor do Analysis Services. Esta abordagem oferece um meio alternativo de se conectar ao Analysis Services quando sua solução de BI requer os seguintes recursos:  
  
-   O acesso de cliente está em conexões via Internet ou extranet, com restrições quanto às portas a serem habilitadas.  
  
-   As conexões de cliente são provenientes de domínios não confiáveis na mesma rede.  
  
-   O aplicativo cliente é executado em um ambiente de rede que permite conexões HTTP, mas não TCP/IP.  
  
-   Os aplicativos cliente não podem usar as bibliotecas de cliente do Analysis Services (por exemplo, um aplicativo Java executado em um servidor UNIX). Se você não puder usar as bibliotecas de cliente do Analysis Services para acessar dados, poderá usar o SOAP e o XML/A em uma conexão HTTP direta a uma instância do Analysis Services.  
  
-   São necessários métodos de autenticação que não sejam a segurança integrada do Windows. Especificamente, você pode usar conexões anônimas e a autenticação Básica ao configurar o Analysis Services para acesso HTTP. Não há suporte para a autenticação Digest, de formulário e ASP.NET. Um requisito de autenticação Básica é um dos principais motivos para permitir o acesso HTTP. Para saber mais, consulte [Autenticação e delegação de identidade do Microsoft BI](http://go.microsoft.com/fwlink/?LinkId=286576).  
  
 É possível configurar o acesso HTTP para qualquer versão com suporte ou edição do Analysis Services, em execução em modo de tabela ou multidimensional. Cubos locais são uma exceção. Não é possível conectar-se a um cubo local por meio de um ponto de extremidade HTTP.  
  
 Configurar o acesso HTTP é uma tarefa pós-instalação. O Analysis Services deve ser instalado antes de ser configurado para o acesso HTTP. Como administrador do Analysis Services, será preciso conceder permissões para contas do Windows para que o acesso HTTP seja possível. Além disso, é uma prática recomendada validar a instalação primeiro, assegurando que ela esteja totalmente operacional antes de configurar qualquer servidor adicional. Após a configuração do acesso HTTP, é possível utilizar o ponto de extremidade HTTP e o nome da rede regular do servidor sobre TCP/IP. Configurar o acesso HTTP não invalida outras abordagens para acesso de dados.  
  
 À medida que avançar com a configuração MSMDPUMP, lembre-se que há duas conexões a serem consideradas: cliente para IIS, IIS para SSAS. As instruções neste artigo são sobre o IIS para SSAS. O aplicativo cliente pode exigir configuração adicional antes que ele possa se conectar ao IIS. Decisões sobre como configurar as associações ou se você deseja utilizar o SSL, estão fora do escopo deste artigo. Veja [servidor Web (IIS)](http://technet.microsoft.com/library/hh831725.aspx) para obter mais informações sobre o IIS.  
  
 Este tópico inclui as seguintes seções:  
  
-   [Visão geral](#bkmk_overview)  
  
-   [Pré-requisitos](#bkmk_prereq)  
  
-   [Copiar o MSMDPUMP.dll em uma pasta no servidor Web.](#bkmk_copy)  
  
-   [Criar um pool de aplicativos e um diretório virtual no IIS](#bkmk_appPool)  
  
-   [Configurar a autenticação de IIS e adicionar a extensão](#bkmk_auth)  
  
-   [Editar o arquivo MSMDPUMP.INI para definir o servidor de destino](#bkmk_edit)  
  
-   [Testar sua configuração](#bkmk_test)  
  
##  <a name="bkmk_overview"></a> Visão geral  
 O MSMDPUMP é uma extensão ISAPI que pode ser carregada no IIS e que fornece redirecionamento para uma instância do Analysis Services local ou remota. Ao configurar essa extensão ISAPI, você cria um ponto de extremidade HTTP para uma instância do Analysis Services.  
  
 Você deve criar e configurar um diretório virtual para cada ponto de extremidade HTTP. Cada ponto de extremidade precisará ter seu próprio conjunto de arquivos MSMDPUMP, para cada instância do Analysis Services à qual você deseja se conectar. Um arquivo de configuração nesse conjunto de arquivos especifica o nome da instância do Analysis Services usado para cada ponto de extremidade HTTP.  
  
 No IIS, o MSMDPUMP se conecta ao Analysis Services usando o provedor OLE DB do Analysis Services no TCP/IP. Embora as solicitações de clientes possam se originar fora da confiabilidade do domínio, o Analysis Services e o IIS devem estar no mesmo domínio ou em domínios confiáveis para que a conexão nativa tenha êxito.  
  
 Quando o MSMDPUMP se conecta ao Analysis Services, ele utiliza uma identidade de usuário do Windows. Esta conta será a conta Anônima se você tiver configurado o diretório virtual para conexões anônimas, ou uma conta de usuário do Windows. A conta deve ter os direitos de acesso a dados apropriados no servidor e banco de dados do Analysis Services.  
  
 ![Diagrama que mostra conexões entre componentes](../media/ssas.gif "diagrama mostrando conexões entre componentes")  
  
 A tabela a seguir lista considerações adicionais quando você habilita o acesso de HTTP para cenários diferentes.  
  
|Cenário|Configuração|  
|--------------|-------------------|  
|O IIS e o Analysis Services no mesmo computador|Esta é a configuração mais simples porque permite usar a configuração padrão (onde o nome de servidor é localhost), o provedor local OLE DB do Analysis Services e a segurança avançada do Windows com NTLM. Assumindo que o cliente também está no mesmo domínio, a autenticação será transparente para o usuário, sem trabalho adicional de sua parte.|  
|O IIS e o Analysis Services em computadores diferentes|Para esta topologia, instale o provedor OLE DB do Analysis Services no servidor Web. Você também precisa editar o arquivo msmdpump.ini para especificar o local da instância do Analysis Services no computador remoto.<br /><br /> Esta topologia adiciona uma etapa de autenticação de salto duplo, em que credenciais devem fluir do cliente para o servidor Web, e para o servidor back-end do Analysis Services. Se você estiver usando credenciais do Windows e o NTLM, obterá um erro porque o NTLM não permite a delegação de credenciais de cliente a um segundo servidor. A solução mais comum é usar a autenticação Básica com o protocolo SSL, mas isso exige que usuários forneçam um nome de usuário e uma senha quando acessam o diretório virtual de MSMDPUMP. Uma abordagem mais simples poderia ser a habilitação do Kerberos e a configuração da delegação restrita do Analysis Services para permitir que usuários acessem o Analysis Services de forma transparente. Para obter detalhes, consulte [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md) .<br /><br /> Avalie quais portas devem ser desbloqueadas no Firewall do Windows. Você precisará desbloquear portas em ambos os servidores para permitir o acesso ao aplicativo Web no IIS, e ao Analysis Services em um servidor remoto.|  
|Conexões de cliente são de um domínio não confiável ou de uma conexão de extranet|Conexões de cliente de um domínio não confiável apresentam restrições adicionais na autenticação. Por padrão, o Analysis Services utiliza a autenticação integrada do Windows; ela exige que os usuários estejam no mesmo domínio que o servidor. Se você tiver usuários de Extranet que se conectam ao IIS de fora do domínio, esses usuários obterão um erro de conexão se o servidor for configurado para usar as configurações padrão.<br /><br /> Soluções alternativas incluem a conexão de usuários Extranet através de um VPN usando credenciais de domínio. Porém, talvez melhor opção seja habilitar a autenticação Básica e o SSL em seu site do IIS.|  
  
##  <a name="bkmk_prereq"></a> Pré-requisitos  
 As instruções neste artigo presumem que o IIS já está configurado e que o Analysis Services já está instalado. O Windows Server 2012 é fornecido com o IIS 8.x como uma função de servidor que pode ser habilitada no sistema.  
  
 **Configuração adicional no IIS 8.0**  
  
 Na configuração padrão do IIS 8.0 estão faltando componentes necessários para o acesso HTTP ao Analysis Services. Esses componentes, encontrados nas áreas de recursos **Segurança** e **Desenvolvimento de aplicativos** da função **servidor Web (IIS)** , incluem o seguinte:  
  
-   **Segurança** | **Autenticação do Windows**ou **Autenticação Básica**e outros recursos de segurança necessários para seu cenário de acesso de dados.  
  
-   **Desenvolvimento de Aplicativos** | **CGI**  
  
-   **Desenvolvimento de aplicativos** | **Extensões ISAPI**  
  
 Para verificar ou adicionar esses componentes, use **Gerenciador do Servidor** | **Gerenciar** | **Adicionar Funções e Recursos**. Percorrer o assistente até chegar nas **Funções de servidor**. Role para baixo até localizar o **Servidor Web (IIS)**.  
  
1.  Abra **Servidor Web** | **Segurança** e escolha os métodos de autenticação.  
  
2.  Abra **Servidor Web** | **Desenvolvimento de aplicativos** e escolha **CGI** e **Extensões ISAPI**.  
  
     ![Página Adicionar recursos para a função de servidor Web](../media/ssas-httpaccess-isapicgi.png "página Adicionar recursos para a função de servidor Web")  
  
 **Quando o IIS está em um servidor remoto**  
  
 Uma conexão remota entre o IIS e o Analysis Services exige a instalação do provedor OLE DB do Analysis Services (MSOLAP) no Windows server executando o IIS.  
  
1.  Vá para a página de download do [Feature Pack do SQL Server 2014](http://www.microsoft.com/download/details.aspx?id=42295)  
  
2.  Clique no botão Baixar.  
  
3.  Role para baixo para encontrar ENU\x64\SQL_AS_OLEDB.msi  
  
4.  Siga as instruções no assistente para concluir a instalação.  
  
> [!NOTE]  
>  Lembre-se de desbloquear as portas no Firewall do Windows para permitir conexões de cliente a um servidor remoto do Analysis Services. Para obter mais informações, consulte [Configure the Windows Firewall to Allow Analysis Services Access](configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
##  <a name="bkmk_copy"></a> Etapa 1: Copiar os arquivos MSMDPUMP para uma pasta no servidor Web.  
 Cada ponto de extremidade HTTP criado deve ter seu próprio conjunto de arquivos MSMDPUMP. Nesta etapa, você copia o executável do MSMDPUMP, o arquivo de configuração e os arquivos de recurso das pastas de programas do Analysis Services para uma nova pasta de diretório virtual que será criada no sistema de arquivos do computador que está executando o IIS.  
  
 A unidade deve ser formatada para o sistema de arquivos NTFS. O caminho para a pasta que você cria não deve conter espaços.  
  
1.  Copie os seguintes arquivos, encontrados em \<unidade >: \Program Files\Microsoft do SQL Server\\< instância\>\OLAP\bin\isapi: MSMDPUMP. DLL, MSMDPUMP. INI e uma pasta recursos.  
  
     ![Explorador de arquivos mostrando arquivos para copiar](../media/ssas-httpaccess-msmdpumpfilecopy.PNG "Explorador de arquivos mostrando arquivos para copiar")  
  
2.  No servidor web, crie uma nova pasta: \<unidade >: \inetpub\wwwroot\\**OLAP**  
  
3.  Cole os arquivos que você copiou anteriormente para essa nova pasta.  
  
4.  Verifique se a pasta \inetpub\wwwroot\OLAP no servidor Web contém o seguinte: MSMDPUMP.DLL, MSMDPUMP.INI e uma pasta Resources. A estrutura de pastas devem ter a seguinte aparência:  
  
    -   \<drive>:\inetpub\wwwroot\OLAP\MSMDPUMP.dll  
  
    -   \<drive>:\inetpub\wwwroot\OLAP\MSMDPUMP.ini  
  
    -   \<unidade >: \inetpub\wwwroot\OLAP\Resources  
  
##  <a name="bkmk_appPool"></a> Etapa 2: Criar um pool de aplicativos e um diretório virtual no IIS  
 Em seguida, crie um pool de aplicativos e um ponto de extremidade para a bomba.  
  
#### <a name="create-an-application-pool"></a>Criar um pool de aplicativos  
  
1.  Inicie o Gerenciador IIS.  
  
2.  Abra a pasta do servidor, clique com o botão direito do mouse em **Pools de Aplicativos** e clique em **Adicionar Pool de Aplicativos**. Crie um pool de aplicativos denominado **OLAP**, utilizando o .NET Framework, com o modo de pipeline Gerenciado definido como **Clássico**.  
  
     ![Caixa de diálogo de captura de tela de Adicionar Pool de aplicativos](../media/ssas-httpaccess.PNG "caixa de diálogo de captura de tela de Adicionar Pool de aplicativos")  
  
3.  Por padrão, o IIS cria pools de aplicativos utilizando **ApplicationPoolIdentity** como a identidade de segurança, que é uma opção válida para o acesso HTTP ao Analysis Services. Se houver motivos específicos para alterar a identidade, clique com o botão direito do mouse em **OLAP**e, em seguida, selecione **Configurações avançadas**. Selecione **ApplicationPoolIdentity**. Clique no botão **Alterar** para que esta propriedade substitua a conta interna pela conta personalizada a ser usada.  
  
     ![Página de propriedade de captura de tela de configurações avançadas](../media/ssas-httpaccess-advsettings.PNG "página de propriedade de captura de tela de configurações avançadas")  
  
4.  Por padrão, em um sistema operacional de 64 bits, o IIS define a propriedade **Enable 32-bit Applications** como **false**. Se você copiou msmdpump.dll de uma instalação de 64 bits do Analysis Services, esta será a configuração correta para a extensão MSMDPUMP em um servidor IIS de 64 bits. Se você copiou os binários de MSMDPUMP de uma instalação de 32 bits, defina-a como **true**. Verifique se agora a propriedade em **Configurações avançadas** foi definida corretamente.  
  
#### <a name="create-an-application"></a>Criar um aplicativo  
  
1.  No Gerenciador do IIS, abra **Sites**, depois abra **Site Padrão**. Você verá uma pasta chamada **Olap**. Essa é uma referência à pasta OLAP criada em \inetpub\wwwroot.  
  
     ![Pasta OLAP no site da web padrão](../media/ssas-httpaccess-convertfolderbefore.png "pasta OLAP no site da web padrão")  
  
2.  Clique com o botão direito do mouse na pasta e escolha **Converter em aplicativo**.  
  
3.  Em Adicionar aplicativo, digite **OLAP** para o alias. Clique em **Selecionar** para escolher o pool de aplicativos OLAP. O caminho físico deve ser definido como C:\inetpub\wwwroot\OLAP  
  
     ![Caixa de diálogo Adicionar aplicativo](../media/ssas-httpaccess-convertedapp.png "caixa de diálogo Adicionar aplicativo")  
  
4.  Clique em **OK**. Atualize o site e observe que a pasta OLAP agora é um aplicativo no Site Padrão. O caminho virtual para o arquivo MSMDPUMP agora está estabelecido.  
  
     ![Pasta OLAP após a conversão do aplicativo](../media/ssas-httpaccess-convertfolderafter.png "pasta OLAP após a conversão do aplicativo")  
  
> [!NOTE]  
>  Versões anteriores dessas instruções incluíam etapas para criar um diretório virtual. Essa etapa não é mais necessária.  
  
##  <a name="bkmk_auth"></a> Etapa 3: Configurar a autenticação do IIS e adicionar a extensão  
 Nesta etapa, você configura mais o diretório virtual do SSAS recém-criado. Você especificará um método de autenticação e depois adicionará um mapa de script. Estes são métodos de autenticação com suporte para o Analysis Services sobre HTTP:  
  
-   Autenticação do Windows (Kerberos ou NTLM)  
  
-   Autenticação Básica  
  
-   Autenticação anônima  
  
 A**Autenticação do Windows** é considerada a alternativa mais segura, e aproveita a infraestrutura existente das redes que usam o Active Directory. Para usar a autenticação do Windows com eficiência, todos os navegadores, aplicativos cliente e aplicativos de servidor devem oferecer suporte a ela. Esse é o modo mais seguro e recomendado, mas requer que o IIS acesse um controlador de domínio do Windows que possa autenticar a identidade do usuário que está solicitando uma conexão.  
  
 Nas topologias que colocam o Analysis Services e o IIS em computadores diferentes, você precisará solucionar os problemas de salto duplo que ocorrem quando uma identidade de usuário precisa ser delegada a um segundo serviço em um computador remoto, normalmente habilitando o Analysis Services para delegação restrita de Kerberos. Para obter mais informações, consulte [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md).  
  
 A**Autenticação Básica** é usada quando você tem identidades do Windows, mas as conexões de usuário são provenientes de domínios não confiáveis, proibindo o uso de conexões representadas ou delegadas. A autenticação Básica permite especificar uma identidade de usuário e uma senha em uma cadeia de conexão. Em vez de usar o contexto de segurança do usuário atual, as credenciais na cadeia de conexão são usadas para estabelecer a conexão com o Analysis Services. Como o Analysis Services oferece suporte apenas à autenticação do Windows, quaisquer credenciais passadas para ele devem ser um usuário ou grupo do Windows que seja membro do domínio em que o Analysis Services está hospedado.  
  
 A**Autenticação anônima** é frequentemente usada durante o teste inicial porque a facilidade de configuração ajuda a validar rapidamente a conectividade HTTP com o Analysis Services. Em apenas algumas etapas, você pode atribuir uma conta de usuário exclusiva como identidade, conceder essas permissões de conta no Analysis Services, usar a conta para verificar o acesso aos dados em um aplicativo cliente e, em seguida, desabilitar a autenticação Anônima quando o teste for concluído.  
  
 Você também poderá usar a autenticação Anônima em um ambiente de produção se os usuários não tiverem contas de usuário do Windows, mas siga as práticas recomendadas bloqueando as permissões no sistema host, conforme destacado neste artigo: [Habilitar a autenticação Anônima (IIS 7)](http://technet.microsoft.com/library/cc731244\(v=ws.10\).aspx). Verifique se a autenticação está definida no diretório virtual, e não no site pai, a fim de reduzir ainda mais o nível da conta de acesso.  
  
 Quando a opção Anônima for habilitada, qualquer conexão de usuário com o ponto de extremidade HTTP será permitida como usuário anônimo. Não será possível fazer a auditoria de cada conexão de usuário nem usar a identidade do usuário para selecionar dados em um modelo. Como você pode ver, o uso da opção Anônima impacta tudo, do modelo de design ao acesso e à atualização dos dados. No entanto, se os usuários não tiverem um logon de usuário do Windows para começar, o uso da conta Anônima talvez seja sua única opção.  
  
#### <a name="set-the-authentication-type-and-add-a-script-map"></a>Definir o tipo de autenticação e adicionar um mapa de script  
  
1.  No Gerenciador do IIS, abra **Sites**, abra **Site Padrão da Web**e selecione o diretório virtual **OLAP** .  
  
2.  Clique duas vezes em **Autenticação** na seção de IIS da página principal.  
  
     ![Página principal da captura de tela do Gerenciador do IIS](../media/ssas-httpaccess-iis.png "página principal da captura de tela do Gerenciador do IIS")  
  
3.  Habilite **Autenticação do Windows** se estiver usando a segurança integrada do Windows.  
  
     ![Configurações de captura de tela de autenticação de Vdir](../media/ssas-httpaccess-iisauth.png "configurações de captura de tela de autenticação de Vdir")  
  
4.  Se desejar, habilite **Autenticação Básica** se os aplicativos cliente e de servidor estiverem em domínios diferentes. Este modo exige que o usuário insira um nome de usuário e uma senha. O nome de usuário e a senha são transmitidos na conexão HTTP para IIS. O IIS tentará representar o usuário usando as credenciais fornecidas ao conectar-se ao MSMDPUMP, mas as credenciais não serão delegadas ao Analysis Services. Em vez disso, você precisará passar um nome de usuário e uma senha válidos em uma conexão, conforme descrito na Etapa 6 deste documento.  
  
    > [!IMPORTANT]  
    >  Observe que é imperativo para qualquer pessoa que esteja compilando um sistema onde a senha é transmitida que encontre formas de proteger o canal de comunicação. O IIS fornece um conjunto de ferramentas que o ajudam a proteger o canal. Para obter mais informações, consulte [Como configurar o SSL no IIS 7](http://go.microsoft.com/fwlink/?LinkId=207562).  
  
5.  Desabilite **Autenticação Anônima** se estiver usando a autenticação Básica ou do Windows. Quando a autenticação Anônima for habilitada, o IIS sempre a usará primeiro, mesmo se outros métodos de autenticação estiverem habilitados.  
  
     Na autenticação Anônima, a bomba (msmdpump.dll) é executada como a conta de usuário estabelecida para o usuário anônimo. Não há distinção entre o usuário que está se conectando o IIS e o usuário que está se conectando ao Analysis Services. Por padrão, o IIS usa a conta IUSR, mas é possível transformá-la em uma conta de usuário de domínio que tenha permissões de rede. Você precisará desse recurso se o IIS e o Analysis Services estiverem em computadores diferentes.  
  
     Para obter instruções sobre como configurar credenciais para a autenticação Anônima, consulte [Autenticação Anônima](http://www.iis.net/configreference/system.webserver/security/authentication/anonymousauthentication).  
  
    > [!IMPORTANT]  
    >  A autenticação Anônima é mais utilizada em um ambiente extremamente controlado, onde o acesso é concedido ou negado aos usuários através de listas de controle de acesso no sistema de arquivos. Para obter as práticas recomendadas, veja [Habilitar a autenticação Anônima (IIS 7)](http://technet.microsoft.com/library/cc731244\(v=ws.10\).aspx).  
  
6.  Clique no diretório virtual **OLAP** para abrir a página principal. Clique duas vezes em **Mapeamentos do Manipulador**.  
  
     ![Ícone de mapeamento de manipulador na página do recurso](../media/ssas-httpaccess-handlermapping.png "ícone de mapeamento de manipulador na página de recursos")  
  
7.  Clique com o botão direito do mouse em qualquer ponto da página e selecione **Adicionar Mapa de Script**. Na caixa de diálogo Adicionar Mapa de Script, especifique **\*.dll** como o caminho de solicitação, especifique c:\inetpub\wwwroot\OLAP\msmdpump.dll como o executável e digite **OLAP** como o nome. Mantenha todas as restrições padrão associadas a esse mapa de script.  
  
     ![Caixa de diálogo de captura de tela de adicionar mapa de Script](../media/ssas-httpaccess-addscript.png "caixa de diálogo de captura de tela de adicionar mapa de Script")  
  
8.  Quando for solicitado a permitir a extensão ISAPI, clique em **Sim**.  
  
     ![Captura de tela de confirmação para adicionar a extensão ISAPI](../media/ssas-httpaccess-isapiprompt.png "captura de tela de confirmação para adicionar a extensão ISAPI")  
  
##  <a name="bkmk_edit"></a> Etapa 4: Editar o arquivo MSMDPUMP.INI para definir o servidor de destino  
 O arquivo MSMDPUMP.INI especifica a instância do Analysis Services ao qual o MSMDPUMP.DLL se conecta. A instância pode ser local ou remota, instalada como padrão ou como uma instância nomeada.  
  
 Abra o arquivo msmdpump.ini localizado na pasta C:\inetpub\wwwroot\OLAP e verifique o conteúdo desse arquivo. Ele deve ter esta aparência:  
  
```  
<ConfigurationSettings>  
<ServerName>localhost</ServerName>  
<SessionTimeout>3600</SessionTimeout>  
<ConnectionPoolSize>100</ConnectionPoolSize>  
</ConfigurationSettings>  
  
```  
  
 Se a instância do Analysis Services para a qual você está configurando o acesso de HTTP estiver localizada no computador local e instala como uma instância padrão, não haverá razão para alterar esta configuração. Caso contrário, você deve especificar o nome do servidor (por exemplo, \<ServerName > ADWRKS-SRV01\</ServerName >). Para um servidor que é instalado como uma instância nomeada, certifique-se de acrescentar o nome da instância (por exemplo, \<ServerName > ADWRKS-SRV01\Tabular\</ServerName >).  
  
 Por padrão, o Analysis Services escuta na porta TCP/IP 2383. Se você instalou o Analysis Services como a instância padrão, você não precisa especificar uma porta em \<ServerName > porque o Analysis Services sabe escutar na porta 2383 automaticamente. Porém, você precisa permitir conexões de entrada a essa porta no Firewall do Windows. Para obter mais informações, consulte [Configure the Windows Firewall to Allow Analysis Services Access](configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
 Se configurado um conjunto nomeado ou padrão a instância do Analysis Services para escutar em uma porta fixa, você deve adicionar o número da porta ao nome do servidor (por exemplo, \<nomedoservidor > AW-Srv01: 55555\</ServerName >) e você deve permitir entrada conexões no Firewall do Windows para essa porta.  
  
## <a name="step-5-grant-data-access-permissions"></a>Etapa 5: Conceder permissões de acesso a dados  
 Como mencionado anteriormente, será preciso conceder permissões à instância do Analysis Services. Cada objeto de banco de dados terá funções que fornecem um nível específico de permissões (leitura ou leitura/gravação), e cada função terá os membros que consistem em identidades de usuário do Windows.  
  
 Para definir permissões, você pode usar o SQL Server Management Studio. Na pasta **Banco de dados** | **Funções** , você pode criar funções, especificar permissões de banco de dados, atribuir a associação às contas de grupo ou de usuário do Windows e conceder permissões de leitura ou gravação em objetos específicos. Normalmente, as permissões de **Leitura** em um cubo são suficientes para as conexões de cliente que usam, mas não atualizam, dados do modelo.  
  
 A atribuição de função varia dependendo de como você configurou a autenticação.  
  
|||  
|-|-|  
|Anônima|Adicione, à lista de associações, a conta especificada em **Editar Credenciais de Autenticação Anônima** no IIS. Para obter mais informações, consulte [Autenticação Anônima](http://www.iis.net/configreference/system.webserver/security/authentication/anonymousauthentication),|  
|Autenticação do Windows|Adicione, à lista de associações, as contas de grupo ou de usuário do Windows que estão solicitando dados do Analysis Services por representação ou delegação.<br /><br /> Supondo que a delegação restrita de Kerberos seja utilizada, as únicas contas que precisam de permissões são as contas de grupo e de usuário do Windows solicitando acesso. Nenhuma permissão é necessária para a identidade do pool de aplicativos.|  
|Autenticação Básica|Adicione, à lista de associações, as contas de grupo ou de usuário do Windows que serão passadas na cadeia de conexão.<br /><br /> Além disso, se você estiver passando as credenciais por meio de `EffectiveUserName` na cadeia de conexão, em seguida, a identidade do pool de aplicativos deve ter direitos de administrador na instância do Analysis Services. No SSMS, clique com botão direito a instância &#124; **propriedades** &#124; **segurança** &#124; **adicionar**. Insira a identidade do pool de aplicativos. Se você usou a identidade padrão interna, a conta é especificada como **AppPool\DefaultAppPool do IIS**.<br /><br /> ![](../media/ssas-httpaccess-iisapppoolidentity.png)|  
  
 Para saber mais sobre como definir permissões, veja [Autorizar o acesso a objetos e operações &#40;Analysis Services 41](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md).  
  
##  <a name="bkmk_test"></a> Etapa 6: Testar a configuração  
 A sintaxe da cadeia de conexão para MSMDPUMP é a URL para o arquivo MSMDPUMP.dll.  
  
 Se o aplicativo web estiver escutando em uma porta fixa, acrescente o número da porta para o nome do servidor ou endereço IP (por exemplo, http://my-web-srv01:8080/OLAP/msmdpump.dll ou http://123.456.789.012:8080/OLAP/msmdpump.dll.  
  
 Para testar rapidamente a conexão, é possível abrir uma conexão utilizando o Microsoft Excel ou o SQL Server Management Studio  
  
 **Testar conexões usando o SQL Server Management Studio**  
  
1.  No Management Studio, na caixa de diálogo Conectar ao Servidor, selecione **Analysis Services** como tipo de servidor. Em Nome do servidor, insira o endereço HTTP da extensão msmdpump: `http://my-web-srv01/OLAP/msmdpump.dll`.  
  
     O pesquisador de objetos exibe a conexão HTTP:  
  
     ![Pesquisador de objetos mostrando conexão http no SSAS](../media/ssas-httpaccess-ssms.PNG "Pesquisador de objetos mostrando conexão http no SSAS")  
  
2.  A autenticação deve ser a autenticação do Windows, e a pessoa que usa o Management Studio deve ser um administrador do Analysis Services. Um administrador pode conceder permissões adicionais para permitir o acesso de outros usuários.  
  
 **Testar as conexões usando o Excel**  
  
1.  Na guia Dados do Excel, em Obter Dados Externos, clique em **De Outras Fontes**e escolha **Do Analysis Services** para iniciar o Assistente para Conexão de Dados.  
  
2.  Em Nome do servidor, insira o endereço HTTP da extensão msmdpump: `http://my-web-srv01/OLAP/msmdpump.dll`.  
  
3.  Em Credenciais de logon, escolha **Usar Autenticação do Windows** se você estiver usando a segurança integrada do Windows ou NTLM, ou Usuário anônimo.  
  
     Para a autenticação Básica, escolha **Usar a seguinte senha e nome de usuário**e especifique as credenciais usadas para entrar. As credenciais fornecidas serão passadas na cadeia de conexão para o Analysis Services.  
  
 **Testar as conexões usando o AMO**  
  
 Você pode testar o acesso HTTP usando o AMO de modo programático, substituindo a URL do ponto de extremidade do nome do servidor. Para obter detalhes, veja [Postagem do fórum (Como sincronizar bancos de dados do SSAS 2008 R2 via HTTPS além dos limites do domínio/floresta e do firewall)](http://social.msdn.microsoft.com/Forums/en/sqlanalysisservices/thread/c4249d55-914d-4c81-9980-44d0b8df9c3e).  
  
 Uma cadeia de conexão de exemplo que ilustra a sintaxe do acesso HTTP(S) usando a autenticação Básica:  
  
 `Data Source=https://<servername>/olap/msmdpump.dll; Initial Catalog=AdventureWorksDW2012; Integrated Security=Basic; User ID=XXXX; Password=XXXXX;`  
  
 Para obter mais informações sobre como configurar a conexão de modo programático, consulte [Establishing Secure Connections in ADOMD.NET](../multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections.md).  
  
 Como etapa final, faça testes mais rigorosos usando um computador cliente executado no ambiente de rede no qual as conexões serão originadas.  
  
## <a name="see-also"></a>Consulte também  
 [Postagem no Fórum (acesso http usando o msmdpump e a autenticação básica)](http://social.msdn.microsoft.com/Forums/en/sqlanalysisservices/thread/79d2f225-df35-46da-aa22-d06e98f7d658)   
 [Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](configure-the-windows-firewall-to-allow-analysis-services-access.md)   
 [Autorizar o acesso a objetos e operações &#40;do Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)   
 [Métodos de autenticação do IIS](http://go.microsoft.com/fwlink/?LinkdID=208461)   
 [Como configurar o SSL no IIS 7](http://go.microsoft.com/fwlink/?LinkId=207562)  
  
  