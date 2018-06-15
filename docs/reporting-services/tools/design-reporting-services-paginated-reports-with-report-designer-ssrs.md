---
title: Criar relatórios com o Designer de Relatórios (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: tools
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], report creation
ms.assetid: 3a26dccc-6ad6-48f5-a882-f96c6c0dd405
caps.latest.revision: 77
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 09311458bc7815a7a63d58ad19c8d8b0a3845da4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33037033"
---
# <a name="design-reporting-services-paginated-reports-with-report-designer-ssrs"></a>Criar relatórios paginados do Reporting Services com o Designer de relatórios (SSRS)

Use o Designer de Relatórios para criar relatórios paginados e soluções completas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . O Designer de Relatórios fornece uma interface gráfica na qual você pode definir fontes de dados, conjuntos de dados e consultas, posições do layout do relatório para regiões de dados e campos e recursos interativos, como parâmetros e conjuntos de relatórios que funcionam em conjunto.  

O Designer de Relatórios é um recurso do  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], um ambiente do Microsoft Visual Studio para criação de soluções de business intelligence. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] não é incluído com o SQL Server. Baixar o [SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=616714). 
  
## <a name="benefits-of-report-projects"></a>Benefícios dos projetos de relatório  
Os projetos de relatório atuam como contêineres para recursos e definições de relatório. Use projetos para:  
  
-   Organizar relatórios e itens relacionados em um contêiner.  
  
-   Testar soluções de relatório que incluem relatórios e itens relacionados localmente.  
  
-   Implantar itens relacionados em conjunto. Usar propriedades de projeto e gerenciamento de configuração para implantação em vários ambientes.  
  
-   Preservar um conjunto de cópias mestres para relatórios e itens relacionados. Depois da implantação, os relatórios publicados podem ser modificados acidentalmente.  
  
 Use as informações deste tópico para criar relatórios paginados e itens relacionados para um único projeto de relatório em uma solução do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] . Para saber mais sobre soluções e vários projetos no SQL Server Data Tools, veja [Reporting Services no SQL Server Data Tools](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md).  

  
##  <a name="bkmk_SharedDataSources"></a> Fontes de dados compartilhadas  
 Use o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para definir e implantar fontes de dados compartilhadas para uma solução de relatório. As fontes de dados compartilhadas podem ser implantadas independentemente de outros itens em um projeto por meio das propriedades **OverwriteDataSources** e **TargetDataSourceFolder** . Para obter mais informações, consulte [Definir propriedades de implantação &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
 No Designer de Relatórios, você trabalha no painel Dados do Relatório e no Gerenciador de Soluções para definir as fontes de dados usadas em um relatório. Para obter mais informações, consulte [Report Data Pane](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_ReportDataPane). Você não pode usar o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para abrir fontes de dados publicadas em um servidor de relatório ou site do SharePoint, mas não incluídas na solução do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] . Para esse recurso, use [Ambiente de criação do Construtor de Relatórios &#40;SSRS&#41;](../../reporting-services/tools/report-builder-authoring-environment-ssrs.md).  
  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] é uma ferramenta de cliente. Você pode testar sua solução de relatório localmente em seu computador, implantá-la em um ambiente de teste para testar a solução de servidor e, em seguida, implantá-la em um ambiente de produção. Depois da implantação, verifique se as extensões de processamento de fonte de dados e as credenciais de fonte de dados estão configuradas para o ambiente de servidor de relatório. Você pode usar o Gerenciador de Configurações para ajudar a gerenciar as propriedades de diferentes implantações. Para obter mais informações, consulte [Reporting Services no SQL Server Data Tools &#40;SSDT&#41;](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md).  
  
 Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
   
##  <a name="bkmk_SharedDatasets"></a> Conjuntos de dados compartilhados  
 Use o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para definir e implantar conjuntos de dados compartilhados para uma solução de relatório. Os conjuntos de dados compartilhados podem ser implantadas independentemente de outros itens em um projeto por meio das propriedades **OverwriteDatasets** e **TargetDatasetFolder** . Para obter mais informações, consulte [Definir propriedades de implantação &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
 No Designer de Relatórios, você trabalha no painel Dados do Relatório e no Gerenciador de Soluções para definir os conjuntos de dados compartilhados usados em um relatório. Para obter mais informações, consulte [Report Data Pane](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_ReportDataPane). Você não pode usar o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para abrir conjuntos de dados publicados diretamente em um servidor de relatório ou site do SharePoint. Para esse recurso, use [Ambiente de criação do Construtor de Relatórios &#40;SSRS&#41;](../../reporting-services/tools/report-builder-authoring-environment-ssrs.md) no modo de Conjunto de Dados Compartilhado.  
  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] é uma ferramenta de cliente. Você pode usar designers de consulta para ajudar a criar e testar os resultados de suas consultas localmente em Visualização. Depois da implantação, você pode gerenciar conjuntos de dados compartilhados independentemente das fontes de dados compartilhadas e dos relatórios dos quais eles dependem. Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md), [Ferramentas de Design da Consulta &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md), e [Gerenciar conjuntos de dados compartilhados](../../reporting-services/report-data/manage-shared-datasets.md).  
  
##  <a name="bkmk_Reports"></a> Relatórios paginados  
Relatórios paginados são arquivos armazenados em um projeto de relatório. Os relatórios podem ser usados como relatórios autônomos, sub-relatórios ou os destinos para ações de detalhamento de relatórios principais. Os relatórios podem ser implantadas independentemente de outros itens em um projeto por meio da propriedade **TargetReportFolder** e de outras propriedades. Para obter mais informações, consulte [Definir propriedades de implantação &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
> [!NOTE]  
>  Se você estiver publicando em um servidor de relatório em modo do SharePoint, alguns recursos de solução de relatório não poderão ser testados no projeto do Designer de Relatórios. As referências a relatórios, sub-relatórios e relatórios detalhados devem usar URLs totalmente qualificadas que possam ser testadas apenas depois de você implantar o projeto de relatório. Para obter mais informações, consulte [Exemplos de URL para itens de relatório publicados em um Servidor de Relatório no modo do SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md).  
  
 Você pode adicionar relatórios a um projeto das seguintes maneiras:  
  
-   **Adicionar um novo projeto de relatório.** Por padrão, um relatório em branco é aberto no Designer de Relatórios. Para obter mais informações, consulte [Adicionar um relatório novo ou existente a um projeto de relatório &#40;SSRS&#41;](../../reporting-services/tools/add-a-new-or-existing-report-to-a-report-project-ssrs.md).  
  
-   **Adicionar um projeto de Assistente de Relatório.** Você cria um relatório de uma maneira orientada passo a passo. O Assistente de Relatório simplifica a definição de dados e o design de relatórios em uma série de etapas que fornecem um relatório concluído. Você pode adicionar estilos para personalizar o assistente para sua própria organização. Para obter mais informações, consulte [Adicionar um relatório novo ou existente a um projeto de relatório &#40;SSRS&#41;](../../reporting-services/tools/add-a-new-or-existing-report-to-a-report-project-ssrs.md).  
  
-   **Adicionar um novo item de tipo Relatório.** Um relatório em branco é aberto no Designer de Relatórios.  
  
-   **Adicionar um item existente.** Uma definição de relatório existente (.rdl) é aberta no Designer de Relatórios. A abertura de um relatório ou projeto em uma versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pode atualizar o projeto automaticamente para a versão atual, e o relatório para o esquema atual. Para obter mais informações, consulte [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md).  
  
-   **Importe um relatório do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access.** Importe todos os relatórios de um banco de dados do Access (.mdb, .accdb) ou arquivo de projeto (.adp). O Designer de Relatórios converte cada relatório em um arquivo de banco de dados ou de projeto em RDL e salva-o no projeto de relatório. Nem todas as funcionalidades de um relatório do Access são transferidas para um arquivo de definição de relatório (.rdl). Para obter mais informações, consulte [Importar relatórios do Microsoft Access &#40;Reporting Services&#41;](http://msdn.microsoft.com/library/4f29d5b8-b77d-4714-a84a-05523df55646) e [Recursos de relatórios do Access com suporte &#40;SSRS&#41;](http://msdn.microsoft.com/library/7ffec331-6365-4c13-8e58-b77a48cffb44).  
  
    > [!NOTE]  
    >  Para usar o recurso de importação, você deve ter o Access 2002 ou uma versão posterior no mesmo computador que o Designer de Relatórios está instalado. A fonte de dados para os relatórios de Access deverá estar disponível quando os relatórios forem importados.  
  
-   **Trabalhar diretamente em RDL.** Quando você grava um relatório no Designer de Relatórios, o relatório é salvo no formato XML como um arquivo de linguagem RDL. Você poderá editar esse arquivo no Designer de Relatórios, em um editor de texto ou em qualquer ferramenta na qual possa editar XML.  
  
     Ao editar a origem da definição do relatório no Designer de Relatórios, você está trabalhando no esquema RDL atual para a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da qual você instalou as ferramentas de desenvolvimento. Quando você compila um projeto, a versão do esquema pode ser alterada de acordo com as propriedades de sua implantação. Para obter mais informações, veja [Implantação e suporte de versão no SQL Server Data Tools &#40;SSRS&#41;](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
     Editar o RDL diretamente pode fazer com que um relatório não possa ser publicado ou executado no servidor de relatórios. Assim como em qualquer arquivo XML, verifique se os caracteres específicos da linguagem XML usados dentro dos elementos estão codificados corretamente. Ao publicar o relatório, o servidor de relatórios usa o esquema para validar o XML que está no arquivo RDL.  
  
     Para incluir elementos que não fazem parte do esquema RDL, coloque-os no Elemento Personalizado. O Elemento Personalizado pode ser lido por extensões de renderização personalizadas, mas é ignorado por extensões de renderização fornecidas com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Por exemplo, você pode usar o elemento Personalizado para armazenar comentários no relatório.  
  
     Para obter mais informações, consulte [Linguagem RDL &#40;SSRS&#41;](../../reporting-services/reports/report-definition-language-ssrs.md).  
  
##  <a name="bkmk_ReportParts"></a> Partes de relatório  
 No Designer de Relatórios, depois de criar tabelas, gráficos e outros itens de relatório paginado em um projeto, você pode publicá-los como *partes de relatório* em um servidor de relatório ou site do SharePoint integrado com um servidor de relatório de forma que você e outros usuários possam reutilizá-las em outros relatórios. Para obter mais informações, consulte [Partes de relatório no Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md).  
  
 As partes de relatório podem ser implantadas independentemente de outros itens em um projeto por meio da propriedade **TargetReportPartFolder** e de outras propriedades. Para obter mais informações, consulte [Definir propriedades de implantação &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
##  <a name="bkmk_Resources"></a> Recursos  
 Você pode adicionar arquivos a seu projeto que estejam relacionados a seu relatório, mas não sejam processados pelo servidor de relatório. Por exemplo, você pode adicionar imagens para imagens ou arquivos de forma ESRI para dados espaciais. Para obter mais informações, consulte [Resources](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md#bkmk_Resources).  
 
##  <a name="bkmk_ReportLayout"></a> Layout de relatório paginado  
 Para criar o layout do relatório, arraste itens do relatório e regiões de dados da Caixa de Ferramentas para a superfície de design e organize-os. Arraste os campos de conjunto de dados para os itens na superfície de design para adicionar dados ao relatório. Para organizar dados em grupos em uma região de dados tablix, arraste campos de conjunto de dados para o painel Agrupamento. Como as ferramentas de criação de relatório são essencialmente uma maneira de criar definições de relatório, a abordagem do design de relatórios é bastante semelhante entre Construtor de Relatórios e Designer de Relatórios.  
   
##  <a name="bkmk_Preview"></a> Visualizar um relatório paginado  
 Use a **Visualização** para verificar os dados e o design de layout do relatório. Quando você visualiza um relatório, o processador de relatório valida o esquema de definição de relatório e a sintaxe de expressão e lista os problemas na janela [Output](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_Output) .  
  
> [!NOTE]  
>  Quando você visualizar um relatório, seus dados serão armazenados em cache em um arquivo no computador local. Ao visualizar novamente o mesmo relatório usando a mesma consulta, os mesmos parâmetros e as mesmas credenciais, o Designer de Relatórios recuperará a cópia em cache em vez de executar a consulta mais uma vez. O arquivo de dados será salvo como *\<nomedorelatório>*.rdl.data no mesmo diretório do arquivo de definição de relatório. Ele não será excluído quando você fechar o Designer de Relatórios.  
  
 Você pode visualizar um relatório das seguintes maneiras:  
  
-   **Exibição de visualização.** Clique na guia **Visualização** . O relatório é executado localmente, por meio da mesma funcionalidade de processamento e renderização de relatório do servidor de relatório. O relatório será exibido como uma imagem interativa: é possível selecionar parâmetros, clicar em links, exibir o mapa do documento e expandir e recolher áreas ocultas do relatório. Também é possível exportar o relatório para qualquer formato de renderização instalado.  
  
-   **Visualização autônoma.** Execute o relatório local em um navegador. Por meio de uma configuração de depuração, você também pode usar esse modo para depurar assemblies personalizados criados por você. Há três maneiras de executar um projeto em modo de Depuração:  
  
    -   No menu **Depurar** , clique em **Iniciar Depuração**.  
  
    -   Na barra de ferramentas padrão do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] , clique no botão **Iniciar** .  
  
    -   Pressione F5.  
  
     Se você usar a configuração de projeto que cria um relatório mas não o implanta, o relatório especificado na propriedade **StartItem** da configuração atual será aberto em outra janela de visualização.  
  
    > [!NOTE]  
    >  Para usar o modo de Depuração, defina um item inicial. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto de relatório, clique em **Propriedades**e, em **StartItem**, selecione o nome do relatório a ser exibido.  
  
     Se quiser visualizar um relatório específico que não é o item inicial do projeto, selecione uma configuração que cria o relatório, mas que não o implanta (por exemplo, a configuração DebugLocal), clique com o botão direito do mouse no relatório e clique em **Executar**. Escolha uma configuração que não implante o relatório, caso contrário, o relatório será publicado no servidor de relatórios em vez de ser exibido localmente na janela de visualização.  
  
-   **Visualizar Impressão.**  
  
     Na primeira vez em que você visualizar o relatório em modo de Visualização ou na janela de visualização, a exibição do relatório será similar a um relatório gerado pela extensão de renderização HTML. A visualização não é HTML, mas o layout e a paginação do relatório são semelhantes a uma saída em HTML.  
  
     Você pode alterar a exibição para representar um relatório impresso alternando para o modo Visualizar Impressão. Clique no botão **Visualizar Impressão** na barra de ferramentas de visualização. O relatório será exibido como se tivesse sido impresso. Essa exibição é semelhante à saída produzida pelas extensões de renderização de Imagem e PDF. A visualização de impressão não é um arquivo de imagem ou PDF, mas o layout e a paginação do relatório são semelhantes a uma saída nesses formatos. Você pode escolher o tamanho da imagem do relatório, por exemplo, definir a largura da página.  
  
     A visualização da impressão ajuda a identificar muitos dos problemas de renderização que você pode encontrar ao imprimir o relatório. Os problemas comuns de renderização incluem:  
  
    -   Páginas em branco extras porque o relatório é muito largo para se ajustar ao tamanho do papel especificado para o relatório.  
  
    -   Páginas em branco extras porque o relatório contém uma matriz que se expande dinamicamente para exceder a largura do papel especificado.  
  
    -   Quebras de páginas entre grupos que não funcionam da maneira desejada.  
  
    -   Cabeçalhos e rodapés que não são exibidos como esperado.  
  
    -   O layout do relatório precisa de modificação para melhor leitura em um formato impresso.  
   
##  <a name="bkmk_SaveandDeploy"></a> Salvar e implantar relatórios paginados  
 No Designer de Relatórios, você pode salvar relatórios e outros arquivos de projeto localmente ou implantá-los em um servidor de relatório ou site do SharePoint. Fontes de dados compartilhadas, conjuntos de dados compartilhados, relatórios, recursos e partes de relatório podem ser implantados independentemente ou em conjunto dependendo das propriedades de implantação configuradas. Para obter mais informações, consulte [Configuration and Deployment Properties](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md#bkmk_ConfigurationandDeploymentProperties).  
  
 No Designer de Relatórios, é importante entender que você cria um relatório por meio do esquema de definição de relatório com suporte da versão atual do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Quando você define propriedades de implantação de projeto para um servidor de relatório específico ou site do SharePoint e, em seguida, salva o relatório, o Designer de Relatórios salva a definição de relatório no diretório de compilação no esquema que corresponde à versão no servidor de relatório de destino. Para criar relatórios que podem ser publicados em um servidor de relatório de versão anterior, o Designer de Relatórios remove itens de relatório que não existem no esquema de destino. Isto ocorre automaticamente e sem solicitar. Quando isso ocorre, a definição de relatório original é preservada na pasta do projeto. A definição de relatório modificada que é implantada está na pasta de compilação.  
  
> [!NOTE]  
>  Para depurar erros de expressões e de implantação, exiba a definição de relatório na pasta de compilação. Não use **Exibir Código-Fonte**. A opção**Exibir Código-Fonte** exibe a origem da definição de relatório na pasta do projeto.  
  
 Para obter mais informações, veja [Implantação e suporte de versão no SQL Server Data Tools &#40;SSRS&#41;](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
### <a name="save-a-report-locally"></a>Salvar um relatório localmente  
 Quando você trabalha em um relatório ou em outros itens de projeto no Designer de Relatórios, os arquivos são salvos em seu computador local ou em um compartilhamento em outro computador ao qual você tem acesso.  
  
 Se estiver usando software de controle de código-fonte, você talvez esteja verificando seus relatórios no servidor de controle do código-fonte ao salvar o relatório. Para obter mais informações, consulte [Source Control](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_SourceControl).  
  
### <a name="deploy-or-publish-paginated-reports"></a>Implantar ou publicar relatórios paginados  
 No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], você pode implantar relatórios ou outros itens de projeto em várias versões de servidores de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Use as configurações de projeto para controlar a atualização de definições de relatório para versões de esquema compatíveis com os servidores de relatório de destino. As propriedades controladas por configurações de projeto incluem o servidor de relatório de destino, a pasta onde o processo de compilação armazena temporariamente as definições de relatórios para visualização e implantação e os níveis de erro. Para obter mais informações, consulte [Propriedades e configuração e de implantação](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md#bkmk_ConfigurationandDeploymentProperties) e [Definir propriedades de implantação &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
### <a name="export-a-paginated-report-to-a-different-file-format"></a>Exportar um relatório paginado para um formato de arquivo diferente  
 Os relatórios podem ser exportados para diversos formatos; esses formatos afetam o funcionamento de alguns recursos de interatividade e de layout de relatório. Para obter mais informações sobre considerações de design para vários formatos de saída, consulte [Exportar relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md).  
   
##  <a name="bkmk_ReportValidationandErrorLevels"></a> Validação de relatórios e níveis de erro  
 Os relatórios são validados antes da visualização e durante a implantação. Vários problemas de compilação podem ocorrer ao compilar relatórios. Os relatórios podem conter cadeias de caracteres como expressões ou consultas incompatíveis com a versão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que a configuração do projeto especifica, por exemplo.  
  
 Use a propriedade ErrorLevel para gerenciar os avisos e os erros de build. A propriedade ErrorLevel pode conter um valor de 0 a 4, inclusive. O valor determina quais problemas de compilação são relatados como erros e quais são relatados como avisos. O valor padrão é 2. Os avisos e erros são gravados na janela [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)][Saída](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_Output) .  
  
 Problemas com níveis de severidade menor ou igual ao valor ErrorLevel são relatados como erros; caso contrário, eles são relatados como avisos.  
  
 A tabela a seguir lista os níveis de erro.  
  
|Nível de erro|Description|  
|-----------------|-----------------|  
|0|Problemas de compilação mais severos e inevitáveis que impedem a visualização e a implantação de relatórios.|  
|1|Problemas de compilação severos que alteram o layout de relatório drasticamente.|  
|2|Problemas de compilação menos severos que alteram o layout de relatório de forma significativa.|  
|3|Problemas de compilação secundários que alteram o layout de relatório de maneira quase imperceptível.|  
|4|Somente usado para publicar avisos.|  
  
 Quando você tenta visualizar ou implantar um relatório que contém novos itens de relatório no [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], esses itens de relatório podem ser removidos do relatório. Por padrão, a propriedade ErrorLevel da configuração é definida como 2, o que causa a falha de build do relatório quando o mapa é removido. Porém, se você alterar o valor da propriedade ErrorLevel para 0 ou 1, o mapa será removido, um aviso será emitido e o processo de build continuará.  

## <a name="next-steps"></a>Próximas etapas

[Baixe o SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=616714)  
[Reporting Services no SQL Server Data Tools](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)   
[Ferramentas de Design da Consulta](../../reporting-services/report-data/query-design-tools-ssrs.md)   
[Implantação e suporte de versão no SQL Server Data Tools](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
