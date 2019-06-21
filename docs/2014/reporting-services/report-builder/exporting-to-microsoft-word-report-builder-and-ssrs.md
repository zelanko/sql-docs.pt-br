---
title: Exportando para o Microsoft Word (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0cd8ae26-4682-4473-8f15-af084951defd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3eaaace0d8ae5924305024e6ee67f7f3fefb415c
ms.sourcegitcommit: 0818f6cc435519699866db07c49133488af323f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285031"
---
# <a name="exporting-to-microsoft-word-report-builder-and-ssrs"></a>Exporting to Microsoft Word (Report Builder and SSRS)
  A extensão de renderização do Word renderiza relatórios para o formato nativo de [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007-2010. O formato é o Office Open XML.  
  
 O renderizador do Word é compatível com o [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007-2010, bem como com o [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 com o Pacote de Compatibilidade do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office para Word, Excel e PowerPoint instalado. 
  
 O tipo de conteúdo dos arquivos gerados por este renderizador é **application/vnd.openxmlformats-officedocument.wordprocessingml.document** , e a extensão de arquivo dos arquivos é .docx.  
  
 A versão anterior da extensão de renderização do Word, compatível com o [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003, é renomeada como Word 2003. Apenas a extensão de renderização do Word está disponível por padrão. Você deve atualizar os arquivos de configuração do Reporting Services para disponibilizar a extensão de renderização do Word 2003. O tipo de conteúdo dos arquivos gerados pelo renderizador do Word 2003 é **application/vnd.ms-word** , e a extensão de nome de arquivo dos arquivos é .doc.  
  
> [!IMPORTANT]  
>  A extensão de renderização [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 é substituída. Para obter mais informações, consulte [recursos preteridos no SQL Server Reporting Services no SQL Server 2014](../deprecated-features-in-sql-server-reporting-services-ssrs.md).  
  
 Depois que o relatório é exportado para um documento do Word, você pode alterar seu conteúdo e criar relatórios com estilo de documento, como etiquetas de endereçamento, ordens de compra ou cartas modelo.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="ReportItemsWord"></a> Itens de relatório no Word  
 Os relatórios exportados para Word aparecem como uma tabela aninhada que representa o corpo do relatório. Uma região de dados tablix é renderizada como uma tabela aninhada que reflete a estrutura da região dos dados no relatório. As caixas de texto e os retângulos são renderizados cada um como uma célula dentro da tabela. O valor da caixa de texto é exibido dentro da célula.  
  
 Imagens, gráficos e barras de dados, minigráficos, mapas e indicadores são renderizados cada um como uma imagem estática dentro da célula da tabela. Hiperlinks e links de detalhamento nesses itens de relatórios são renderizados. Mapas e áreas que podem ser clicados dentro de um gráfico não têm suporte.  
  
 Relatórios de colunas tipo boletins informativos não são renderizados no Word. O corpo de relatório e as imagens de fundo das páginas e as cores não são renderizados.  
  
##  <a name="Pagination"></a> Paginação  
 Após o relatório ser aberto, o Word repagina o relatório inteiro novamente baseado no tamanho da página. A repaginação pode causar a inserção de quebras de páginas em locais onde você não pretendia acrescentá-las e, em alguns casos, pode fazer com que o relatório exportado tenha duas quebras de página sucessivas em uma linha ou até acrescentar páginas em branco. Você pode tentar alterar a paginação do Word ajustando as margens das páginas.  
  
 Este processador dá suporte somente às quebras de página lógicas.  
  
### <a name="page-sizing"></a>Dimensionamento de página  
 Quando o relatório é renderizado, a altura e a largura da página do Word são definidas pelas seguintes propriedades RDL: altura e largura do tamanho do papel, margens direta e esquerda da página e as margens superior e inferior da página.  
  
### <a name="page-width"></a>Largura da Página  
 O Word dá suporte às larguras de página que tiverem até 22 polegadas de largura. Se o relatório for mais largo de que 22 polegadas, mesmo assim o processador irá renderizar o relatório, porém o Word não exibirá o conteúdo do relatório quando em exibição de layout de impressão ou exibição de layout de leitura. Para exibir os dados, alterna para a exibição normal ou para a exibição de layout de Web. Nestes exibições, o Word reduz a quantidade de espaços em branco, exibindo portanto uma parte maior do conteúdo de seu relatório.  
  
 Quando o relatório é renderizado, sua largura aumenta na extensão necessária, atingindo até 22 polegadas, com o intuito de exibir o conteúdo. A largura mínima do relatório baseia-se na propriedade Width do RDL no painel Propriedades.  
  
##  <a name="DocumentProperties"></a> Propriedades do documento  
 O processador do Word grava os seguintes metadados no arquivo DOCX.  
  
|Propriedades do Elemento de Relatório|Descrição|  
|-------------------------------|-----------------|  
|Título do Relatório (título do relatório)|Title|  
|Autor do Relatório|Autor|  
|Descrição do Relatório|Comentários|  
  
##  <a name="ReportHeadersFooters"></a> Cabeçalhos e rodapés de página  
 Os cabeçalhos e os rodapés das páginas são renderizados no Word como regiões de rodapé e cabeçalho. Se o número de página de um relatório ou uma expressão que indica o número total de páginas do relatório aparecer no cabeçalho ou rodapé da página, eles são transferidos para um campo do word para que o número preciso da página seja exibido no relatório renderizado. Se a altura do cabeçalho ou do rodapé estiver definida no relatório, o Word não poderá dar suporte a esta configuração. A propriedade PrintOnFirstPage pode, em algumas circunstâncias, especificar se o texto do cabeçalho e do rodapé de uma página é impresso na primeira página de um relatório. Se o relatório renderizado tiver várias páginas, e cada página contiver somente uma única seção, você poderá definir PrintOnFirstPage como False e o texto será suprimido na primeira página; caso contrário, o texto será impresso independentemente do valor da propriedade PrintOnFirstPage.  
  
 O renderizador do Word tenta analisar todas as expressões em cabeçalhos e rodapés de páginas quando estes são exportados para o Word. Muitos formulários de expressões são analisados com êxito, e os valores esperados aparecem nos rodapés e cabeçalhos de todas as páginas do relatório.  
  
 No entanto, quando um rodapé ou um cabeçalho da página contém uma expressão complexa que é avaliada como valores diferentes em páginas diferentes de um relatório, o mesmo valor pode ser exibido em todas as páginas do relatório. Os números de página nas duas expressões a seguir não incrementam no relatório exportado. O número da página é traduzido como o mesmo valor em todas as páginas do relatório.  
  
-   `="Page: " + Globals!PageNumber.ToString + " of " + Globals!TotalPages.ToString`  
  
-   `=Avg(Fields!YTDPurchase.Value, "Sales") & " Page Number " & Globals!PageNumber`  
  
 Isto ocorre porque o renderizador do Word analisa o relatório em busca de campos relacionados à paginação como **PageNumber** e **TotalPages** , e trata somente de referências simples, não chamadas para uma função. Neste caso, a expressão chama a função **ToString** . As duas expressões a seguir são equivalentes e ambas renderizam corretamente quando você visualiza o relatório no Construtor de Relatórios ou Designer de Relatórios, ou quando renderiza o relatório publicado no Gerenciador de Relatórios ou em uma biblioteca do SharePoint. Porém, o renderizador do Word analisa somente a segunda expressão com êxito e renderiza os números de página corretos.  
  
-   **Expressão complexa:**  A expressão é `="Average Sales " & Avg(Fields!YTDPurchase.Value, "Sales") & " Page Number " & Globals!PageNumber`  
  
-   **Expressão com Execuções de Texto:** Texto, **Média de Vendas** e a expressão, `=Avg(Fields!YTDPurchase.Value, "Sales)`, e o texto, **Número da Página** e a expressão `=Globals!PageNumber`  
  
 Para evitar esse problema, use várias sequências de texto em vez de uma expressão complexa quando usar expressões em rodapés e cabeçalhos. As duas expressões a seguir são equivalentes. A primeira é uma expressão complexa, e a segunda usa sequências de texto. O renderizador de Word analisa somente a segunda expressão com êxito.  
  
##  <a name="Interactivity"></a> Interatividade  
 Alguns elementos interativos têm suporte no Word. A seguir, uma descrição dos comportamentos específicos.  
  
### <a name="show-and-hide"></a>Mostrar e Ocultar  
 O processador do Word renderiza os itens de relatório com base no seu estado quando renderizado. Se o estado de um item de relatório for oculto, este item não será renderizado no documento do Word. Se o estado de um item de relatório for mostrado, oculto, este item será renderizado no documento do Word. A funcionalidade para alternar não tem suporte no Word.  
  
### <a name="document-map"></a>Mapa do documento  
 Se etiquetas de mapas de documentos existirem no relatório, elas são renderizadas como etiquetas de Índice nos itens e grupos do respectivo item de relatório. A etiqueta do mapa do documento é usada como o texto de etiqueta para as etiquetas de TOC. O link de destino é posicionado perto do item no qual a etiqueta está definida. Mesmo se um TOC não é criado para você no documento do Word, você pode montar seu próprio TCO usando as etiquetas de mapa do documento que são renderizadas no relatório.  
  
### <a name="hyperlink-and-drillthrough-links"></a>Hiperlink e Links de detalhamento  
 Hiperlinks e links de detalhamento in caixa de texto e itens de relatório tipo imagem são renderizados como hiperlinks no documento de Word. Quando você clicar no hiperlink, o navegador padrão da Web será aberto e navegará para a URL. Quando você clicar no hiperlink de detalhamento, o servidor de relatório originando é acessado.  
  
### <a name="interactive-sorting"></a>Classificação interativa  
 Os conteúdos de relatório são renderizados com base em como eles estão classificados no momento dentro da região de dados do relatório. O Word não dá suporte à classificação interativa. Após o relatório ser renderizado, você pode aplicar a tabela de classificação do Word.  
  
### <a name="bookmarks"></a>Indicadores  
 Os indicadores no relatórios são renderizados como indicadores do Word. Links de indicadores são renderizados como hiperlinks que se conectam aos rótulos de indicadores no documento. Os rótulos de indicadores devem ter menos de 40 caracteres. O único caractere especial que pode ser usado em um rótulo de indicador é o sublinhado (_). Carateres especiais sem-suporte são eliminados do rótulo do indicador e, se o nome for mais comprido que 40 caracteres, o nome é truncado. Se houver nomes de indicadores duplicados no relatório, esses indicadores não serão renderizados no Word.  
  
##  <a name="WordStyleRendering"></a> Renderização de estilo no Word  
 A seguir uma descrição breve de como os estilos são renderizados no Word.  
  
### <a name="color-palette"></a>Paleta de cores  
 As cores incluídas no relatório são renderizadas no documento do Word.  
  
### <a name="border"></a>Borda  
 As bordas dos itens de relatório, além da borda da página, são renderizadas no Word como bordas de células de tabela.  
  
##  <a name="SquigglyLines"></a> Linhas curvadas em relatórios exportados  
 Quando exportados e exibidos no Word, os dados de relatório ou constantes podem ser sublinhadas com linhas curvadas vermelhas ou verdes. As linhas curvadas vermelhas identificam erros de ortografia. As linhas curvadas verdes identificam erros gramaticais. Isso ocorre quando o relatório inclui palavras que não estão de acordo com a revisão de texto (ortografia e gramática) do idioma de edição que é especificado no Word. Por exemplo, os títulos de coluna de relatório em inglês provavelmente serão sublinhados por linhas curvadas vermelhas quando o relatório for renderizado em uma versão do Word em espanhol. Erros de ortografia percebidos são mais comuns em relatórios do que erros gramaticais percebidos porque relatórios costumam incluir apenas texto curto, e não frases ou parágrafos inteiros.  
  
 A presença de linhas curvadas em relatórios implica que o relatório tem erros, o que provavelmente não ocorre. Você pode remover as linhas curvadas alterando o idioma da revisão de texto para o relatório. Para alterar o idioma da revisão de texto, selecione o conteúdo do relatório e especifique o idioma adequado ao conteúdo. Você pode selecionar todo o documento ou parte dele. No Word 2010, a opção de idioma, **Definir Idioma da Revisão de Texto**, está na área **Idioma** na guia **Revisar** . Após atualizar o conteúdo, salve o documento novamente.  
  
 Dependendo da versão do idioma do programa Office, as ferramentas de revisão de texto (por exemplo, o dicionário) do idioma escolhido são incluídas no programa ou fornecidas em um pacote de idioma do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office que você adquiriu.  
  
 Os tópicos a seguir fornecem informações adicionais sobre como definir opções do Office e do Word.  
  
-   Mude o idioma de edição na caixa de diálogo **Preferências de Idioma do Microsoft Office 2010** ou **Opções do Word** no Word. Para obter mais informações, consulte [Habilitar o uso de outros idiomas nos programas do Office](http://office.microsoft.com/word-help/enable-the-use-of-other-languages-in-your-office-programs-HA010354783.aspx?CTT=1).  
  
-   Adicione pacotes de idiomas do Office e altere o idioma de edição. Para obter mais informações, consulte [Habilitar o uso de outros idiomas nos programas do Office](http://office.microsoft.com/word-help/enable-the-use-of-other-languages-in-your-office-programs-HA010354783.aspx?CTT=1) e [Opções de idioma do Office 2010](http://office.microsoft.com/language/).  
  
> [!NOTE]  
>  Quando você altera o idioma de edição na caixa de diálogo **Preferências de Idioma do Microsoft Office 2010** ou **Opções do Word** no Word, a alteração se aplica a todos os programas do Office.  
  
##  <a name="WordLimitations"></a> Limitações do Word  
 As limitações a seguir são aplicadas pelo [!INCLUDE[ofprword](../../includes/ofprword-md.md)]:  
  
-   As tabelas de Word dão suporte a um máximo de 63 colunas. Se o seu relatório tiver mais de 63 colunas e você tentar renderizá-lo, o Word dividirá a tabela. As colunas adicionais serão colocadas adjacente às 63 colunas exibidas no corpo do relatório. Portanto, as colunas do relatório podem não ser alinhadas conforme o esperado.  
  
-   O Word dá suporte uma largura de página máxima de 22 polegadas e uma altura também de 22 polegadas alto. Se o conteúdo for mais largo que 22 polegadas, alguns dados poderão não ser exibidos no Layout de impressão.  
  
-   O Word ignora as configurações de altura de cabeçalho e rodapé.  
  
-   Após o relatório ser exportado, o Word pagina o relatório novamente. Isto pode fazer com que quebras de página adicionais seja acrescentadas ao relatório renderizado.  
  
-   O Word não repete linhas de cabeçalho na página dois e acima, embora você defina a propriedade RepeatOnNewPage da linha de cabeçalho estática em um tablix (tabela, matriz ou lista) `True`. Você pode definir quebras de página explícitas em seu relatório para forçar linhas de cabeçalho a aparecerem em novas páginas. Porém, como o Word aplica sua própria paginação ao relatório renderizado exportado para o Word, os resultados poderão variar, e a linha de cabeçalho talvez não se repita de maneira previsível. A linha de cabeçalho estática é a linha que contém os cabeçalhos de coluna.  
  
-   Caixas de Texto crescem quando contêm espaços sem-quebras.  
  
-   Quando o texto é exportado para o Word, o texto que apresenta certas fontes com decoração pode gerar glifos inesperados ou não exibidos no relatório renderizado.  
  
##  <a name="WordBenefits"></a> Benefícios do uso do renderizador do Word  
 Além de disponibilizar os recursos que são novos no [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007-2010 para relatórios exportados, os arquivos *.docx de relatórios exportados tendem a ser menores. Os relatórios exportados usando o renderizador do Word são geralmente significativamente menores que os mesmos relatórios exportados usando o renderizador do Word 2003.  
  
## <a name="backward-compatibility-of-exported-reports"></a>Compatibilidade com versões anteriores de relatórios exportados  
 Você pode selecionar um modo de compatibilidade de Word e definir opções de compatibilidade. O renderizador do Word cria documentos com o modo de compatibilidade ligado. Salvar novamente os documentos com o modo de compatibilidade desligado pode afetar o layout do documento.  
  
 Se você desligar o modo de compatibilidade e salvar um relatório novamente, o layout do relatório pode alterar de maneiras inesperadas.  
  
##  <a name="AvailabilityWord"></a> Disponibilidade do renderizador do Word 2003  
 No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o renderizador padrão do Word é a versão que renderiza para o formato nativo do [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007-2010. Esta é a opção do **Word** listada pelos menus **Exportar** no Gerenciador de Relatórios e no SharePoint. A versão anterior, compatível somente com o [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003, é nomeado Word 2003 e listada em menus usando esse nome. A opção de menu **Word 2003** não é visível por padrão, mas um administrador pode torná-la visível atualizando o arquivo de configuração RSReportServer. Para exportar relatórios do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usando o renderizador do Word 2003, atualize o arquivo de configuração RSReportDesigner. Porém, tornar o renderizador do Word 2003 visível não significa disponibilizá-lo em todos os cenários. Como o arquivo de configuração de RSReportServer reside no servidor de relatório, as ferramentas ou produtos de que onde você exporta relatórios devem estar conectados a um servidor de relatório para ler o arquivo de configuração. Se você usar ferramentas ou produtos em modo desconectado ou local, tornar o renderizador do Word 2003 visível não terá efeito. A opção de menu **Word 2003** permanece indisponível. Se você tornar o renderizador do Word 2003 visível no arquivo de configuração RSReportDesigner, a opção de menu **Word 2003** sempre estará disponível na visualização de relatório do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
 A opção de menu do **Word 2003** nunca fica visível nos seguintes cenários:  
  
-   Construtor de Relatórios em modo desconectado e você visualiza um relatório no Construtor de Relatórios. Isso ocorre nas versões [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] e autônoma do Construtor de Relatórios.  
  
-   O Web Part do Visualizador de Relatórios em modo local e o farm do SharePoint não são integrados com um servidor de relatório [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Relatórios no modo Local versus em modo Conectado no Visualizador de Relatórios &#40;Reporting Services no modo do SharePoint&#41;](../local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md)  
  
 Se o renderizador do **Word 2003** estiver configurado para ficar visível, as opções de menu do **Word** e do **Word 2003** estarão disponíveis nos seguintes cenários:  
  
-   Gerenciador de Relatórios quando o Reporting Services está instalado no modo nativo.  
  
-   Site do SharePoint quando o Reporting Services é instalado no modo integrado do SharePoint.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e visualização de relatórios  
  
-   Construtor de Relatórios conectado a um servidor de relatórios. Esta pode ser uma versão [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] ou autônoma do Construtor de Relatórios.  
  
-   O Web Part do Visualizador de Relatórios em modo remoto.  
  
 O seguinte XML mostra os elementos para as duas extensões de renderização do Word nos arquivos de configuração RSReportServer e RSReportDesigner:  
  
 `<Extension Name="WORDOPENXML" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordOpenXmlRenderer.WordOpenXmlDocumentRenderer,Microsoft.ReportingServices.WordRendering"/>`  
  
 `<Extension Name="WORD" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordDocumentRenderer,Microsoft.ReportingServices.WordRendering" Visible="false"/>`  
  
 A extensão WORDOPENXML define o renderizador do Word para o [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007-2010. A extensão WORD define a versão do [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003. `Visible = "false"` indica que o renderizador do Word 2003 está oculto. Para obter mais informações, consulte [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md) e [RSReportDesigner Configuration File](../report-server/rsreportdesigner-configuration-file.md).  
  
##  <a name="Differences"></a> Diferenças entre os renderizadores do Word 2003 e Word  
 Relatórios, renderizados usando renderizadores do Word ou Word 2003 tendem a ser visualmente indistinguíveis. Porém, você pode notar diferenças sutis entre os dois formatos do Word ou Word 2003.  
  
##  <a name="DeviceInfo"></a> Configurações de informações de dispositivo  
 É possível alterar algumas configurações padrão para este processador, como omitir hiperlinks e links de detalhamento ou expandir todos os itens que podem ser alternados independentemente do estado original do item quando renderizado, mudando as configurações das informações do dispositivo. Para obter mais informações, consulte [Word Device Information Settings](../word-device-information-settings.md).  
  
## <a name="see-also"></a>Consulte também  
 [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidade interativa para extensões de renderização de relatório diferentes &#40;Construtor de Relatórios e SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [Renderizando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
