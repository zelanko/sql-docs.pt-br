---
title: 'Lista de verificação de implantação: instalação de vários servidores do PowerPivot para SharePoint 2010 | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 4380040a-1368-4a47-8930-47c65a192e59
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 20d32f3a050e79aef90eb8df302bd7a590cead3e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85045145"
---
# <a name="deployment-checklist-multi-server-installation-of-powerpivot-for-sharepoint-2010"></a>Lista de verificação de implantação: instalação multisservidor do PowerPivot para SharePoint 2010
  Esta lista de verificação orienta você pelas etapas para adicionar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint a um farm do sharepoint 2010 de três camadas que você cria desde o início. Um farm em três níveis contém os níveis de banco de dados, aplicativo e Web. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]A adição a essa topologia requer que você execute SQL Server instalação para instalar [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] na camada de aplicativo. Os arquivos de programa do PowerPivot são adicionados à camada da Web, mas somente como uma tarefa de pós-instalação quando você implanta a solução de aplicativo Web. Embora haja etapas de instalação, não é necessário executar nenhuma etapa de instalação separada na camada da Web nem na camada de dados. A única etapa de instalação que você precisa executar é a instalação [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] nos servidores de aplicativos.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2010|  
  
  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você deve ser um administrador local para instalar o SQL Server e o SharePoint 2010.  
  
 A pessoa que instalar o SharePoint também deve configurar o farm. Para configurar o farm, você deve ter um logon do SQL Server no servidor de banco de dados. O logon deve ser atribuído às seguintes funções: `dbcreator`, `securityadmin` e `public`.  
  
 Você precisa ter a edição enterprise ou enterprise evaluation do SharePoint Server 2010.  
  
 O computador deve ser unido a um domínio.  
  
 Você deve saber quais contas usará para executar o Mecanismo de Banco de Dados, os serviços no seu farm, e o Analysis Services no modo Integrado do SharePoint. Embora você possa alterar essas contas posteriormente, deve especificá-las pela primeira vez durante a instalação.  
  
 As contas de serviço que você especifica durante a instalação devem ser contas de usuário de domínio.  
  
 Antes de iniciar a instalação, verifique suas configurações de navegador para saber se tem uma conexão à Internet. O instalador obrigatório abre uma conexão à Internet para baixar o software necessário. Você deve fazer as seguintes alterações para garantir que terá todo o software necessário:  
  
-   No Gerenciador de Servidor, desative temporariamente a Configuração de Segurança Avançada do Internet Explorer para permitir downloads no servidor. Para baixar o software necessário, você pode desativar a ESC do IE apenas para os Administradores.  
  
-   No Internet Explorer, também pode ser necessário configurar seu navegador para ignorar um servidor de proxy para permitir acesso do host local a URLs da Internet.  
  
    1.  No Internet Explorer, no menu Ferramentas, clique em Opções.  
  
    2.  Na guia Conexões, na área de configurações de Rede local (LAN), clique em Configurações de LAN.  
  
    3.  Na área de configuração Automática, desmarque a caixa de seleção Detectar automaticamente as configurações.  
  
    4.  Na área Servidor de Proxy, marque a caixa de seleção Usar um servidor de proxy na sua LAN.  
  
    5.  Digite o endereço do servidor de proxy na caixa Endereço.  
  
    6.  Digite o número da porta do servidor de proxy na caixa Porta.  
  
    7.  Marque a caixa de seleção Ignorar servidor de proxy para endereços locais.  
  
    8.  Clique em OK para fechar a caixa de diálogo Configurações de Rede local (LAN).  
  
    9. Clique em OK para fechar a caixa de diálogo Opções da Internet.  
  
##  <a name="install-a-database-server"></a><a name="installdb"></a>Instalar um servidor de banco de dados  
 Este tópico pressupõe que a topologia do farm se baseia na descrita no artigo [vários servidores para um farm de três camadas](https://go.microsoft.com/fwlink/?LinkId=182771). Se você já tiver um farm que esteja operacional, pule para [instalar PowerPivot para SharePoint](#installppapp).  
  
 Se você está apenas começando a usar sua topologia, comece instalando um Mecanismo de Banco de Dados do SQL Server. Estas instruções geram um servidor de banco de dados que pode ser acessado pelos servidores do SharePoint no seu farm.  
  
1.  No computador que você está usando para o servidor de banco de dados, execute SQL Server instalação para instalar SQL Server Mecanismo de Banco de Dados (consulte [instalar SQL Server 2014 no assistente de instalação &#40;&#41;de instalação ](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)).  
  
     Ao selecionar os recursos que deseja instalar, escolha o seguinte:  
  
    -   Serviços do Mecanismo de Banco de Dados  
  
    -   Conectividade das ferramentas de cliente  
  
    -   Ferramentas de Gerenciamento - Completo (O Básico será incluído automaticamente)  
  
2.  Depois que o Mecanismo de Banco de Dados estiver instalado, ative o TCP/IP para conexões remotas e reinicie o serviço:  
  
    1.  Inicie o SQL Server Configuration Manager  
  
    2.  Abra Configuração de Rede do SQL Server.  
  
    3.  Selecione **Protocolos do MSSQLSERVER**.  
  
    4.  Clique com o botão direito do mouse em **TCP/IP** e selecione **habilitar**.  
  
    5.  Clique em **serviços SQL Servers**.  
  
    6.  Clique com o botão direito do mouse em **SQL Server (MSSQLSERVER)** e clique em **reiniciar**.  
  
3.  Ative o acesso de entrada no servidor de banco de dados através do Firewall do Windows. Isso permite que os servidores do SharePoint no farm se conectem aos bancos de dados de do SharePoint. Para obter mais informações sobre como fazer isso, veja [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
    1.  No painel de controle do Windows, em ferramentas administrativas, clique em **Firewall do Windows com segurança avançada**.  
  
    2.  Clique em **Regras de Entrada**.  
  
    3.  Clique em **nova regra**.  
  
    4.  Em tipo de regra, clique em **personalizado**.  
  
    5.  Clique em **Próximo**.  
  
    6.  Em programa, na seção serviços, clique em **Personalizar**.  
  
    7.  Clique em **aplicar a este serviço**.  
  
    8.  Selecione **SQL Server (MSSQLSERVER)** se você instalou SQL Server como a instância padrão e, em seguida, clique em **OK**.  
  
    9. Clique em **Próximo**.  
  
    10. Em protocolo e portas, aceite as configurações padrão e clique em **Avançar**.  
  
    11. Em escopo, aceite as configurações padrão e clique em **Avançar**.  
  
    12. Em ação, aceite as configurações padrão e clique em **Avançar**.  
  
    13. Em perfil, desmarque as caixas de seleção para **privado** e **público**e clique em **Avançar**.  
  
    14. Em nome, digite um nome descritivo para a regra de entrada (por exemplo, **SQL Server**).  
  
    15. Clique em **Concluir**.  
  
##  <a name="install-and-configure-a-three-tier-sharepoint-2010-farm"></a><a name="installsp"></a>Instalar e configurar um farm do SharePoint 2010 de três camadas  
 Nos computadores você está usando como servidores do SharePoint, execute o programa SharePoint Prerequisite Installer em cada um, seguido pela Instalação do SharePoint Server.  
  
 Use as instruções a seguir na documentação do SharePoint 2010 para instalar e configurar um farm do SharePoint 2010 que inclua dois servidores de Web e um servidor de aplicativos:  
  
 [Vários servidores para um farm de três camadas (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=182771)  
  
 Quando for solicitado que você especifique um servidor de banco de dados, especifique o servidor de banco de dados que você instalou anteriormente.  
  
 Nos procedimentos a seguir, pressupõe-se que você configurou o farm seguindo as instruções de instalação de um farm de três níveis. O farm deve incluir os seguintes serviços e recursos:  
  
-   Serviços do Excel, Serviço de Pesquisa e Serviço de Repositório Seguro  
  
-   Um aplicativo de Web e um conjunto de sites  
  
-   Coleta de dados de uso e integridade  
  
-   Registro de diagnóstico  
  
##  <a name="install-powerpivot-for-sharepoint-on-an-application-server"></a><a name="installppapp"></a>Instalar o PowerPivot para SharePoint em um servidor de aplicativos  
 Execute a Instalação do SQL Server para adicionar o PowerPivot para SharePoint a um farm do SharePoint. Se o farm consistir em vários servidores SharePoint, você deverá executar a Instalação do SQL Server em um servidor de aplicativos já inserido no farm.  
  
 Sempre instale o PowerPivot para SharePoint em um servidor de aplicativos. Embora os servidores Web de front-end também executem os componentes de servidor do PowerPivot para SharePoint, os componentes executados no front-end da Web serão instalados durante a etapa de configuração do PowerPivot para SharePoint, quando você implantar soluções no farm. Para obter mais informações sobre a instalação, consulte [instalar PowerPivot para SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md).  
  
 Se a topologia de implantação exigir duas instâncias do PowerPivot para SharePoint, execute a Instalação do SQL Server em cada servidor de aplicativo. Você pode ter apenas uma instância do PowerPivot para SharePoint em um único computador. Se você precisar de várias instâncias, use servidores adicionais. Para obter mais informações sobre como adicionar vários servidores PowerPivot para SharePoint ao mesmo farm, consulte [lista de verificação de implantação: expansão adicionando servidores PowerPivot a um farm do SharePoint 2010](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md).  
  
##  <a name="install-analysis-services-client-libraries-on-sharepoint-applications-servers-that-do-not-have-an-installation-of-powerpivot-for-sharepoint"></a><a name="installclientlib"></a>Instalar Analysis Services bibliotecas de cliente em servidores de aplicativos do SharePoint que não têm uma instalação do PowerPivot para SharePoint  
 Uma topologia de farm, que inclui um servidor de aplicativo ou servidor de front-end da Web que executa os aplicativos a seguir sem uma instalação do PowerPivot para SharePoint no mesmo computador, exigirá software adicional para dar suporte a recursos e acesso a dados PowerPivot:  
  
-   Serviços do Excel ou serviços do PerformancePoint  
  
-   Administração Central executada como um aplicativo autônomo em seu próprio servidor  
  
 Os Serviços do Excel e os Serviços do PerformancePoint exigem uma versão mais recente do provedor OLE DB do Analysis Services para dar suporte a acesso a dados PowerPivot. Se você executar qualquer aplicativo em um computador que não tenha o provedor do OLE DB mais recente, instale o provedor manualmente. Para obter mais informações, consulte [instalar o provedor Analysis Services OLE DB em servidores do SharePoint](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)  
  
 De modo semelhante, um computador que tenha somente a Administração Central, sem o PowerPivot para SharePoint no mesmo computador, exigirá a biblioteca de cliente do ADOMD.NET. Essa biblioteca é usada pelo Painel de Gerenciamento do PowerPivot para acessar dados internos usados para preencher o painel. Para obter mais informações, confira [Instalar o ADOMD.NET em servidores Web front-end executando a Administração Central](../../../2014/sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md).  
  
##  <a name="configure-the-server"></a><a name="configsrvr"></a>Configurar o servidor  
 Use a Ferramenta de Configuração do PowerPivot para configurar o PowerPivot para SharePoint. A ferramenta examinará a configuração existente do farm e fornecerá opções para instalar ou ativar os recursos do SharePoint necessários para PowerPivot para SharePoint. Durante essa etapa, o Claims to Windows Token Service será iniciado. Além disso, se outros recursos necessários do SharePoint ainda não tiverem sido habilitados, a ferramenta de configuração os adicionará à lista e incluirá ações para habilitação do recurso.  
  
 Para obter mais informações, consulte [Configurar ou reparar 2010 PowerPivot para SharePoint &#40;ferramenta de configuração do PowerPivot&#41;](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md).  
  
##  <a name="configure-alternate-access-mapping-for-web-front-end-servers"></a><a name="AAM"></a>Configurar o mapeamento de acesso alternativo para servidores Web front-end  
 Para garantir que as solicitações de acesso a dados PowerPivot ou de atualização de dados sejam tratadas por cada servidor de front-end da Web, você deve correlacionar as diferentes URLs de cada servidor com o mesmo aplicativo da Web.  
  
1.  Na administração central, em gerenciamento de aplicativos, clique em **configurar mapeamentos alternativos de acesso**.  
  
2.  Em Conjunto de Mapeamento de Acesso Alternativo, selecione seu aplicativo de Web.  
  
3.  Clique em **Adicionar URL interna**.  
  
4.  Especifique a URL do primeiro servidor de front-end da Web.  
  
5.  Repita as etapas anteriores para adicionar a URL do segundo servidor de front-end da Web.  
  
##  <a name="activate-powerpivot-feature-integration-for-site-collections"></a><a name="activatePP"></a>Ativar a integração de recursos do PowerPivot para coleções de sites  
 A ativação de recursos em nível de coleção de sites disponibiliza as páginas de aplicativos e os modelos em seus sites, incluindo páginas de configuração para atualização de dados agendada e páginas de aplicativo para Galeria do PowerPivot e bibliotecas de Feed de Dados.  
  
 A Ferramenta de Configuração do PowerPivot ativará a integração do recurso com o conjunto de sites especificado. Você pode executar a ferramenta várias vezes para selecionar conjuntos de sites adicionais. Alternativamente, os administradores de site podem configurar a ativação de recurso de dentro do SharePoint. Para obter mais informações, consulte [ativar a integração de recursos do PowerPivot para coleções de sites na administração central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca).  
  
##  <a name="verify-integration-and-server-availability"></a><a name="verify"></a>Verificar a integração e a disponibilidade do servidor  
 O processamento de consultas do PowerPivot no farm ocorre quando um usuário ou aplicativo abre uma pasta de trabalho do Excel que contém dados PowerPivot. No mínimo, você pode verificar se páginas de sites do SharePoint contêm recursos do PowerPivot disponíveis. No entanto, para verificar integralmente uma instalação, você deve ter uma pasta de trabalho PowerPivot que possa publicar no SharePoint e acessar em uma biblioteca. Para fins de teste, é possível publicar uma pasta de trabalho de exemplo que já contenha os dados PowerPivot e usá-la para confirmar se essa integração com o SharePoint está configurada corretamente.  
  
 Para verificar a integração do PowerPivot com um site do SharePoint, faça o seguinte:  
  
1.  Em um navegador, abra o aplicativo Web criado. Se você usou valores padrão, poderá especificar http:// \<your computer name> no endereço da URL.  
  
2.  Verifique se os recursos de acesso aos dados e de processamento do PowerPivot estão disponíveis no aplicativo. É possível fazer isso verificando a presença de modelos de biblioteca fornecidos pelo PowerPivot:  
  
    1.  Em ações do site, clique em **mais opções..**.  
  
    2.  Em bibliotecas, você deve ver **biblioteca de feeds de dados** e **Galeria PowerPivot**. Esses modelos de biblioteca são fornecidos pelo recurso do PowerPivot, estando visíveis na lista Bibliotecas apenas se o recurso estiver integrado corretamente.  
  
 Para verificar o acesso a dados PowerPivot no servidor, faça o seguinte:  
  
1.  [Baixe](https://go.microsoft.com/fwlink/?LinkID=219108) os exemplos de dados Picnic que acompanham um tutorial do Reporting Services. Você usará a pasta de trabalho de exemplo nesse download para verificar o acesso aos dados PowerPivot. Extraia os arquivos.  
  
2.  Carregue uma pasta de trabalho PowerPivot na Galeria PowerPivot ou em qualquer biblioteca do SharePoint.  
  
3.  Clique no documento para abri-lo na biblioteca.  
  
4.  Clique em uma segmentação de dados ou filtre os dados para iniciar uma consulta do PowerPivot. O servidor carregará dados PowerPivot em segundo plano e retornará os resultados. Na próxima etapa, você se conectará ao servidor para verificar se os dados foram carregados e armazenados em cache.  
  
5.  Inicie o SQL Server Management Studio no grupo de programas Microsoft SQL Server 2008 R2 no menu Iniciar. Se essa ferramenta não estiver instalada no servidor, será possível passar à última etapa para confirmar a presença de arquivos armazenados em cache.  
  
6.  Em tipo de servidor, selecione **Analysis Services**.  
  
7.  Em nome do servidor, digite ** \<server-name> \powerpivot**, em que **\<server-name>** é o nome do computador que tem a instalação do PowerPivot para SharePoint.  
  
8.  Clique em **Conectar**.  
  
9. No Pesquisador de objetos, clique em **bancos** de dados para exibir a lista de arquivos de dados PowerPivot que são carregados.  
  
10. No sistema de arquivos do computador, verifique a pasta a seguir para determinar se os arquivos estão armazenados no cache em disco. A presença de arquivos armazenados em cache é a verificação adicional de que a implantação é operacional. Para exibir o cache de arquivos, vá até a pasta \Arquivos de programas\Microsoft SQL Server\MSAS10_50.POWERPIVOT\OLAP\Backup.  
  
##  <a name="post-installation-steps"></a><a name="nextsteps"></a>Etapas pós-instalação  
 Depois que você verificar a instalação, conclua a configuração do serviço criando uma Galeria PowerPivot ou ajustando parâmetros de configuração individuais. Para usar integralmente os componentes do servidor recém-instalados, você pode baixar o [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] para criar e publicar sua primeira pasta de trabalho PowerPivot.  
  
####  <a name="set-upper-limits-on-disk-space-usage"></a><a name="bkmk_disk"></a>Definir limites superiores de uso de espaço em disco  
 Você pode definir um limite máximo de utilização de espaço em disco para arquivos de dados PowerPivot que são armazenados em cache no disco. O padrão é usar todo o espaço disponível em disco. Para obter instruções sobre como limitar o uso de espaço em disco, consulte [Configurar o uso de espaço em disco &#40;PowerPivot para SharePoint&#41;](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-disk-space-usage-power-pivot-for-sharepoint).  
  
####  <a name="increase-file-maximum-upload-size-for-sharepoint-web-applications"></a><a name="Upload"></a>Aumentar tamanho máximo de carregamento do arquivo para aplicativos Web do SharePoint  
 Como as pastas de trabalho PowerPivot podem ser grandes, você pode aumentar o tamanho máximo do carregamento de arquivo. Há duas configurações de tamanho de arquivo a serem configuradas: Tamanho Máximo de Carregamento para o aplicativo Web e Tamanho Máximo da Pasta de Trabalho em Serviços do Excel. O tamanho de arquivo máximo deve ser definido para o mesmo valor em ambos os aplicativos. Para obter instruções, consulte [Configurar o tamanho máximo de upload de arquivo &#40;PowerPivot para SharePoint&#41;](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint).  
  
#### <a name="grant-sharepoint-permissions-to-workbook-users"></a>Conceder permissões do SharePoint a usuários de pastas de trabalho  
 Os usuários precisarão de permissões do SharePoint para publicar ou exibir pastas de trabalho. Certifique-se de conceder permissões de **exibição** a usuários que precisam exibir pastas de trabalho publicadas e permissões de **colaboração** para usuários que publicam ou gerenciem pastas de trabalho. Você deve ser um administrador do conjunto de sites para conceder permissões.  
  
1.  No site do, clique em **ações do site**.  
  
2.  Clique em **permissões do site**.  
  
3.  Marque a caixa de seleção do grupo **Membros** do conjunto de sites.  
  
4.  Na faixa de faixas, clique em **conceder permissões**.  
  
5.  Insira o usuário do domínio do Windows ou as contas do grupo que devem ter permissão para adicionar ou remover documentos.  
  
6.  Clique em **OK**.  
  
7.  Marque a caixa de seleção do grupo **visitantes** do conjunto de sites.  
  
8.  Na faixa de faixas, clique em **conceder permissões**.  
  
9. Insira o usuário do domínio do Windows ou as contas do grupo que devem ter permissão para exibir documentos. Como anteriormente, não use endereços de email ou grupos de distribuição se o aplicativo estiver configurado para autenticação clássica.  
  
10. Clique em **OK**.  
  
#### <a name="install-adonet-data-services-35-sp1"></a>Instale o ADO.NET Data Services 3.5 SP1  
 O ADO.NET Data Services é obrigatório para uma exportação do feed de dados das listas do SharePoint. O SharePoint 2010 não inclui esse componente no programa PrerequisiteInstaller, assim você deve instalá-lo manualmente. Para obter mais informações sobre como instalar os serviços de dados do ADO.NET, consulte [instalar o ADO.NET Data Services para dar suporte às exportações de feed de dados de listas do SharePoint](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md).  
  
#### <a name="install-data-providers-used-in-data-refresh-and-check-user-permissions"></a>Instalar provedores de dados usados na atualização de dados e verificar permissões de usuário  
 A atualização de dados do servidor permite que os usuários reimportem dados atualizados para suas pastas de trabalho no modo autônomo. Para que a atualização de dados seja bem-sucedida, o servidor deve ter o mesmo provedor de dados que foi usado originalmente para importar os dados. Além disso, a conta de usuário na qual a atualização de dados é executada frequentemente requer permissões de leitura nas fontes de dados externas. Verifique os requisitos para habilitar e configurar a atualização de dados para garantir êxito no resultado. Para obter mais informações, consulte [PowerPivot data Refresh com o SharePoint 2010](../../../2014/analysis-services/powerpivot-data-refresh-with-sharepoint-2010.md).  
  
#### <a name="create-a-powerpivot-gallery"></a>Criar uma Galeria PowerPivot  
 A Galeria PowerPivot é uma biblioteca que inclui opções de visualização e apresentação para exibir pastas de trabalho PowerPivot em um site do SharePoint. Recomenda-se usar a Galeria PowerPivot para publicar e exibir pastas de trabalho do PowerPivot em função do seu recurso de visualização. Além disso, se você também implantou o Reporting Services no mesmo servidor do SharePoint, uma Galeria PowerPivot permitirá a facilidade de uso na criação de relatórios. Você pode iniciar o Construtor de Relatórios a partir da Galeria PowerPivot para basear um novo relatório em uma pasta de trabalho publicada do PowerPivot. Para obter mais informações sobre como criar e usar a biblioteca, consulte [criar e personalizar a Galeria PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery) e [usar a Galeria PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/use-power-pivot-gallery).  
  
#### <a name="tune-configuration-settings"></a>Ajustar definições de configuração  
 Um aplicativo do serviço PowerPivot é criado usando propriedades e valores padrão. Você pode modificar parâmetros de configuração para aplicativos de serviço individuais para alterar a metodologia pela qual solicitações são alocadas, definir tempos limite de servidor, alterar os limites para eventos de relatório de resposta de consulta ou especificar por quanto tempo os dados de uso são retidos. Para obter mais informações sobre a configuração na administração central ou sobre como usar recursos do PowerPivot em aplicativos Web do SharePoint, consulte [Administração e configuração do servidor PowerPivot na administração central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration).  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos com suporte nas edições do SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473)   
 [Instalar o PowerPivot para SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)   
 [Lista de verificação de implantação: expansão adicionando servidores PowerPivot a um farm do SharePoint 2010](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)  
  
  
