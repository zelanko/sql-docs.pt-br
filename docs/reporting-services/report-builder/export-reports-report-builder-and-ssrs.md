---
title: Exportar relatórios (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-builder
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10437"
ms.assetid: a2bab8c1-505d-4da3-b1db-ea0ae13b2336
caps.latest.revision: 23
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9c4b6d1ac7e16cc7260667ffc786b68a5f2d9a18
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="export-reports-report-builder-and-ssrs"></a>Exportar relatórios (Construtor de Relatórios e SSRS)

  Você pode exportar um relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para outro formato de arquivo, como PowerPoint, Image, PDF, [!INCLUDE[ofprword](../../includes/ofprword-md.md)], [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] ou então exportá-lo gerando um documento do serviço Atom, listando os feeds de dados compatíveis com o Atom disponíveis no relatório. Você pode exportar o relatório do Construtor de Relatórios, do Designer de Relatórios ([!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]) ou do servidor de relatórios.  
  
 Para exportar um relatório, siga este procedimento:  
  
-   **Trabalhar com os dados do relatório em outro aplicativo.** Por exemplo, você pode exportar seu relatório para o Excel e continuar trabalhando com os dados no Excel.  
  
-   **Imprimir o relatório em outro formato.** Por exemplo, você pode exportar o relatório para o formato de arquivo PDF e depois imprimir o conteúdo dele.  
  
-   **Salvar uma cópia do relatório como outro tipo de arquivo.** Por exemplo, você pode exportar um relatório para o Word e salvá-lo, criando uma cópia do relatório.  
  
-   **Use os dados do relatório como feeds de dados em aplicativos.** Por exemplo, você pode gerar feeds de dados em conformidade com Atom que podem ser consumidos pelo Power Pivot ou Power BI e, em seguida, trabalhar com os dados no Power Pivot ou no Power BI. Para obter mais informações, consulte [Gerar feeds de dados com base em um relatório](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md)  
  
-   A renderização do relatório no servidor de relatórios é útil quando você configura assinaturas ou fornece seus relatórios por email, ou quando deseja salvar um relatório disponível no servidor de relatórios. Para obter mais informações, consulte [Assinaturas e entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece muitas extensões de renderização, suportando exportações de relatórios para formatos de arquivos comuns. As extensões de renderização oferecem suporte somente a quebras flexíveis (por exemplo, Word ou Excel), quebras da página não flexíveis (por exemplo, PDF ou TIFF) ou somente dados (por exemplo, XML compatível com Atom ou CSV).  
  
 Pode ser que a paginação do relatório seja afetada quando você exporta um relatório para outro formato. Ao visualizar um relatório, você está visualizando-o como se estivesse renderizado pela extensão de renderização HTML, que segue as regras de quebra de página flexível. Quando você exporta um relatório para um formato de arquivo diferente, como Adobe Acrobat (PDF), a paginação se baseia no tamanho de página físico que segue regras de quebra de página não flexíveis. As páginas também podem ser separadas por quebra de página lógica que você adiciona a um relatório, mas o comprimento real da página varia com base no tipo de processador usado. Para alterar a paginação de seu relatório, você deve entender o comportamento de paginação da extensão de renderização escolhida. Talvez seja necessário ajustar o design de seu layout de relatório para esta extensão de renderização. Para obter mais informações, consulte [Layout da página e renderização](../../reporting-services/report-design/page-layout-and-rendering-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]

## <a name="bkmk_export_from_rb"></a> Para exportar um relatório do Construtor de Relatórios

1.  Execute ou visualize o relatório.  
  
2.  Na faixa de opções, clique em **Exportar**.  
  
     ![Exportação do Construtor de Relatórios](../../reporting-services/report-builder/media/ssrb-export.png "Exportação do Construtor de Relatórios")  
  
3.  Selecione o formato que você deseja usar.  
  
     A caixa **Salvar Como** é aberta. Por padrão, o nome do arquivo é o mesmo do relatório que você exportou. Opcionalmente, você pode alterar o nome do arquivo.  
  
##  <a name="bkmk_export_from_rm"></a> Para exportar um relatório do portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
1.  Na [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] página inicial **do portal da Web do** , navegue até o relatório que deseja exportar.  
  
2.  Clique no relatório para renderizá-lo e visualizá-lo.  
  
3.  Na barra de ferramentas do Visualizador de Relatórios, clique na seta suspensa **Exportar** .  
  
     ![Exportação do portal da Web do Reporting Services](../../reporting-services/report-builder/media/ssrsportal-export.png "Exportação do portal da Web do Reporting Services")  
  
4.  Selecione o formato que você deseja usar.  
  
5.  Clique em **Exportar**. Uma mensagem é exibida perguntando se você deseja abrir ou salvar o arquivo.  
  
6.  Para exibir o relatório no formato de exportação selecionado, clique em **Abrir**.  
  
     \- ou –  
  
     Para salvar imediatamente o relatório no formato de exportação selecionado, clique em **Salvar**.  
  
     Usando o aplicativo associado ao formato escolhido, o relatório é exibido ou salvo. Se você clicar em **Salvar**, você será solicitado a indicar um local no qual seja possível salvar o relatório.  
  
##  <a name="bkmk_export_from_sharepoint"></a> Para exportar o relatório de uma biblioteca do SharePoint  
  
1.  Visualize o relatório.  
  
2.  Na barra de ferramentas, clique em **Ações**, aponte para **Exportar**e selecione o formato desejado.  
  
     A caixa de diálogo **Download de Arquivo** é aberta.  
  
3.  Para exibir o relatório no formato de exportação selecionado, clique em **Abrir**.  
  
     \- ou –  
  
     Para salvar imediatamente o relatório no formato de exportação selecionado, clique em **Salvar**.  
  
     Usando o aplicativo associado ao formato escolhido, o relatório é exibido ou salvo. Se você clicar em **Salvar**, você será solicitado a indicar um local no qual seja possível salvar o relatório.  
  
     Outra opção é alterar o nome do arquivo do relatório exportado.  
  
     **Observação** Se o programa não puder abrir o relatório no formato escolhido porque você não tem um programa associado a esse tipo de arquivo, você será solicitado a salvar o relatório exportado ou a localizar um programa online para abri-lo.  
  
##  <a name="RendererTypes"></a> Tipos de extensão de renderização  
 Há três tipos de extensões de renderização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   **Extensões dos processadores de dados** As extensões de renderização de dados eliminam todas as informações de formatação e layout do relatório e exibem apenas os dados. O arquivo resultante pode ser usado para importar os dados brutos do relatório em outro tipo de arquivo, como o Excel, outro banco de dados, uma mensagem de dados XML, ou um aplicativo personalizado. Processadores de dados não oferecem suporte a quebras de páginas.  
  
     As seguintes extensões de renderização de dados são suportadas: CSV, XML e Atom.  
  
-   **Extensões do renderizador de quebra suave de página** As extensões de renderização de quebra suave de página mantêm o layout e a formatação do relatório. O arquivo resultante é otimizado para exibição com base em tela e entrega, como em uma página da Web ou nos controles do **ReportViewer** .  
  
     As extensões de renderização de quebra de página flexível a seguir têm suporte: o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word e arquivo da Web (MHTML).  
  
-   **Extensões de renderização de quebra de página impressa** As extensões do renderizador de quebra de página impressa mantêm o layout e a formatação do relatório. O arquivo resultante é otimizado para uma experiência consistente de impressão, ou para exibir o relatório online em formato de um livro.  
  
     As extensões de renderização de quebra de página não flexível a seguinte têm suporte: TIFF e PDF.  
  
##  <a name="ExportFormats"></a> Formatos para os quais você pode exportar enquanto exibe relatórios  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece extensões de renderização que renderizam relatórios em formatos diferentes. Você deve otimizar o design de relatório para seu formato de arquivo escolhido.  A tabela a seguir lista os formatos para osquais você pode exportar da interface do usuário.  Há formatos adicionais que podem ser usados com assinaturas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou caso você esteja exportando do acesso à URL.  Consulte a seção [Outros modos de exportar relatórios](#OtherWaysExportingReports)neste tópico.  
  
|Formato|Tipos de extensão de renderização|Description|  
|------------|------------------------------|-----------------|  
|Arquivo do Acrobat (PDF)|Quebra de página não flexível|A extensão de renderização PDF renderiza um relatório para os arquivos que podem ser abertos no Adobe Acrobat e em outros visualizadores em PDF de terceiros que dão suporte ao PDF 1.3. Embora o PDF 1.3 seja compatível com o Adobe Acrobat 4.0 e posterior, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dá suporte ao para o Adobe Acrobat 6 ou posterior. A extensão de renderização não requer que o software Adobe renderize o relatório. Porém, os visualizadores de PDF, como o Adobe Acrobat, são necessários para exibir ou imprimir um relatório em formato PDF.<br /><br /> Para obter mais informações, consulte [Exportando para um arquivo PDF](../../reporting-services/report-builder/exporting-to-a-pdf-file-report-builder-and-ssrs.md).|  
|Atom|data|A extensão de renderização do Atom gera feeds de dados compatíveis com o Atom a partir de relatórios. Os feeds de dados são legíveis e intercambiáveis com aplicativos como o Power Pivot ou o Power BI, que pode consumir feeds de dados em conformidade com Atom.<br /><br /> A saída é documento de serviço Atom que lista os feeds de dados disponíveis a partir de um relatório. É criado pelo menos um feed de dados para cada região no relatório. Dependendo do tipo de região de dados e dos dados que a região de dados exibe, vários feeds de dados poderão ser gerados.<br /><br /> Para obter mais informações, consulte [Gerando feeds de dados com base em relatórios](../../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md).|  
|CSV|data|A extensão de renderização CSV (Comma-Separated Value) renderiza relatórios como uma representação mesclada dos dados de um relatório padronizado, em formato de texto simples que pode ser facilmente lido e que também permite a troca com vários aplicativos.<br /><br /> Para obter mais informações, consulte [Exportando para um arquivo CSV](../../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md).|  
|EXCELOPENXML|Quebra de página flexível|Exibido como "Excel" nos menus de exportação ao examinar relatórios. A extensão de renderização do Excel renderiza um relatório como um documento do Excel (.xlsx) que é compatível com o [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2013.  Para obter mais informações, consulte [Exportando para o Microsoft Excel](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).|  
|PowerPoint|Quebra de página não flexível|A extensão de renderização do PowerPoint renderiza um relatório como um documento do PowerPoint (.pptx) que é compatível com o PowerPoint 2013.|  
|Arquivo TIFF|Quebra de página não flexível|A extensão de renderização da Imagem renderiza um relatório para um bitmap ou metarquivo. Por padrão, a extensão de renderização da Imagem produz um arquivo TIFF do relatório, que pode ser exibido em várias páginas. Quando o cliente receber a imagem, ela pode ser exibida em um visualizador de imagem e impressa.<br /><br /> A extensão de renderização de Imagem pode gerar arquivos em qualquer um dos formatos que tenham o suporte do [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]: BMP, EMF, EMFPlus, GIF, JPEG, PNG e TIFF.<br /><br /> Para obter mais informações, consulte [Exportando para um arquivo de imagem](../../reporting-services/report-builder/exporting-to-an-image-file-report-builder-and-ssrs.md).|  
|Arquivo da Web|Quebra de página flexível|A extensão de renderização HTML renderiza um relatório no formato HTML. A extensão de renderização também pode produzir páginas HTML totalmente formadas ou fragmentos de HTML a serem inseridos em outras páginas HTML. Todo o HTML é gerado com a codificação UTF-8.<br /><br /> A extensão de renderização HTML é a extensão de renderização padrão para relatórios que visualizados no Construtor de Relatórios e são exibidos em um navegador, incluindo quando executados no portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .<br /><br /> Para obter mais informações, consulte [Renderizando para HTML](../../reporting-services/report-builder/rendering-to-html-report-builder-and-ssrs.md).|  
|WORDOPENXML|Quebra de página flexível|Exibido como "Word" no menu Exportar ao exibir relatórios. A extensão de renderização do Word renderiza um relatório como um documento do Word (.docx) que é compatível com o [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2013.  Para obter mais informações, consulte [Exportando para o Microsoft Word](../../reporting-services/report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md).|  
|XML|Dados|A extensão XML de renderização retorna um relatório no formato XML. O esquema para o XML do relatório é específico para este relatório e contém somente dados. As informações de layout não são renderizadas e a paginação não é mantida pela extensão XML de renderização. O XML gerado por esta extensão pode ser importado para um banco de dados, usado como uma mensagem de dados XML ou enviado para um aplicativo personalizado.<br/><br/> Para obter mais informações, consulte [Exportando para XML](../../reporting-services/report-builder/exporting-to-xml-report-builder-and-ssrs.md).|  
  
##  <a name="GeneratingDataFeedsFromReport"></a> Gerando feeds de dados a partir do relatório  
 Para gerar feeds de dados de um relatório, execute-o no portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e clique no ícone **Gerar Feed de Dados** na barra de ferramentas do portal da Web. Você deverá escolher se deseja salvar ou abrir o arquivo. Se você escolheu **Abrir**, o documento de serviço do Atom será aberto no aplicativo associado à extensão do arquivo .atomsvc. Se você escolheu **Salvar**, o documento será salvo como um arquivo .atomsvc. Por padrão, o nome do arquivo é o nome do relatório. Você pode alterar o nome para um que seja mais significativo.  
  
 Salve o documento de serviço do Atom em seu computador. Posteriormente, será possível carregá-lo em um servidor de relatório ou outro servidor para que ele seja disponibilizado ao uso de outras pessoas. Para obter mais informações, consulte [Gerando feeds de dados com base em relatórios](../../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md) e [Gerar feeds de dados com base em um relatório](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md).  
  
##  <a name="Troubleshooting"></a> Solucionando problemas de relatórios exportados  
 Às vezes, os relatórios parecem diferente ou não funcionam da maneira desejada depois que você os exporta para um formato diferente. Isso ocorre porque determinas regras e limitações podem se aplicar ao renderizador. É possível resolver muitas limitações, considerando-as durante a criação do relatório. Você talvez precise usar um layout um pouco diferente no relatório, alinhar cuidadosamente itens dentro do relatório, confinar rodapés do relatório a uma única linha de texto e assim por diante.  
  
 Se o seu relatório contiver texto Unicode com números arábicos ou contiver datas em árabe, as datas e os números não serão renderizados corretamente quando você exportar o relatório para qualquer um dos seguintes formatos ou imprimir o relatório.  
  
-   PDF  
  
-   Word  
  
-   Excel  
  
-   Imagem/TIFF  
  
 Se você exportar o relatório para HTML, as datas e os números serão renderizados corretamente.  
  
 Os tópicos sobre renderizadores específicos descrevem como itens de relatório e regiões de dados são renderizados, bem como as limitações e as soluções para cada renderizador.  
  
-   [Exportação para um arquivo CSV &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)  
  
-   [Exportando para o Microsoft Excel &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)  
  
-   [Exportando para o Microsoft Word &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md)  
  
-   [Renderizando para HTML &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/rendering-to-html-report-builder-and-ssrs.md)  
  
-   [Exportação para um arquivo PDF &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/exporting-to-a-pdf-file-report-builder-and-ssrs.md)  
  
-   [Exportando para um arquivo de imagem &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/exporting-to-an-image-file-report-builder-and-ssrs.md)  
  
-   [Exportação para um XML &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/exporting-to-xml-report-builder-and-ssrs.md)  
  
-   [Gerando feeds de dados de relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece recursos adicionais para ajudar a criar relatórios que funcionam bem em outros formatos. Quebras de páginas em regiões de dados Tablix (tabela, matriz e lista), grupos e retângulos dão um melhor controle sobre a paginação de relatórios. As páginas do relatório, delimitadas por quebras de páginas, podem ter nomes de página diferentes e a numeração de páginas redefinida. Usando-se expressões, os nomes e os números de páginas podem ser atualizados dinamicamente quando o relatório é executado. Para obter mais informações, consulte [Paginação no Reporting Services](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
 Além disso, é possível usar RenderFormat interno global para aplicar condicionalmente layouts de relatório diferentes a renderizadores distintos. Para obter mais informações, consulte [Referências de globais internas e referências de usuários](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)

##  <a name="OtherWaysExportingReports"></a> Outros modos de exportar relatórios  
 A exportação de um relatório é uma tarefa sob demanda que você executa quando o relatório é aberto no portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou no Construtor de Relatórios. Se quiser automatizar uma operação de exportação (por exemplo, para exportar um relatório para uma pasta compartilhada como um tipo de arquivo específico em uma agenda recorrente), crie uma assinatura que entregue o relatório para uma pasta compartilhada. Para obter mais informações, consulte [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md).  
  
 Os relatórios visualizados nas ferramentas para relatórios ou abertos em um aplicativo de navegação como o portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são sempre renderizados primeiro em HTML. Você não pode especificar uma extensão de renderização diferente como padrão para visualização. Todavia, você pode criar uma assinatura que produz um relatório no formato de renderização desejado para a entrega subsequente a uma caixa de entrada de email ou uma pasta compartilhada. Para obter mais informações, consulte [Crie e gerencie assinaturas de servidores de relatório no modo Nativo](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md) e [Criar, modificar e excluir assinaturas controladas por dados](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md).  
  
 Você também pode acessar um relatório por uma URL que especifique uma extensão de renderização como um parâmetro de URL e renderizar o relatório diretamente para o formato especificado, sem renderizá-lo primeiro em HTML. Este exemplo renderiza um relatório no formato Excel:  
  
```  
http://<Report Server Name>/reportserver?/Sales/YearlySalesSummary&rs:Format=Excel&rs:Command=Render  
```  
  
 e a seguir renderiza um relatório do PowerPoint de uma instância nomeada:  
  
```  
http://<Report Server Name/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  
  
 Para saber mais, confira [Export a Report Using URL Access](../../reporting-services/export-a-report-using-url-access.md).  

## <a name="next-steps"></a>Próximas etapas

[Controlando quebras de páginas, títulos, colunas e linhas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
[Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
[Imprimir relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
[Salvando relatórios &#40;Construtor de Relatórios&#41;](../../reporting-services/report-builder/saving-reports-report-builder.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
