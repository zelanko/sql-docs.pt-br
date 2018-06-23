---
title: Instalar o PowerPivot para SharePoint 2010 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eec38696-5e26-46fa-bc83-aa776f470ce8
caps.latest.revision: 52
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: c77fa146f7703fb67cf0d1ad5c9aa0c042737976
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121202"
---
# <a name="install-powerpivot-for-sharepoint-2010"></a>Instale o PowerPivot para SharePoint 2010
  O [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] é uma coleção de serviços de camada intermediária e backend que fornece acesso a dados PowerPivot em um farm do SharePoint 2010. Se sua organização usa o aplicativo cliente, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel 2010, para criar pastas de trabalho contendo dados analíticos, você precisa ter o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] para acessar esses dados em um ambiente de servidor. Este tópico orienta você pelo processo básico de instalação e vincula a tópicos adicionais para ajudar a configurar o PowerPivot.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
 
  
 Para obter instruções sobre como instalar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no mesmo servidor, consulte [lista de verificação de implantação: Reporting Services, Power View e PowerPivot para SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md).  
  
## <a name="prerequisites"></a>Prerequisites  
  
1.  Você deve ser um administrador local para executar a Instalação do SQL Server.  
  
2.  O SharePoint Server 2010 Enterprise Edition é necessário ao [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. Você também pode usar a edição evaluation enterprise.  
  
3.  O SharePoint Server 2010 SP2 deve ser instalado. Sem ele, você não poderá configurar o farm para usar os recursos do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
4.  O computador deve ser unido a um domínio.  
  
5.  Você deve ter uma conta de usuário de domínio para provisionar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Em uma instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], a conta de serviço Analysis Services deve ser uma conta de usuário de domínio de forma que você pode gerenciar isto de Administração Central. Você digitará a conta e as credenciais na página **Configuração do Servidor** como parte das etapas deste documento.  
  
6.  O nome da instância do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] deve estar disponível. Você não pode ter uma instância nomeada existente do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no computador em que está instalando o PowerPivot para SharePoint.  
  
7.  A instância do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] não pode fazer parte de um cluster de failover do SQL Server. Use os recursos de alta disponibilidade do produto do SharePoint. Por exemplo, os Serviços do Excel gerenciam o balanceamento de carga dos servidores PowerPivot para SharePoint. Para obter mais informações, consulte [modelo de dados de gerenciar os serviços do Excel (SharePoint Server 2013) de configurações](http://technet.microsoft.com/library/jj219780.aspx) (http://technet.microsoft.com/library/jj219780.aspx).  
  
8.  Se você estiver instalando o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] em um farm existente, deverá ter um ou mais aplicativos Web SharePoint configurados para a autenticação de modo clássico. O acesso a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] só funcionará se o aplicativo Web oferecer suporte à autenticação de modo clássica. Para obter mais informações sobre requisitos do modo clássico, consulte [PowerPivot Authentication and Authorization](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md).  
  
9. Analise os tópicos adicionais a seguir para entender os requisitos de sistema e de versão:  
  
    -   [Orientação para usar os recursos de BI do SQL Server em um farm do SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
##  <a name="InstallSQL"></a> Etapa 1: Instalar o PowerPivot para SharePoint  
 Nesta etapa, você executa o SQL Server para instalar o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. Em uma etapa subsequente, você configurará o servidor como uma tarefa de post-instalação.  
  
1.  Insira a mídia de instalação ou abra uma pasta que contém os arquivos de instalação do SQL Server e clique duas vezes em **setup.exe**.  
  
2.  Clique em **Instalação** no painel de navegação esquerdo.  
  
3.  Clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
4.  Na página **Chave do Produto (Product Key)** , especifique a edição de avaliação ou digite uma chave do produto (product key) de uma cópia licenciada da edição empresarial.  
  
     Clique em **Avançar**.  
  
5.  Aceite os termos do contrato de licença de software da Microsoft e nós agradeceremos se você também ativar a experiência do cliente e o relatório de erros. Clique em **Avançar**.  
  
6.  Atualize os arquivos de instalação se você for solicitado a fazer isso.  
  
7.  Na página **Regras de Instalação** , a instalação identifica problemas que poderiam impedir a instalação. Examine a lista para determinar se a Instalação detectou problemas potenciais no sistema.  
  
    > [!NOTE]  
    >  Como o Firewall do Windows está ativado, você será avisado para abrir portas a fim de permitir o acesso remoto. Esse aviso geralmente não é aplicável a instalações do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. As conexões com arquivos de dados e serviços do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são feitas com o uso de portas do SharePoint que já estão abertas para a comunicação entre serviços do SharePoint.  
  
     Clique em **Avançar**. Aguarde enquanto os arquivos do programa de Instalação do SQL Server são instalados no servidor.  
  
8.  Na página **Função de Instalação** , selecione **SQL Server PowerPivot para SharePoint**.  
  
9. Opcionalmente, você pode acrescentar uma instância do Mecanismo de banco de dados a sua instalação. Você pode fazer isso se estiver configurando um novo farm e precisar de um servidor de banco de dados para executar os bancos de dados de configuração e conteúdo do farm. Se você adicionar o Mecanismo de Banco de Dados, ele será instalado como uma instância nomeada do PowerPivot. Sempre que você precisa especificar uma conexão com esta instância (por exemplo, no assistente configuração farm se você estiver usando o Assistente para configurar o farm), insira o nome do banco de dados neste formato: <`servername`> \PowerPivot.  
  
     ![GMNI_SetupUI_FeatureRole](../../../2014/sql-server/install/media/gmni-setupui-featurerole.gif "GMNI_SetupUI_FeatureRole")  
  
10. Clique em **Avançar**.  
  
11. Na página **Seleção de Recursos** , uma lista somente leitura dos recursos a serem instalados será exibida para fins informativos. Não é possível adicionar ou remover itens pré-selecionados para essa função. Clique em **Avançar**.  
  
12. Na página **Regras de Recurso** , clique em **Avançar**. A página pode ser ignorada.  
  
13. Na página **Configuração da Instância** , um nome de instância somente leitura do 'PowerPivot' é exibido para fins informativos. Esse nome de instância do **POWERPIVOT** é **obrigatória e não pode ser modificada**. No entanto, é possível inserir um ID da Instância exclusivo para especificar um nome de diretório descritivo e chaves do Registro. Clique em **Avançar**.  
  
14. Na página **Configuração do Servidor** , digite as informações da conta desejada.  
  
     Para o SQL Server Analysis Services, é preciso especificar uma conta de usuário do domínio. Não especifique uma conta interna. As contas de domínio não necessárias para gerenciar a conta de serviço do Analysis Services como uma *conta gerenciada* na Administração Central do SharePoint.  
  
     ![Configuração do servidor SSAS](../../../2014/sql-server/install/media/ssas-powerpivotsetupsql2012sp1-serverconfiguration.gif "configuração do servidor SSAS")  
  
     Se você adicionou o Mecanismo de Banco de Dados do SQL Server e o SQL Server Agent, é possível configurar os serviços para serem executados como contas de usuário do domínio ou na conta virtual padrão.  
  
     Nunca use sua própria conta de usuário de domínio para provisionar qualquer serviço. Isso concede ao servidor as mesmas permissões que você tem aos recursos em sua rede. Se o servidor for afetado por um usuário mal-intencionado, esse usuário será conectado com suas credenciais de domínio, com capacidade para baixar ou usar os mesmos dados e aplicativos que você use.  
  
15. Clique em **Avançar**.  
  
16. Se você estiver instalando o Mecanismo de Banco de Dados, a página Configuração do Mecanismo de Banco de Dados será exibida. Em Configuração do Mecanismo de Banco de Dados, clique em **Adicionar Usuário Atual** para conceder à conta do usuário permissões de administrador na instância do Mecanismo de Banco de Dados. Clique em **Adicionar** para adicionar contas. Clique em **Avançar**.  
  
17. Na página **Configuração do Analysis Services** , clique em **Adicionar Usuário Atual** para conceder à conta do usuário permissões administrativas. Você precisará de permissão administrativa para configurar o servidor depois que Instalação seja concluída.  
  
18. Na mesma página, adicione a conta de usuário do Windows de qualquer pessoa que também precise de permissões administrativas. Por exemplo, qualquer usuário que quiser se conectar à instância do [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] no SQL Server Management Studio para solucionar problemas de conexão do banco de dados ou obter informações sobre a versão deve ter permissões de administrador do sistema no servidor. Adicione a conta do usuário de qualquer pessoa que precise solucionar problemas ou administrar o servidor agora.  
  
19. Clique em **Avançar**.  
  
20. Clique em **Avançar** em cada uma das páginas restantes até chegar à página Pronto para Instalar.  
  
21. Clique em **Instalar**.  
  
> [!TIP]  
>  Se você precisar problemas ao fazer a instalação do SQL Server, consulte [exibir e ler arquivos de Log do SQL Server Setup](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
##  <a name="bkmk_config"></a> Etapa 2: Configurar o servidor  
  
> [!IMPORTANT]  
>  O SharePoint 2010 SP2 deve ser instalado antes da configuração do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] ou de um farm do SharePoint que use um servidor de banco de dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Se você ainda não instalou o service pack; faça isso agora, antes de começar a configurar o servidor.  
  
 Instalação não é completa até que o servidor é configurado. Nesta versão, configuração de servidor é executada sempre como tarefa de pós-instalação, enquanto usando um das abordagens seguintes: Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], Administração Central ou PowerShell. Para continuar, escolha uma das seguintes abordagens:  
  
-   [Configurar ou reparar o PowerPivot para SharePoint 2010 &#40;ferramenta de configuração do PowerPivot&#41;](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md)  
  
-   [Administração e configuração de servidor do PowerPivot na Administração Central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
-   [Configuração do PowerPivot usando o Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
 **Conectando-se à instância do mecanismo de banco de dados.** Quando você instalar o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], a Instalação do SQL Server dá a opção de adicionar uma instância do Mecanismo de Banco de Dados a sua instalação. Você poderá ter adicionado uma instância do Mecanismo de Banco de Dados à sua instalação se estiver configurando um novo farm e precisar de um servidor de banco de dados para executar os bancos de dados de configuração e conteúdo do farm. Se você adicionou o Mecanismo de Banco de Dados, ele foi instalado como uma instância nomeada do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Sempre que você precisa especificar uma conexão com esta instância (por exemplo, no assistente configuração farm se você estiver usando o Assistente para configurar o farm), lembre-se de inserir o nome do banco de dados neste formato: <`servername`> \PowerPivot.  
  
##  <a name="bkmk_redist"></a> Etapa 3: Provedores de instalação do OLE DB do Analysis Services em servidores de aplicativos de serviços do Excel  
 As etapas de instalação adicionais serão necessárias se você executar os Serviços de Cálculo do Excel e o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em servidores de aplicativo separados. Nos servidores de aplicativo que executam os Serviços de Cálculo do Excel, instale a versão apropriada do provedor OLE DB do Analysis Services (MSOLAP).  
  
-   A versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do MSOLAP é incluída na Instalação do SQL Server, portanto, instalar explicitamente a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do MSOLAP só será necessária se o servidor de aplicativo não for um servidor de aplicativo do PowerPivot.  
  
    > [!NOTE]  
    >  O servidor de aplicativo dos Serviços de Cálculo do Excel também precisa de uma instância do arquivo **Microsoft.AnalysisServices.Xmla.dll** no assembly global. Para instalar o arquivo .dll no servidor de aplicativo, instale o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Selecione as “Ferramentas de Gerenciamento – Completo” na página **Seleção de Recursos** do assistente de Instalação do SQL Server.  
  
-   Para que o servidor de aplicativos ofereça suporte às pastas de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] mais antigas, você precisa instalar a versão SQL Server 2008 R2 do MSOLAP.  
  
 Para obter mais informações sobre como instalar o provedor, incluindo as etapas de verificação, consulte [instalar o Analysis Services OLE DB Provider em SharePoint Servers](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)  
  
##  <a name="bkmk_verify"></a> Etapa 4: Verificar a instalação  
 Nesta última etapa, você verificará que o SharePoint 2010 e o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] estão funcionando completamente. Para obter instruções, consulte [verificar um PowerPivot para SharePoint](../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md).  
  
## <a name="see-also"></a>Consulte também  
 [PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [Lista de verificação de implantação: Reporting Services, Power View e PowerPivot para SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md)   
 [Lista de verificação de implantação: Expansão adicionando servidores do PowerPivot a um farm do SharePoint 2010](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)   
 [Lista de verificação de implantação: Instalação em vários servidores do PowerPivot para SharePoint 2010](../../../2014/sql-server/install/deployment-checklist-multiserver-installation-powerpivot-sharepoint-2010.md)  
  
  