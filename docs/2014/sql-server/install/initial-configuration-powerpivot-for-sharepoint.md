---
title: Iniciais de configuração (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: dc6ab85f562aa4a2149e6471b13422e97d7fc7c5
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53353421"
---
# <a name="initial-configuration-powerpivot-for-sharepoint"></a>Configuração inicial (PowerPivot para SharePoint)
  Use as etapas deste tópico para configurar uma instalação inicial do PowerPivot para o SharePoint. O modo mais fácil de configurar uma instalação inicial é usar a ferramenta de Configuração do PowerPivot. Ela automatiza todas s etapas de configuração que são descritas abaixo.  
  
 Alternativamente, se você desejar maior controle sobre como o servidor é configurado, poderá usar a Administração Central e as informações deste tópico para executar cada etapa individualmente.  
  
 
  
## <a name="prerequisites"></a>Prerequisites  
 O servidor do SharePoint deve ter sido instalado usando a opção de instalação Farm de Servidores na instalação do SharePoint. Um servidor do SharePoint autônomo que usa um banco de dados interno não tem suporte. Para obter mais informações, consulte [diretrizes para usar recursos de BI do SQL Server em um Farm do SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md).  
  
> [!IMPORTANT]  
>  O SharePoint 2010 SP1 deve ser instalado antes da configuração do PowerPivot para SharePoint ou de um farm do SharePoint que use um servidor de banco de dados [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Se você ainda não instalou o service pack; faça isso agora, antes de começar a configurar o servidor.  
  
 O PowerPivot para SharePoint deve ser instalado. No mínimo, a solução de farm deve ser implantada. Use a ferramenta de Configuração do PowerPivot ou o script de PowerShell para implantar a solução de farm. As instruções para esta etapa são fornecidas neste tópico.  
  
 O computador deve ser unido a um domínio. As contas especificadas para serviços devem ser contas de usuário de domínio. No mínimo, você precisará de uma conta de domínio para o aplicativo de serviço PowerPivot. Se você estiver configurando serviços adicionais (como os Serviços do Excel), deverá ter contas separadas para cada serviço provisionado.  
  
 Você deve ser um administrador do farm para adicionar o PowerPivot para SharePoint ao farm. Você deve conhecer o passphrase para acrescentar servidores e aplicativos ao farm.  
  
##  <a name="deploywsp"></a> Etapa 1: Implantar soluções PowerPivot  
 Há duas soluções que devem ser instaladas e implantadas: uma solução de farm e uma solução de aplicativo Web.  
  
 **Instalar e implantar a solução de Farm**  
  
 Na versão anterior, a Instalação do SQL Server instalou e implantou a solução de farm. Nesta versão, use a ferramenta de Configuração do PowerPivot ou o script do PowerShell para implantar a solução de farm. Você não pode usar a Administração Central para implantar a solução de farm. Esta é a única etapa na configuração do PowerPivot para SharePoint que não pode ser executada na Administração Central. Depois que a solução de farm é implantada, você pode usar a Administração Central e as etapas deste tópico para configurar uma instalação do PowerPivot para SharePoint.  
  
 Nesta etapa, você executa o PowerShell para instalar e implantar a solução de farm. Para obter mais informações, consulte [configuração do PowerPivot usando o Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md).  
  
1.  Abra um Shell de Gerenciamento do SharePoint 2010 usando a opção **Executar como Administrador** .  
  
2.  Execute o primeiro cmdlet:  
  
    ```  
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     O cmdlet retorna o nome da solução, sua ID de solução e Deployed=False. Na próxima etapa, você implantará a solução.  
  
3.  Execute o segundo cmdlet para implantar a solução:  
  
    ```  
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
 **Implantar a solução de aplicativo web**  
  
1.  Clique no botão Iniciar, selecione **todos os programas**, selecione **produtos do Microsoft SharePoint 2010**e, em seguida, selecione **Administração Central do SharePoint 2010**.  
  
2.  Na Administração Central do SharePoint 2010, em Configurações do Sistema, clique em **Gerenciar soluções de farm**.  
  
     Você deverá ver dois pacotes de soluções separados: powerpivotfarm.wsp e powerpivotwebapp.wsp. A primeira solução (powerpivotfarm.wsp) já deve estar implantada. Quando é implantado, ela nunca precisa ser implantada novamente. A segunda solução (powerpivotwebapp.wsp) é implantada para a Administração Central, mas você deve implantar essa solução manualmente para cada aplicativo Web do SharePoint que oferecerá suporte ao acesso a dados PowerPivot.  
  
3.  Clique em **Powerpivotwebapp.wsp**.  
  
4.  Clique em **implantar a solução.**  
  
5.  Na **implantar em?**, selecione o aplicativo web do SharePoint ao qual você deseja adicionar suporte ao recurso PowerPivot.  
  
6.  Clique em **OK**.  
  
7.  Repita para outros aplicativos Web do SharePoint que também oferecerão suporte ao acesso a dados PowerPivot.  
  
##  <a name="Geneva"></a> Etapa 2: Iniciar serviços no servidor  
 Uma implantação do PowerPivot para SharePoint requer que seu farm inclua os seguintes serviços: Serviços de cálculo do Excel, serviço de repositório seguro e reivindicações ao Serviço de Token do Windows.  
  
 As Reivindicações para o Windows Token Service são obrigatórias para os Serviços do Excel e o PowerPivot para SharePoint. Elas são usadas para estabelecer conexões com fontes de dados externas que usam a identidade de Windows do usuário do SharePoint atual. Esse serviço deve ser executado em todos os servidores SharePoint em que os Serviços do Excel ou o PowerPivot para SharePoint esteja ativado. Se o serviço ainda não estiver iniciado, você deverá iniciá-lo agora para habilitar os Serviços do Excel para encaminhar solicitações autenticadas ao Serviço do Sistema PowerPivot.  
  
1.  Na Administração Central, em Configurações do Sistema, clique em **Gerenciar serviços no servidor**.  
  
2.  Inicie as Reivindicações para o Windows Token Service.  
  
3.  Inicie os Serviços de Cálculo do Excel.  
  
4.  Inicie o Serviço de Repositório Seguro.  
  
5.  Verifique se o SQL Server Analysis Services e o Serviço de Sistema PowerPivot do SQL Server foram iniciados.  
  
##  <a name="createapp"></a> Etapa 3: Criar um aplicativo de serviço PowerPivot  
 A próxima etapa é criar um aplicativo de serviço PowerPivot.  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Na faixa de opções **Aplicativos de Serviço** , clique em **Novo**.  
  
3.  Selecione **aplicativo de serviço PowerPivot do SQL Server**. Se ele não aparecer na lista, o PowerPivot para SharePoint não estará instalado ou a solução não estará implantada.  
  
4.  No **criar novo aplicativo de serviço PowerPivot** página, insira um nome para o aplicativo. O padrão é PowerPivotServiceApplication\<número >. Se você estiver criando vários aplicativos de serviço PowerPivot, um nome descritivo ajudará outros administradores a entender como o aplicativo é usado.  
  
5.  Em Pool de Aplicativos, crie um novo pool de aplicativos e selecione uma conta de segurança para ele. Uma conta de usuário de domínio é necessária.  
  
6.  Na **servidor de banco de dados**, escolha um servidor de banco de dados no qual criar o banco de dados do aplicativo de serviço. O valor padrão é a instância de Mecanismo de Banco de Dados do SQL Server que hospeda os bancos de dados de configuração de farm.  
  
7.  Na **nome do banco de dados**, o valor padrão é PowerPivotServiceApplication1_\<guid >. O nome do banco de dados padrão corresponde ao nome padrão do aplicativo de serviço. Se você inseriu um nome de aplicativo de serviço exclusivo, siga uma convenção de nomenclatura semelhante para seu nome de banco de dados de forma que você possa gerenciá-los em conjunto.  
  
8.  Em **Autenticação de Banco de dados**, o padrão é Autenticação do Windows. Se você escolher **Autenticação SQL**, consulte o guia de práticas recomendadas do administrador do SharePoint para saber como usar esse tipo de autenticação em uma implantação do SharePoint.  
  
9. Selecione a caixa de seleção **adicionar o proxy para este aplicativo de serviço PowerPivot ao grupo proxy padrão.** . Esse procedimento adiciona a conexão de aplicativo de serviço ao grupo de conexões de serviço padrão. Você precisa ter pelo menos um aplicativo de serviço PowerPivot no grupo de conexões padrão.  
  
     Se um aplicativo de serviço PowerPivot já estiver listado no grupo de conexões padrão, não adicione um segundo aplicativo de serviço a esse grupo. A adição de dois aplicativos de serviço do mesmo tipo do grupo de conexões padrão não é uma configuração com suporte. Para obter mais informações sobre como usar aplicativos de serviço adicionais em um grupo de conexão, consulte [conectar um aplicativo de serviço do PowerPivot a um aplicativo Web do SharePoint na Administração Central](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md).  
  
10. Clique em **OK.** O serviço aparecerá ao lado de outros serviços gerenciados na lista de aplicativos de serviço do farm.  
  
##  <a name="ExcelServ"></a> Etapa 4: Habilitar Serviços do Excel  
 O PowerPivot para SharePoint exige os Serviços do Excel para dar suporte ao acesso a dados PowerPivot no farm. Você pode determinar se os Serviços do Excel já estão habilitados confirmando se o Aplicativo de Serviços do Excel aparece na lista de aplicativos de serviço na Administração Central. Se os Serviços do Excel não estiverem listados, siga estas etapas para habilitá-los agora.  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Na faixa de opções Aplicativos de Serviço, em Criar, clique em **Novo**.  
  
3.  Selecione **aplicativo de serviços do Excel**.  
  
4.  Em Criar Novo Aplicativo de Serviços do Excel, especifique um nome (por exemplo, Aplicativo de Serviços do Excel).  
  
5.  Em Pool de Aplicativos, selecione Criar novo pool de aplicativos e atribua um nome descritivo (por exemplo, Pool de Aplicativos de Serviços do Excel).  
  
6.  Em Configurável, selecione uma conta de usuário de domínio do Windows para essa identidade de pool de aplicativos.  
  
7.  Mantenha a caixa de seleção padrão que adiciona o proxy do aplicativo de serviço à lista padrão de conexões de serviço.  
  
8.  Clique em **OK**.  
  
9. Clique no aplicativo de Serviços do Excel recém-criado.  
  
10. Clique em **locais de arquivos confiáveis** e nesta página, selecione seu local confiável. (Normalmente, isso é listado como **http://** na coluna endereço.) Para assegurar que os Serviços do Excel e o serviço PowerPivot tenham acesso à pasta de trabalho, você deve incluir o SharePoint como um local confiável dos Serviços do Excel. O Serviço do Sistema PowerPivot não pode acessar pastas de trabalho que estão armazenadas fora de um farm do SharePoint.  
  
11. Na área propriedades da pasta de trabalho, defina **tamanho máximo da pasta de trabalho** como 50.  
  
12. Em dados externos, defina **permitir dados externos** à **bibliotecas de conexão de dados confiáveis e incorporadas**. Essa configuração é necessária para o acesso a dados PowerPivot em uma pasta de trabalho.  
  
13. Desmarque a **Avisar ao atualizar dados** caixa de seleção para permitir imagens de visualização de planilhas individuais na Galeria PowerPivot. Se você optar por manter o aviso e as configurações de pasta de trabalho especificarem a atualização na abertura, talvez você obtenha uma única imagem de visualização do aviso em vez das páginas em sua pasta de trabalho.  
  
14. Clique em **OK**.  
  
##  <a name="SSS"></a> Etapa 5: Habilitar o Serviço de Repositório Seguro e configurar a atualização de dados  
 O PowerPivot para SharePoint requer o Serviço de Repositório Seguro para armazenar credenciais e a conta de execução autônoma para a atualização de dados. Você poderá determinar se Serviço de Repositório Seguro já está habilitado confirmando se ele aparece na lista de aplicativos de serviço.  
  
> [!IMPORTANT]  
>  Se o Serviço de Repositório Seguro estiver habilitado, você ainda deverá verificar se uma chave mestra foi gerada para ele. Para obter instruções, consulte a parte 2: Gere a chave mestra no procedimento a seguir.  
  
 Se o Serviço de Repositório Seguro não estiver listado, siga estas etapas para habilitá-lo agora. Ao habilitar o Repositório Seguro, autores da pasta de trabalho e proprietários do documento podem acessar um intervalo mais amplo de opções de conexão da fonte de dados ao agendar a atualização de dados para suas pastas de trabalho publicadas.  
  
##### <a name="part-1-enable-secure-store-service"></a>Parte 1: Habilitar o Serviço de Repositório Seguro  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Na faixa de opções Aplicativos de Serviço, em Criar, clique em **Novo**.  
  
3.  Selecione **Serviço de Repositório Seguro**.  
  
4.  Na página **Criar Aplicativo de Repositório Seguro** , insira um nome para o aplicativo.  
  
5.  Em **Banco de Dados**, especifique a instância do SQL Server que hospedará o banco de dados para este aplicativo de serviço. O valor padrão é a instância de Mecanismo de Banco de Dados do SQL Server que hospeda os bancos de dados de configuração de farm.  
  
6.  Em **Nome do Banco de Dados**, insira o nome do banco de dados de aplicativo de serviço. O valor padrão é Secure_Store_Service_DB_\<guid >. O nome padrão corresponde ao nome padrão do aplicativo de serviço. Se você inseriu um nome de aplicativo de serviço exclusivo, siga uma convenção de nomenclatura semelhante para seu nome de banco de dados de forma que você possa gerenciá-los em conjunto.  
  
7.  Em **Autenticação de Banco de dados**, o padrão é Autenticação do Windows. Se você escolher Autenticação SQL, consulte o guia do administrador do SharePoint para saber como usar o tipo de autenticação no farm.  
  
8.  No Pool de Aplicativos, selecione **Criar novo pool de aplicativos** . Especifique um nome descritivo que ajudará outros administradores do servidor a identificar como o pool de aplicativos é usado.  
  
9. Selecione uma conta de segurança para o pool de aplicativos. Especifique uma conta gerenciada para usar uma conta de usuário de domínio.  
  
10. Aceite os valores padrão restantes e clique em **OK.** O aplicativo de serviço aparecerá ao lado de outros serviços gerenciados na lista de aplicativos de serviço do farm.  
  
##### <a name="part-2-generate-the-master-key"></a>Parte 2: Gerar a chave mestra  
  
1.  Clique no aplicativo de Serviço de Repositório Seguro na lista.  
  
2.  Na faixa de opções Aplicativos de Serviço, clique em **Gerenciar**.  
  
3.  Em Gerenciamento de Chaves, clique em **Gerar Nova Chave**.  
  
4.  Digite e confirme uma frase secreta. A frase de senha será usada para adicionar aplicativos de serviço compartilhado do repositório seguro.  
  
5.  Clique em **OK**.  
  
##### <a name="part-3-configure-the-unattended-powerpivot-data-refresh-account"></a>Parte 3: Configurar a conta de atualização de dados PowerPivot autônoma  
 Em geral, é necessário criar uma conta autônoma de atualização de dados para o acesso a dados PowerPivot para o acesso a dados externo durante a atualização de dados. Por exemplo, se o Kerberos não estiver habilitado, você deverá criar uma conta autônoma que o serviço PowerPivot possa usar para se conectar a fontes de dados externas.  
  
 Para obter instruções sobre como criar os dados PowerPivot autônomos de atualização conta ou outras credenciais armazenadas que são usados na atualização de dados, consulte [configurar a conta autônoma PowerPivot Data Refresh &#40;PowerPivot para SharePoint&#41; ](../../analysis-services/configure-unattended-data-refresh-account-powerpivot-sharepoint.md) e [configurar credenciais armazenadas para atualização de dados PowerPivot &#40;o PowerPivot para SharePoint&#41;](../../../2014/analysis-services/configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
##  <a name="Usage"></a> Etapa 6: Habilitar a coleta de dados de uso  
 O PowerPivot para SharePoint usa a infraestrutura da coleção de dados de uso do SharePoint para obter informações sobre o uso do PowerPivot em todo o farm. Embora os dados de uso sempre façam parte de uma instalação do SharePoint, talvez seja necessário habilitá-los para que possam ser usados. Para obter instruções, consulte [configurar a coleta de dados de uso para &#40;PowerPivot para SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md).  
  
##  <a name="Upload"></a> Etapa 7: Aumentar o tamanho de carregamento máximo para aplicativos Web do SharePoint e Serviços do Excel  
 Como as pastas de trabalho PowerPivot podem ser grandes, você pode aumentar o tamanho de arquivo máximo. Há duas configurações de tamanho do arquivo para configurar: Tamanho máximo do carregamento para o aplicativo Web e tamanho máximo da pasta de trabalho nos serviços do Excel. O tamanho de arquivo máximo deve ser definido para o mesmo valor em ambos os aplicativos. Para obter instruções, consulte [configurar o tamanho máximo do arquivo de carregamento &#40;PowerPivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).  
  
##  <a name="activatePP"></a> Etapa 8: Ativar a integração de recursos do PowerPivot para conjuntos de sites  
 A ativação de recursos em nível de coleção de sites disponibiliza as páginas de aplicativos e os modelos em seus sites, incluindo páginas de configuração para atualização de dados agendada e páginas de aplicativo para Galeria do PowerPivot e bibliotecas de Feed de Dados.  
  
1.  Em um site do SharePoint, clique em **Ações do Site**.  
  
     Por padrão, os aplicativos Web do SharePoint são acessados pela porta 80. Isso significa que você pode acessar frequentemente um site do SharePoint inserindo http://\<nome do computador > para abrir o conjunto de sites raiz.  
  
2.  Clique em **Configurações de Site**.  
  
3.  Em Administração do Conjunto de Sites, clique em **Recursos do conjunto de sites**.  
  
4.  Role a página até encontrar **recurso de coleção de sites de integração do PowerPivot**.  
  
5.  Clique em **Ativar**.  
  
6.  Repita a operação em outros conjuntos de sites, abrindo cada site e clicando em **Ações do Site**.  
  
 Para obter mais informações, consulte [ativar a integração do recurso do PowerPivot para coleções de sites na Administração Central](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md).  
  
##  <a name="bkmk_redist"></a> Etapa 9: Instale a versão SQL Server 2008 R2 do provedor OLE DB em uma instância do SQL Server 2012 PowerPivot para SharePoint  
 Se você desejar executar versões mais antigas e mais novas de pastas de trabalho PowerPivot lado a lado no mesmo servidor, instale o provedor OLE DB do Analysis Services que acompanha o SQL Server 2008 R2 em um servidor do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot para SharePoint.  
  
 A instalação do provedor permite que as pastas de trabalho que referenciam o MSOLAP.4 na cadeia de conexão de dados funcionem como esperado em um servidor PowerPivot do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. A instalação do provedor OLE DB do SQL Server 2008 R2 é uma abordagem alternativa para atualizar pastas de trabalho criadas em uma versão anterior do PowerPivot para Excel.  
  
 Você pode baixar o provedor do [página do SQL Server 2008 R2 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=159570). Procure **Microsoft® Analysis Services OLE DB Provider para Microsoft® SQL Server® 2008 R2**e, em seguida, baixe o x64 pacote o `SQLServer2008_ASOLEDB10.msi` programa de instalação.  
  
 Para obter mais informações sobre como instalar o provedor, incluindo as etapas de verificação, consulte [instalar o Analysis Services OLE DB Provider em SharePoint Servers](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).  
  
##  <a name="verifyinstall"></a> Etapa 10: Verificar a instalação  
 O processamento de consultas do PowerPivot no farm ocorre quando um usuário ou aplicativo abre uma pasta de trabalho do Excel que contém dados PowerPivot. No mínimo, você pode verificar se páginas de sites do SharePoint contêm recursos do PowerPivot disponíveis. No entanto, para verificar integralmente uma instalação, você deve ter uma pasta de trabalho PowerPivot que possa publicar no SharePoint e acessar em uma biblioteca. Para fins de teste, é possível publicar uma pasta de trabalho de exemplo que já contenha os dados PowerPivot e usá-la para confirmar se essa integração com o SharePoint está configurada corretamente.  
  
 Para verificar a integração do PowerPivot com um site do SharePoint, faça o seguinte:  
  
1.  Em um navegador, abra o aplicativo Web criado. Se você usou valores padrão, você pode especificar http://\<o nome do computador > no endereço da URL.  
  
2.  Verifique se os recursos de acesso aos dados e de processamento do PowerPivot estão disponíveis no aplicativo. É possível fazer isso verificando a presença de modelos de biblioteca fornecidos pelo PowerPivot:  
  
    1.  Em ações do Site, clique em **mais opções...** .  
  
    2.  Em bibliotecas, você deve ver **biblioteca de Feed de dados** e **Galeria PowerPivot**. Esses modelos de biblioteca são fornecidos pelo recurso do PowerPivot, estando visíveis na lista Bibliotecas apenas se o recurso estiver integrado corretamente.  
  
 Para verificar o acesso a dados PowerPivot no servidor, faça o seguinte:  
  
1.  Carregue uma pasta de trabalho PowerPivot na Galeria PowerPivot ou em qualquer biblioteca do SharePoint.  
  
2.  Clique no documento para abri-lo na biblioteca.  
  
3.  Clique em uma segmentação de dados ou filtre os dados para iniciar uma consulta do PowerPivot. O servidor carregará dados PowerPivot em segundo plano e retornará os resultados. Na próxima etapa, você se conectará ao servidor para verificar se os dados foram carregados e armazenados em cache.  
  
4.  Inicie o SQL Server Management Studio no grupo de programas Microsoft SQL Server 2008 R2 no menu Iniciar. Se essa ferramenta não estiver instalada no servidor, será possível passar à última etapa para confirmar a presença de arquivos armazenados em cache.  
  
5.  Em Tipo de Servidor, selecione **Analysis Services**.  
  
6.  Em nome do servidor, digite  **\<server-name > \powerpivot.**, onde  **\<nome do servidor >** é o nome do computador que tem a instalação do PowerPivot para SharePoint.  
  
7.  Clique em **Conectar**.  
  
8.  No Pesquisador de objetos, clique em **bancos de dados** para exibir a lista de arquivos de dados do PowerPivot que são carregados.  
  
9. No sistema de arquivos do computador, verifique a pasta a seguir para determinar se os arquivos estão armazenados no cache em disco. A presença de arquivos armazenados em cache é a verificação adicional de que a implantação é operacional. Para exibir o cache de arquivos, vá até a pasta \Arquivos de programas\Microsoft SQL Server\MSAS10_50.POWERPIVOT\OLAP\Backup.  
  
##  <a name="nextsteps"></a> Etapas pós-instalação  
 Depois que você verificar a instalação, conclua a configuração do serviço criando uma Galeria PowerPivot ou ajustando parâmetros de configuração individuais. Para usar integralmente os componentes do servidor recém-instalados, você pode baixar o [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] para criar e publicar sua primeira pasta de trabalho PowerPivot.  
  
### <a name="install-data-providers-used-for-data-refresh"></a>Instalar provedores de dados usados para atualização de dados  
 Se você habilitou a atualização de dados, o servidor precisará dos mesmos provedores de dados para acesso externo a dados que foram usados pelo aplicativo cliente PowerPivot para importar os dados originais (por exemplo, se os dados foram originalmente importados usando um provedor de 32 bits, a atualização de dados do servidor também exigirá o provedor de 32 bits quando acessar a mesma fonte de dados externa). Para obter mais informações, consulte [atualização de dados do PowerPivot com SharePoint 2010](../../../2014/analysis-services/powerpivot-data-refresh-with-sharepoint-2010.md).  
  
### <a name="install-adonet-data-services"></a>Instalar o ADO.NET Data Services  
 Você deverá instalar o ADO.NET Data Services 3.5 SP1 se desejar exportar listas do SharePoint como feeds de dados. Para obter instruções, consulte [exportações das listas do SharePoint do feed de instalar o ADO.NET Data Services para dar suporte a dados](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md).  
  
### <a name="create-a-powerpivot-gallery"></a>Criar uma Galeria PowerPivot  
 A Galeria PowerPivot é uma biblioteca que inclui opções de visualização e apresentação para exibir pastas de trabalho PowerPivot em um site do SharePoint. Recomenda-se usar a Galeria PowerPivot para publicar e exibir pastas de trabalho do PowerPivot em função do seu recurso de visualização. Além disso, se você também implantou o Reporting Services no mesmo servidor do SharePoint, uma Galeria PowerPivot permitirá a facilidade de uso na criação de relatórios. Você pode iniciar o Construtor de Relatórios a partir da Galeria PowerPivot para basear um novo relatório em uma pasta de trabalho publicada do PowerPivot. Para obter mais informações sobre como criar e usar a biblioteca, consulte [criar e personalizar a Galeria PowerPivot](../../analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery.md) e [usar a Galeria PowerPivot](../../analysis-services/power-pivot-sharepoint/use-power-pivot-gallery.md).  
  
### <a name="create-additional-trusted-sites-in-excel-services"></a>Crie sites de confiança adicionais nos Serviços do Excel  
 Você pode adicionar sites de confiança nos Serviços do Excel para variar as permissões e os parâmetros de configuração em sites que fornecem pastas de trabalho do Excel e dados PowerPivot. Para obter mais informações, consulte [criar um local confiável para sites do PowerPivot na Administração Central](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
### <a name="tune-configuration-settings"></a>Ajustar definições de configuração  
 Um aplicativo do serviço PowerPivot é criado usando propriedades e valores padrão. Você pode modificar parâmetros de configuração para aplicativos de serviço individuais para alterar a metodologia pela qual solicitações são alocadas, definir tempos limite de servidor, alterar os limites para eventos de relatório de resposta de consulta ou especificar por quanto tempo os dados de uso são retidos. Para obter mais informações sobre a configuração na Administração Central ou sobre como usar recursos do PowerPivot em aplicativos Web do SharePoint, consulte [administração de servidor do PowerPivot e a configuração na Administração Central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md).  
  
### <a name="install-powerpivot-for-excel-and-build-a-powerpivot-workbook"></a>Instalar o PowerPivot para Excel e criar uma pasta de trabalho PowerPivot  
 Depois de instalar os componentes do servidor em um farm, você poderá criar sua primeira pasta de trabalho do Excel 2010 que usa os dados PowerPivot inseridos e, em seguida, publicá-la em uma biblioteca do SharePoint em um aplicativo Web. Para criar pastas de trabalho do Excel que incluam dados do PowerPivot, você deve iniciar uma instalação do Excel 2010, seguida do suplemento PowerPivot para Excel que estende o Excel para dar suporte à importação e ao enriquecimento de dados do PowerPivot.  
  
### <a name="add-servers-or-applications"></a>Adicionar servidores ou aplicativos  
 Quando você implanta a solução PowerPivot, a integração de recursos é ativada no nível de coleção de sites para todas as coleções de sites no aplicativo Web. À medida que você criar novos aplicativos Web ao longo do tempo, deverá implantar a solução powerpivotwebapp para cada um deles. Para obter instruções, consulte [implantar soluções do PowerPivot para SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md).  
  
 Dependendo de como você configurar o aplicativo de serviço PowerPivot, o Serviço do Sistema PowerPivot será adicionado ao grupo de conexões padrão, tornando-o disponível para todos os aplicativos Web que usam conexões padrão. Entretanto, se você tiver configurado seus aplicativos Web para usarem listas personalizadas de conexões de aplicativos de serviço, deverá adicionar o aplicativo de serviço PowerPivot a cada aplicativo Web SharePoint para o qual deseja habilitar o processamento de dados PowerPivot. Para obter mais informações, consulte [conectar um aplicativo de serviço do PowerPivot a um aplicativo Web do SharePoint na Administração Central](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md).  
  
 Com o tempo, se você determinar a necessidade de armazenamento de dados e recursos de processamento adicionais, poderá adicionar uma segunda instância do servidor PowerPivot para SharePoint ao farm. O processo de instalação é quase idêntico às etapas que você seguiu para adicionar o primeiro servidor, com exceção dos requisitos sobre como especificar nomes de instância e informações de conta de serviço. Para obter instruções, consulte [lista de verificação de implantação: Expansão adicionando servidores do PowerPivot a um farm do SharePoint 2010](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md).  
  
## <a name="see-also"></a>Consulte também  
 [Recursos com suporte nas edições do SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Configurar contas de serviço PowerPivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [Criar e configurar um aplicativo de serviço PowerPivot na Administração Central](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)   
 [Implantar soluções do PowerPivot para SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)   
 [Ativar a integração de recursos do PowerPivot para coleções de sites na Administração Central](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)   
 [Instalação do PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
