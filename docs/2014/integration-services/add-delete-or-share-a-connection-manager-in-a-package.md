---
title: Adicionar, excluir ou compartilhar um Gerenciador de Conexão em um pacote | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], adding
- adding connection managers
ms.assetid: 6f2ba4ea-10be-4c40-9e80-7efcf6ee9655
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fdcc6285ba1a75827f91f856319d296c0cbbff5d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58391684"
---
# <a name="add-delete-or-share-a-connection-manager-in-a-package"></a>Adicionar, excluir ou compartilhar um gerenciador de conexões em um pacote
  O [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui uma variedade de gerenciadores de conexões para se conectar com fontes de dados diferentes, como bancos de dados relacionais, bancos de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e arquivos nos formatos CSV e XML. Um gerenciador de conexões pode ser criado no nível de pacote ou no nível de projeto. O gerenciador de conexões criado no nível de projeto está disponível para todos os pacotes no projeto. Por outro lado, o gerenciador de conexões criado no nível de pacote está disponível para aquele pacote específico.  
  
 Use gerenciadores de conexões que são criados no nível de projeto em vez de fontes de dados, para compartilhar conexões com origens. Para adicionar um gerenciador de conexões no nível de projeto, o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] deve usar o modelo de implantação de projeto. Quando um projeto é configurado para usar este modelo, a pasta **Gerenciadores de Conexões** é exibida no **Gerenciador de Soluções**e a pasta **Fontes de Dados** é removida do **Gerenciador de Soluções**.  
  
> [!NOTE]  
>  Se você quiser usar fontes de dados em seu pacote, precisará converter o projeto para o modelo de implantação do pacote.  
>   
>  Para obter mais informações sobre os dois modelos, consulte [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md). Para obter mais informações sobre conversão de um projeto para o modelo de implantação de projetos, consulte [Deploy Projects to Integration Services Server](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
 Estes procedimentos aplicam-se a todos os tipos de gerenciadores de conexões e descrevem como realizar as seguintes tarefas:  
  
-   [Para adicionar um Gerenciador de conexão durante a criação de um pacote](#wizard)  
  
-   [Para adicionar um Gerenciador de conexão a um pacote existente](#package)  
  
-   [Para adicionar um Gerenciador de conexão no nível do projeto](#project)  
  
-   [Para criar um parâmetro para uma propriedade de Gerenciador de conexão](#parameter)  
  
-   [Para excluir um Gerenciador de conexão de um pacote](#DeletePackageLevel)  
  
-   [Para excluir um Gerenciador de conexão compartilhada (Gerenciador de conexão de nível de projeto)](#DeleteProjectLevel)  
  
##  <a name="wizard"></a> Para adicionar um Gerenciador de conexão durante a criação de um pacote  
  
-   Usar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]   
  
     Além de criar e configurar um gerenciador de conexões, o assistente também ajuda a criar e configurar origens e destinos que usam o gerenciador de conexões. Para obter mais informações, consulte [Create Packages in SQL Server Data Tools](create-packages-in-sql-server-data-tools.md).  
  
##  <a name="package"></a> Para adicionar um Gerenciador de conexão a um pacote existente  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo  
  
3.  No Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , clique na guia **Controle de Fluxo** , na guia **Fluxo de Dados** , ou na guia **Manipulador de Eventos** para disponibilizar o **Gerenciador de Conexões** .  
  
4.  Clique com o botão direito do mouse em qualquer lugar na área **Gerenciadores de Conexões** e execute uma das seguintes ações:  
  
    -   Clique no tipo de gerenciador de conexões que será adicionado ao pacote.  
  
         -ou-  
  
    -   Se o tipo que deseja adicionar não estiver listado, clique em **Nova Conexão** para abrir a caixa de diálogo **Adicionar Gerenciador de Conexões SSIS** , selecione um tipo de gerenciador de conexões e clique em **OK**.  
  
     A caixa de diálogo personalizada para o tipo de gerenciador de conexões selecionado é aberta. Para obter mais informações sobre tipos de gerenciador de conexões e as opções que estão disponíveis, consulte a tabela de opções a seguir.  
  
    |Gerenciador de conexões|Opções|  
    |------------------------|-------------|  
    |[Gerenciador de conexões ADO](connection-manager/ado-connection-manager.md)|[Configurar Gerenciador de Conexões OLE DB](configure-ole-db-connection-manager.md)|  
    |[Gerenciador de conexões ADO.NET](connection-manager/ado-net-connection-manager.md)|[Configurar Gerenciador de Conexões ADO.NET](configure-ado-net-connection-manager.md)|  
    |[Gerenciador de Conexões do Analysis Services](connection-manager/analysis-services-connection-manager.md)|[Referência de IU da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Gerenciador de Conexões do Excel](connection-manager/excel-connection-manager.md)|[Editor de Gerenciador de Conexões do Excel](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de Arquivos](connection-manager/file-connection-manager.md)|[Editor do Gerenciador de Conexões de Arquivos](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de Vários Arquivos](connection-manager/multiple-files-connection-manager.md)|[Referência de IU da caixa de diálogo Adicionar Gerenciador de Conexões de Arquivos](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Gerenciador de Conexões de Arquivos Simples](connection-manager/flat-file-connection-manager.md)|[Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Geral&#41;](general-page-of-integration-services-designers-options.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Colunas&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Avançado&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Visualização&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[Gerenciador de Conexões de Vários Arquivos Simples](connection-manager/multiple-flat-files-connection-manager.md)|[Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Geral&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Colunas&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Avançado&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Visualização&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Gerenciador de Conexões de FTP](connection-manager/ftp-connection-manager.md)|[Editor do Gerenciador de Conexões FTP](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de HTTP](connection-manager/http-connection-manager.md)|[Editor do Gerenciador de Conexões HTTP &#40;Página Servidor&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [Editor do Gerenciador de Conexões HTTP &#40;Página Proxy&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[Gerenciador de Conexões MSMQ](connection-manager/msmq-connection-manager.md)|[Editor do Gerenciador de Conexões MSMQ](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[Gerenciador de Conexões ODBC](connection-manager/odbc-connection-manager.md)|[Referência da interface do usuário do Gerenciador de Conexões ODBC](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[Gerenciador de Conexões OLE DB](connection-manager/ole-db-connection-manager.md)|[Configurar Gerenciador de Conexões OLE DB](configure-ole-db-connection-manager.md)|  
    |[Gerenciador de Conexões SMO](connection-manager/smo-connection-manager.md)|[Editor do Gerenciador de Conexões SMO](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[Gerenciador de Conexões SMTP](connection-manager/smtp-connection-manager.md)|[Editor do Gerenciador de Conexões SMTP](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[Gerenciador de Conexões do SQL Server Compact Edition](connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página de Conexão&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página Tudo&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Gerenciador de Conexões WMI](connection-manager/wmi-connection-manager.md)|[Editor do Gerenciador de Conexões WMI](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
     A área **Gerenciadores de Conexões** lista o gerenciador de conexões adicionado.  
  
5.  Como opção, clique com o botão direito do mouse no gerenciador de conexões, clique em **Renomear**e modifique o nome padrão do gerenciador de conexões.  
  
6.  Para salvar o pacote atualizado, clique em **Salvar Item Selecionado** no menu **Arquivo** .  
  
##  <a name="project"></a> Para adicionar um Gerenciador de conexão no nível do projeto  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
2.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Gerenciadores de Conexões**e clique em **Novo Gerenciador de Conexões**.  
  
3.  Na caixa de diálogo **Adicionar Gerenciador de Conexões SSIS** , selecione o tipo de gerenciador de conexões e clique em **Adicionar**.  
  
     A caixa de diálogo personalizada para o tipo de gerenciador de conexões selecionado é aberta. Para obter mais informações sobre tipos de gerenciador de conexões e as opções que estão disponíveis, consulte a tabela de opções a seguir.  
  
    |Gerenciador de conexões|Opções|  
    |------------------------|-------------|  
    |[Gerenciador de conexões ADO](connection-manager/ado-connection-manager.md)|[Configurar Gerenciador de Conexões OLE DB](configure-ole-db-connection-manager.md)|  
    |[Gerenciador de conexões ADO.NET](connection-manager/ado-net-connection-manager.md)|[Configurar Gerenciador de Conexões ADO.NET](configure-ado-net-connection-manager.md)|  
    |[Gerenciador de Conexões do Analysis Services](connection-manager/analysis-services-connection-manager.md)|[Referência de IU da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Gerenciador de Conexões do Excel](connection-manager/excel-connection-manager.md)|[Editor de Gerenciador de Conexões do Excel](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de Arquivos](connection-manager/file-connection-manager.md)|[Editor do Gerenciador de Conexões de Arquivos](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de Vários Arquivos](connection-manager/multiple-files-connection-manager.md)|[Referência de IU da caixa de diálogo Adicionar Gerenciador de Conexões de Arquivos](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Gerenciador de Conexões de Arquivos Simples](connection-manager/flat-file-connection-manager.md)|[Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Geral&#41;](general-page-of-integration-services-designers-options.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Colunas&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Avançado&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Visualização&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[Gerenciador de Conexões de Vários Arquivos Simples](connection-manager/multiple-flat-files-connection-manager.md)|[Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Geral&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Colunas&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Avançado&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Visualização&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Gerenciador de Conexões de FTP](connection-manager/ftp-connection-manager.md)|[Editor do Gerenciador de Conexões FTP](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de HTTP](connection-manager/http-connection-manager.md)|[Editor do Gerenciador de Conexões HTTP &#40;Página Servidor&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [Editor do Gerenciador de Conexões HTTP &#40;Página Proxy&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[Gerenciador de Conexões MSMQ](connection-manager/msmq-connection-manager.md)|[Editor do Gerenciador de Conexões MSMQ](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[Gerenciador de Conexões ODBC](connection-manager/odbc-connection-manager.md)|[Referência da interface do usuário do Gerenciador de Conexões ODBC](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[Gerenciador de Conexões OLE DB](connection-manager/ole-db-connection-manager.md)|[Configurar Gerenciador de Conexões OLE DB](configure-ole-db-connection-manager.md)|  
    |[Gerenciador de Conexões SMO](connection-manager/smo-connection-manager.md)|[Editor do Gerenciador de Conexões SMO](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[Gerenciador de Conexões SMTP](connection-manager/smtp-connection-manager.md)|[Editor do Gerenciador de Conexões SMTP](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[Gerenciador de Conexões do SQL Server Compact Edition](connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página de Conexão&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página Tudo&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Gerenciador de Conexões WMI](connection-manager/wmi-connection-manager.md)|[Editor do Gerenciador de Conexões WMI](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
     O gerenciador de conexões que você adicionou aparecerá sob o nó **Gerenciadores de Conexões** no **Gerenciador de Soluções**. Ele também aparecerá na guia **Gerenciadores de Conexões** na janela **Designer SSIS** para todos os pacotes no projeto. O nome do gerenciador de conexões nesta guia terá um prefixo **(projeto)** para diferenciar este gerenciador de conexões de nível de projeto dos gerenciadores de conexões de nível de pacote.  
  
4.  Como opção, clique com o botão direito do mouse no gerenciador de conexões na janela **Gerenciador de Soluções** no nó **Gerenciadores de Conexões** ou na guia **Gerenciadores de Conexões** da janela **Designer SSIS** , clique em **Renomear**e modifique o nome padrão do gerenciador de conexões.  
  
    > [!NOTE]  
    >  Na guia **Gerenciadores de Conexões** da janela **Designer SSIS**, você não poderá substituir o prefixo **(projeto)** do nome do gerenciador de conexões. Isso ocorre por design.  
  
##  <a name="parameter"></a> Para criar um parâmetro para uma propriedade de Gerenciador de conexão  
  
1.  Na área **Gerenciadores de Conexões** , clique com o botão direito do mouse no gerenciador de conexões para o qual você deseja criar um parâmetro e clique em **Definir Parâmetros**.  
  
2.  Configure os parâmetros na caixa de diálogo **Definir Parâmetros** . Para obter mais informações, consulte [Parameterize Dialog Box](../../2014/integration-services/parameterize-dialog-box.md).  
  
##  <a name="DeletePackageLevel"></a> Para excluir um Gerenciador de conexão de um pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , clique na guia **Controle de Fluxo** , na guia **Fluxo de Dados** , ou na guia **Manipulador de Eventos** para disponibilizar o **Gerenciador de Conexões** .  
  
4.  Clique com o botão direito do mouse no gerenciador de conexões que deseja excluir e clique em **Excluir**.  
  
     Ao excluir um gerenciador de conexões utilizado por um elemento do pacote, como uma tarefa Executar SQL ou uma fonte OLE DB, você terá os seguintes resultados:  
  
    -   Um ícone de erro aparece no elemento do pacote que usou o gerenciador de conexões excluído.  
  
    -   O pacote não é validado.  
  
    -   O pacote não pode ser executado.  
  
5.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
##  <a name="DeleteProjectLevel"></a> Para excluir um Gerenciador de conexão compartilhada (Gerenciador de conexão de nível de projeto)  
  
1.  Para excluir um gerenciador de conexões de nível de projeto, clique com o botão direito do mouse no gerenciador de conexões no nó **Gerenciadores de Conexões** na janela **Gerenciador de Soluções** e clique em **Excluir**. [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] exibe a seguinte mensagem de aviso:  
  
    > [!WARNING]  
    >  Quando você exclui um gerenciador de conexões de projeto, os pacotes que usam o gerenciador de conexões podem não ser executados. Você não pode desfazer essa ação. Você quer excluir o gerenciador de conexões?  
  
2.  Clique em OK para excluir o gerenciador de conexões ou em Cancelar para mantê-lo.  
  
    > [!NOTE]  
    >  Você também pode excluir um gerenciador de conexões de nível de projeto da guia **Gerenciador de Conexões** da janela **Designer SSIS** aberta para qualquer pacote no projeto. Isso é feito clicando-se com o botão direito do mouse no gerenciador de conexões na guia e clicando em **Excluir**.  
  
## <a name="see-also"></a>Consulte também  
 [Conexões do SSIS &#40;Integration Services&#41;](connection-manager/integration-services-ssis-connections.md)   
 [Definir as propriedades de um Gerenciador de Conexões](../../2014/integration-services/set-the-properties-of-a-connection-manager.md)  
  
  
