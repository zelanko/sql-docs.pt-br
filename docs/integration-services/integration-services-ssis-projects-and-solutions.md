---
title: Projetos e soluções do SSIS (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.importprojectwizard.f1
helpviewer_keywords:
- projects [Integration Services], creating
- folders [Integration Services], projects
- files [Integration Services], projects
- folders [Integration Services]
- projects [Integration Services], about projects
ms.assetid: 28ea8120-0a79-4029-93f0-07d521b32bee
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9f74f80b4d20f3314184d8fba891632f2aaa1d82
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47703244"
---
# <a name="integration-services-ssis-projects-and-solutions"></a>Projetos e soluções do Integration Services (SSIS)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornece o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para o desenvolvimento de pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
Os pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] residem em projetos. Para criar e trabalhar com projetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , você deve instalar o ambiente do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] . Para obter mais informações, consulte [Instalar o Integration Services](../integration-services/install-windows/install-integration-services.md).  
  
 Quando você cria um novo projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], a caixa de diálogo **Novo Projeto** inclui um modelo do **Integration Services Project** . Este modelo de projeto cria um novo projeto que contém um único pacote.  
  
## <a name="projects-and-solutions"></a>Projetos e Soluções  
 Projetos são armazenados em soluções. Você pode primeiro criar uma solução e, então, adicionar um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] à solução. Se não existir uma solução, ela será criada automaticamente pelo [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] quando o projeto for criado pela primeira vez. Uma solução pode conter vários projetos de tipos diferentes.  
  
> [!TIP]  
>  Por padrão, quando você cria um novo projeto no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], a solução não é mostrada no painel **Gerenciador de Soluções**. Para alterar este comportamento padrão, no menu **Ferramentas** , clique em **Opções**. Na caixa de diálogo **Opções** , expanda **Projetos e Soluções**e clique em **Geral**. Na página **Geral** , selecione **Sempre mostrar solução**.  

## <a name="solutions-contain-projects"></a>As soluções contêm projetos  
 Uma solução é um contêiner que agrupa e gerencia os projetos que você usa quando desenvolve soluções empresariais completas. Uma solução permite que você manipule vários projetos como uma unidade e una um ou mais projetos relacionados que contribuam para uma solução empresarial.  
  
 Soluções podem incluir diferentes tipos de projetos. Se você quiser usar o [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer para criar um pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , trabalhe em um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em uma solução fornecida por [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Quando você cria uma nova solução, o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] adiciona uma pasta Solução ao Gerenciador de Soluções e cria arquivos que têm extensões .sln e .suo.  
  
-   O arquivo * .sln contém informações sobre as configurações da solução e lista os projetos na solução.  
  
-   O arquivo *.suo contém informações sobre suas preferências para trabalhar com a solução.  
  
 Embora o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] crie automaticamente uma solução quando um novo projeto é criado, você também pode criar uma solução em branco e então adicionar projetos depois.  
   
## <a name="integration-services-projects-contain-packages"></a>Projetos do Integration Services contêm pacotes  
 Um projeto é um contêiner no qual você desenvolve pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] armazena e agrupa os arquivos que são relacionados ao pacote. Por exemplo, um projeto inclui os arquivos necessários para criar uma solução de ETL (extração, transferência e carregamento) específica.  
  
 Antes de você criar um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , familiarize-se com o conteúdo básico deste tipo de projeto. Depois de entender o que um projeto contém, você pode começar a criar e trabalhar com um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="folders-in-integration-services-projects"></a>Pastas nos projetos do Integration Services  
 O diagrama a seguir mostra as pastas em um projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 ![Pastas em um projeto do Integration Services](../integration-services/media/solutionexplorer.gif "Pastas em um projeto do Integration Services")  
  
 A tabela a seguir descreve as pastas que aparecem em um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
|Pasta|Descrição|  
|------------|-----------------|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)] Packages|Contém pacotes. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Pacotes](../integration-services/integration-services-ssis-packages.md).|  
|Diversos|Contém arquivos diferentes de arquivos de pacotes.|  
  
## <a name="files-in-integration-services-projects"></a>Arquivos em projetos do Integration Services  
 Ao adicionar um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] novo ou existente a uma solução, o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] cria arquivos de projeto que têm extensões .dtproj e .dtproj.user e .database.  
  
-   O arquivo *.dtproj contém informações sobre configurações de projeto e itens como pacotes.  
  
-   O arquivo * .dtproj.user contém informações sobre suas preferências para trabalhar com o projeto  
  
-   O arquivo * .database contém informações que o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] exige abrir o projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="version-targeting-in-integration-services-projects"></a>Direcionamento de versão nos projetos do Integration Services  
 No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], você pode criar, manter e executar pacotes que se destinam ao SQL Server 2016, SQL Server 2014 ou SQL Server 2012.  
  
 No Gerenciador de Soluções, clique com o botão direito do mouse em um projeto do Integration Services e selecione **Propriedades** para abrir as páginas de propriedades do projeto. Na guia **Geral** de **Propriedades de Configuração**, selecione a propriedade **TargetServerVersion** e, em seguida, escolha o SQL Server 2012, SQL Server 2014 ou SQL Server 2016.  
  
 ![Propriedade TargetServerVersion na caixa de diálogo de propriedades do projeto](../integration-services/media/targetserverversion2.png "Propriedade TargetServerVersion na caixa de diálogo de propriedades do projeto")  
 
## <a name="create-a-new-integration-services-project"></a>Criar um novo projeto do Integration Services  
  
1.  Abra o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  No menu **Arquivo** , aponte para **Novo**e clique em **Projeto**.  
  
3.  Na caixa de diálogo **Novo Projeto**, no painel **Modelos**, selecione o modelo **Projeto do Integration Services**.  
  
     O modelo **Projeto do Integration Services** cria um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém um único pacote vazio.  
  
4.  (Opcional) Edite o nome do projeto e o local.  
  
     O nome da solução é automaticamente atualizado para corresponder ao nome do projeto.  
  
5.  Para criar uma pasta separada para o arquivo de solução, selecione **Criar diretório para solução**. Essa é a opção padrão.  
  
6.  Se o software de controle do código-fonte estiver instalado no computador, selecione **Adicionar ao controle do código-fonte** para associar o projeto ao controle do código-fonte.  
  
7.  Se o software de controle do código-fonte for o [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe, a caixa de diálogo **Logon do Visual SourceSafe** será aberta. Em **Logon do Visual SourceSafe**, forneça um nome de usuário, uma senha e o nome do banco de dados do [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe. Clique em **Procurar** para localizar o banco de dados.  
  
    > **OBSERVAÇÃO:** para exibir e alterar o plug-in de controle do código-fonte selecionado e configurar o ambiente de controle do código-fonte, clique em **Opções** no menu **Ferramentas** e expanda o nó **Controle do Código-fonte**.  
  
8.  Clique em **OK** para adicionar a solução ao **Gerenciador de Soluções** e adicionar o projeto à solução.  
  
## <a name="choose-the-target-version-of-a-project-and-its-packages"></a>Escolher a versão de destino de um projeto e seus pacotes  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse em um projeto do Integration Services e selecione **Propriedades** para abrir as páginas de propriedades do projeto.  
  
2.  Na guia **Geral** de **Propriedades de Configuração**, selecione a propriedade **TargetServerVersion** e, em seguida, escolha o SQL Server 2012, SQL Server 2014 ou SQL Server 2016.  
  
     ![Propriedade TargetServerVersion na caixa de diálogo de propriedades do projeto](../integration-services/media/targetserverversion2.png "Propriedade TargetServerVersion na caixa de diálogo de propriedades do projeto")  
  
 Você pode criar, manter e executar pacotes que se destinam ao SQL Server 2016, SQL Server 2014 ou SQL Server 2012.  

## <a name="import-an-existing-project-with-the-import-project-wizard"></a>Importar um projeto existente com o Assistente para Importação de Projeto
  
1.  No [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], clique em **Novo** > **Projeto** no menu **Arquivo** .  
  
2.  Na área **Modelos Instalados** da janela **Novo Projeto** , expanda **Business Intelligence**e clique em **Integration Services**.  
  
3.  Selecione **Assistente de Importação de Projeto do Integration Services** da lista de tipos de projetos.  
  
4.  Digite o nome do novo projeto a ser criado na caixa de texto **Nome** .  
  
5.  Digite o caminho ou o local para o projeto na caixa de texto **Localização** ou clique em **Procurar** para selecionar um.  
  
6.  Digite um nome para a solução na caixa de texto **Nome da solução** .  
  
7.  Clique em **OK** para iniciar a caixa de diálogo **Assistente de Importação de Projeto do Integration Services** .  
  
8.  Clique em **Avançar** para alternar para a página **Selecionar Origem** .  
  
9. Se você estiver importando de um arquivo **.ispac** , digite o caminho incluindo o nome de arquivo na caixa de texto **Caminho** . Clique em **Procurar** para navegar até a pasta onde você deseja que a solução seja armazenada e digite o nome do arquivo na caixa de texto **Nome de arquivo** e clique em **Abrir**.  
  
     Se você estiver importando de um **Catálogo do Integration Services**, digite o nome da instância de banco de dados na caixa de texto **Nome do servidor** ou clique em **Procurar** e selecione a instância de banco de dados que contém o catálogo.  
  
     Clique em **Procurar** ao lado da caixa de texto **Caminho** , expanda a pasta no catálogo, selecione o projeto que você deseja importar e clique em **OK**.  
  
     Clique em **Avançar** para alternar para a página **Revisar** .  
  
10. Revise as informações e clique em **Importar** para criar um projeto baseado no projeto existente que você selecionou.  
  
11. Opcional: clique em **Salvar Relatório** para salvar os resultados em um arquivo  
  
12. Clique em **Fechar** para fechar a caixa de diálogo **Assistente de Importação de Projeto do Integration Services** .  

## <a name="add-a-project-to-a-solution"></a>Adicionar um projeto a uma solução 
 Ao adicionar um projeto, você pode deixar que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] crie um novo projeto em branco ou pode adicionar um projeto que já tenha sido criado em outra solução. Você só pode adicionar um projeto a uma solução existente quando a solução estiver visível em [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
### <a name="add-a-new-project-to-a-solution"></a>Adicionar um novo projeto a uma solução  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra a solução à qual deseja adicionar um novo projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e siga um destes procedimentos:  
  
    -   Clique com o botão direito do mouse na solução, escolha **Adicionar** e clique em **Novo Projeto**.  
  
    -   No menu **Arquivo**, aponte para **Adicionar** e clique em **Novo Projeto**.  
  
2.  Na caixa de diálogo **Adicionar Novo Projeto**, clique em **Projeto do Integration Services** no painel **Modelos**.  
  
3.  Se preferir, edite o nome e o local do projeto.  
  
4.  Clique em **OK**.  
  
### <a name="add-an-existing-project-to-a-solution"></a>Adicionar um projeto existente a uma solução  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra a solução à qual deseja adicionar um projeto existente do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e siga um destes procedimentos:  
  
    -   Clique com o botão direito do mouse na solução, aponte a **Adicionar** e escolha **Projeto Existente**.  
  
    -   No menu **Arquivo**, clique em **Adicionar** e escolha **Projeto Existente**.  
  
2.  Na caixa de diálogo **Adicionar Projeto Existente**, navegue até o local ao qual deseja adicionar o projeto e clique em **Abrir**.  
  
3.  O projeto é adicionado à pasta da solução no **Gerenciador de Soluções**.  
  
## <a name="remove-a-project-from-a-solution"></a>Remover um projeto de uma solução
 Você só pode remover um projeto de uma solução quando a solução estiver visível em [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Assim que a solução estiver visível, você poderá remover tudo, exceto um projeto. Quando restar apenas um projeto, o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] não exibirá mais a pasta da solução e o último projeto não poderá ser removido.  
   
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra a solução da qual deseja remover um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e, em seguida, clique em **Descarregar Projeto**.  
  
3.  Clique em **OK** para confirmar a remoção.  

## <a name="add-an-item-to-a-project"></a>Adicionar um item a um projeto  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra a solução que contém o projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ao qual deseja adicionar um item.  
  
2.  Em Gerenciador de Soluções, clique com o botão direito do mouse no projeto, aponte para **Adicionar**e siga um destes procedimentos:  
  
    -   Clique em **Novo Item**e selecione um modelo no painel **Modelos** na caixa de diálogo **Adicionar Novo Item** .  
  
    -   Clique em **Item Existente**, navegue até a caixa de diálogo **Adicionar Item Existente** para localizar o item que deseja adicionar ao projeto e clique em **Adicionar**.  
  
3.  O novo item será exibido na pasta apropriada no Gerenciador de Soluções.  

## <a name="copy-project-items"></a>Copiar itens do projeto  
Você pode copiar objetos em um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ou entre projetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Você também pode copiar objetos entre os outros tipos de projetos do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] , [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para copiar entre projetos, o projeto deve fazer parte da mesma solução [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] .

1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto ou solução [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] com que deseja trabalhar.  
  
2.  Expanda o projeto e pasta de item do qual deseja copiar.  
  
3.  Clique com o botão direito do mouse no item e clique em **Copiar**.  
  
4.  Clique com o botão direito do mouse no projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] a ser copiado e clique em **Colar**.  
  
     Os itens são copiados automaticamente na pasta correta. Se você copiar itens que não são pacotes no projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , os itens serão copiados na pasta **Diversos** .  
     
