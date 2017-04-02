---
title: "Implantar projetos no Servidor do Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6e9402f4-4d50-49ff-820d-65a77829c4a5
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Implantar projetos no Servidor do Integration Services
  Na versão atual do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você pode implantar seus projetos no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . O servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite gerenciar pacotes, executar pacotes, e configura valores de tempo de execução para pacotes por meio de ambientes.  
  
 Para obter mais informações sobre ambientes, consulte [Criar e mapear um ambiente de servidor](../../integration-services/packages/create-and-map-a-server-environment.md).  
  
> [!NOTE]  
>  Como nas versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], na versão atual você também pode implantar seus pacotes em uma instância do SQL Server e usar o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para executar e gerenciar os pacotes. Você usa o modelo de implantação de pacote. Para obter mais informações, consulte [Implantação de pacote herdado &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).  
  
 Para implantar um projeto no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , conclua as tarefas a seguir:  
  
1.  Criar um catálogo do SSISDB, se ainda não tiver criado. Para obter mais informações, consulte [Criar o catálogo SSIS](../../integration-services/service/create-the-ssis-catalog.md).  
  
2.  Converta o projeto no modelo de implantação de projeto executando o **Assistente de Conversão de Projeto do Integration Services** . Para obter mais informações, consulte as instruções abaixo: [Para converter um projeto no modelo de implantação de projeto](#convert).  
  
    -   Se você criou o projeto no [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)], por padrão o projeto usará o modelo de implantação de projeto.  
  
    -   Se você criou o projeto em uma versão anterior do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], depois que abrir o arquivo de projeto no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], converta o projeto no modelo de implantação de projeto.  
  
        > [!NOTE]  
        >  Se o projeto contiver uma ou mais fontes de dados, as fontes de dados serão removidas quando a conversão de projeto estiver concluída. Para criar uma conexão com uma fonte de dados que pode ser compartilhada pelos pacotes no projeto, adicione um gerenciador de conexões no nível de projeto. Para obter mais informações, consulte [Add, Delete, or Share a Connection Manager in a Package](../Topic/Add,%20Delete,%20or%20Share%20a%20Connection%20Manager%20in%20a%20Package.md).  
  
         Dependendo em se você executa o **Assistente de Conversão de Projeto do Integration Services** no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ou no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o assistente executa tarefas de conversão diferentes.  
  
        -   Se você executar o assistente de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], os pacotes contidos no projeto serão convertidos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 2005, 2008 ou 2008 R2 no formato usado pela versão atual do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. O projeto original (.dtproj) e os arquivos de pacotes (.dtsx) são atualizados.  
  
        -   Se você executar o assistente de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ele gerará um arquivo de implantação de projeto (.ispac) de pacotes e configurações contidos no projeto. Os arquivos de pacote original (.dtsx) não são atualizados.  
  
             Você pode selecionar um arquivo existente ou criar um novo arquivo, na página **Destino de Seleção** do assistente.  
  
             Para atualizar arquivos de pacotes quando um projeto é convertido, execute o **Assistente de Conversão de Projeto do Integration Services** de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Para atualizar os arquivos de pacotes separadamente de uma conversão de projeto, execute o **Assistente de Conversão de Projeto do Integration Services** do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e, em seguida, execute o **Assistente de Atualização de Pacotes SSIS**. Se você atualizar os arquivos de pacotes separadamente, verifique se você salvou as alterações. Caso contrário, quando você converter o projeto no modelo de implantação de projeto, todas as alterações não salvas no pacote não serão convertidas.  
  
     Para obter mais informações sobre a atualização de pacotes, consulte [Atualizar pacotes do Integration Services](../../integration-services/install-windows/upgrade-integration-services-packages.md) e [Atualizar pacotes do Integration Services usando o Assistente de Atualização de Pacote SSIS](../../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md).  
  
3.  Implante o projeto no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações, consulte as instruções abaixo: [Para implantar um projeto no Servidor do Integration Services](#deploy).  
  
4.  (Opcional) Crie um ambiente para o projeto implantado. Para obter mais informações, consulte [Criar e mapear um ambiente de servidor](../../integration-services/packages/create-and-map-a-server-environment.md).  
  
##  <a name="convert"></a> Para converter um projeto no modelo de implantação de projeto  
  
1.  Abra o projeto no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e, no Gerenciador de Soluções, clique com o botão direito do mouse no projeto e clique em **Converter em Modelo de Implantação de Projeto**.  
  
     -ou-  
  
     No Pesquisador de Objetos, no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], clique com o botão direito do mouse no nó **Projetos** e selecione **Importar Pacotes**.  
  
2.  Conclua o assistente. Para obter mais informações, consulte [Integration Services Project Conversion Wizard](../../integration-services/packages/integration-services-project-conversion-wizard.md).  
  
##  <a name="deploy"></a> Para implantar um projeto no Servidor do Integration Services  
  
1.  Abra o projeto no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]e, em seguida, no menu **Projeto** , selecione **Implantar** para implantar o **Assistente de Implantação do Integration Services**.  
  
     -ou-  
  
     No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] > **SSISDB** no Pesquisador de Objetos e localize a pasta Projetos do projeto que você deseja implantar. Clique com o botão direito do mouse na pasta **Projetos** e clique em **Implantar Projeto**.  
  
     -ou-  
  
     No prompt de comando, execute **isdeploymentwizard.exe** de **%ProgramFiles%\Microsoft SQL Server\110\DTS\Binn**. Em computadores de 64 bits, há também uma versão de 32 bits da ferramenta em **%ProgramFiles(x86)%\Microsoft SQL Server\100\DTS\Binn**.  
  
2.  Na página **Selecionar Origem** , clique em **Arquivo de implantação de projeto** para selecionar o arquivo de implantação do projeto.  
  
     -Ou-  
  
     Clique em **Catálogo do Integration Services** para selecionar um projeto que já foi implantado no catálogo do SSISDB.  
  
3.  Conclua o assistente. Para obter mais informações, consulte [Integration Services Deployment Wizard](../../integration-services/packages/integration-services-deployment-wizard.md).  
  
  