---
title: Exportando para o Microsoft Excel (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 74f726fc-2167-47af-9093-1644e03ef01f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ed18d5f14a2245290e14804d4a64f58beba885d8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107909"
---
# <a name="exporting-to-microsoft-excel-report-builder-and-ssrs"></a>Exporting to Microsoft Excel (Report Builder and SSRS)
  A extensão de renderização Excel do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] renderiza um relatório para o formato nativo do [!INCLUDE[ofprexcel](../../../includes/ofprexcel-md.md)] 2007-2010. Com a extensão de renderização do Excel, a largura de colunas em Excel reflete com maior precisão a largura de colunas em relatórios.  
  
 O formato é o Office Open XML. O tipo de conteúdo dos arquivos gerados por este renderizador é **application/vnd.openxmlformats-officedocument.spreadsheetml.sheet** e a extensão de arquivo dos arquivos é .xlsx.  
  
 Você pode alterar algumas configurações padrão desse renderizador alterando as configurações de informações de dispositivo. Para obter mais informações, consulte [Excel Device Information Settings](../excel-device-information-settings.md).  
  
> [!IMPORTANT]  
>  Para evitar mensagens de erro ao exportar um relatório maior que 10 MB para o Excel, instale o service pack mais recente para [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. O problema foi corrigido no SP2.  
>   
>  Para obter mais informações sobre o problema, consulte [Corrigir: O SSRS 2012 não consegue exportar um relatório maior que 10 MB para o formato Excel](https://go.microsoft.com/fwlink/p/?LinkId=402513)  
>   
>  Para obter o service pack mais recente para o [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], consulte [Como obter o service pack mais recente para o SQL Server 2012](https://go.microsoft.com/fwlink/p/?LinkId=402512)  
  
> [!IMPORTANT]  
>  Quando você define um parâmetro do tipo `String`, é exibida para o usuário uma caixa de texto que pode ter qualquer valor. Se um parâmetro de relatório não estiver associado a um parâmetro de consulta e os valores de parâmetro forem incluídos no relatório, um usuário do relatório poderá digitar a sintaxe de expressão, um script ou um URL no valor de parâmetro e processar o relatório em Excel. Se outro usuário exibir o relatório e clicar no conteúdo do parâmetro renderizado, o usuário poderá executar acidentalmente o script ou link mal-intencionado.  
>   
>  Para reduzir o risco de execução acidental de scripts mal-intencionados, só abra relatórios renderizados de fontes confiáveis. Para obter mais informações sobre como proteger relatórios, consulte [Protegendo Relatórios e Recursos](../security/secure-reports-and-resources.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="ExcelLimitations"></a>Limitações do Excel  
 
  [!INCLUDE[ofprexcel](../../../includes/ofprexcel-md.md)] impõe limitações a relatórios exportados devido aos recursos do Excel e de seus formatos de arquivo. Estas são as mais significativas:  
  
-   A largura máxima de coluna está limitada a 255 caracteres ou 1726,5 pontos. O processador não verifica se a largura da coluna é inferior ao limite.  
  
-   A altura de linha máxima é 409 pontos. Se o conteúdo da linha fizer com que a altura da linha aumente além dos 409 pontos, a célula do Excel mostrará uma quantidade parcial de texto até 409 pontos. O restante do conteúdo da célula ainda ficará dentro da célula (até o número máximo de 32.767 caracteres do Excel).

-   Como a altura máxima da linha é de 409 pontos, se a altura definida da célula do relatório for algo maior que 409 pontos, o Excel dividirá o conteúdo da célula em várias linhas. 
  
-   O número máximo de caracteres em uma célula é limitado a 32,767. Se isto for excedido, o processador exibirá uma mensagem de erro.  
  
    > [!NOTE]  
    >  No Excel 2003, aproximadamente 1.000 caracteres são exibidos em uma célula Excel na planilha, mas até o número máximo de caracteres que possam ser editados na barra de fórmulas. Essa limitação não se aplica ao Excel 2007-2010.  
  
-   O número máximo de planilhas não é definido no Excel, mas fatores externos, como memória e espaço em disco, podem levar à aplicação de limitações.  
  
-   Em estruturas de tópico, o Excel só permite até sete níveis aninhados.  
  
-   Se o item de relatório que controla se outro item está alternado não estiver na linha ou coluna anterior ou posterior do item que está sendo alternado, a estrutura de tópicos também será desabilitada.  
  
### <a name="sizes-of-excel-2003-files"></a>Tamanhos de arquivos do Excel 2003  
 Quando são exportados e salvos inicialmente no Excel 2003, os relatórios não usufruem da otimização de arquivo aplicada automaticamente pelo Excel aos arquivos de pasta de trabalho *.xls. O tamanho de arquivo maior pode causar problemas para assinaturas de e-mail e anexos. Para reduzir o tamanho dos arquivos \*.xls para relatórios exportados, abra os arquivos \*.xls e, em seguida, salve novamente as pastas de trabalho. Salvar novamente as pastas de trabalho normalmente reduz os tamanhos de arquivo entre 40 e 50 por cento.  
  
### <a name="text-boxes-and-text"></a>Caixas de texto e texto  
 As seguintes limitações se aplicam a caixas de texto e texto:  
  
-   Valores de caixas de texto que sejam expressões não são convertidos em fórmulas do Excel. O valor da cada caixa de texto é avaliado durante o processamento de relatório. A expressão avaliada é exportada como o conteúdo de cada célula do Excel.  
  
-   As caixas de texto são renderizadas dentro de uma célula do Excel. Tamanho de fonte, fonte, decoração e estilo de fonte são os únicos tipos de formatação suportados em texto individual dentro de uma célula do Excel.  
  
-   O efeito de texto "Linha sobreposta" não tem suporte no Excel.  
  
-   O Excel adiciona um preenchimento padrão de aproximadamente 3,75 pontos à esquerda e à direita das células. Se as configurações de preenchimento de uma caixa de texto forem inferiores a 3,75 pontos e largas o suficiente para acomodar o texto, o texto poderá ser encapsulado no Excel.  
  
    > [!NOTE]  
    >  Para solucionar esse problema, aumente a largura da caixa de texto no relatório.  
  
### <a name="images"></a>Imagens  
 As seguintes limitações também se aplicam:  
  
-   Imagens em segundo plano para itens de relatório são ignoradas porque o Excel não dá suporte a imagens em segundo plano para células individuais.  
  
-   A extensão de renderização do Excel só dá suporte à imagem de fundo do corpo do relatório. Se a imagem de fundo do corpo do relatório for exibida no relatório, a imagem será renderizada como imagem de fundo da planilha.  
  
### <a name="rectangles"></a>Retângulos  
 A seguinte limitação se aplica a retângulos.  
  
-   Os retângulos em rodapés do relatório não são exportados para o Excel. No entanto, os retângulos no corpo do relatório, as células tablix etc. são renderizados como um intervalo das células do Excel.  
  
### <a name="report-headers-and-footers"></a>Cabeçalhos e rodapés de relatórios  
 As seguintes limitações se aplicam a cabeçalhos e rodapés de relatórios:  
  
-   Os cabeçalhos e os rodapés do Excel dão suporte a um máximo de 256 caracteres, inclusive a marcação. A extensão de renderização trunca a cadeia de caracteres em 256 caracteres.  
  
-   
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] não dá suporte a margens em cabeçalhos e rodapés de relatórios. Quando exportados para o Excel, os valores de margem são definidos como zero e qualquer cabeçalho ou rodapé que contenha várias linhas de dados talvez não imprima várias linhas, dependendo das configurações da impressora.  
  
-   As caixas de texto em um cabeçalho ou rodapé mantêm a formatação, mas não o alinhamento durante a exportação para o Excel. Isso ocorre porque os espaços à esquerda e à direita são removidos quando o relatório é renderizado no Excel.  
  
### <a name="merging-cells"></a>Mesclando células  
 A seguinte limitação se aplica à mesclagem de células:  
  
-   Se as células forem mescladas, a quebra automática de linha não funcionará corretamente. Se houver células mescladas em uma linha na qual uma caixa de texto seja renderizada com a propriedade AutoSize, o dimensionamento automático não funcionará.  
  
 O renderizador do Excel é essencialmente um renderizador de layout. A meta é replicar o layout do relatório renderizado da maneira mais próxima possível de uma planilha do Excel para que, assim, as células possam ser mescladas na planilha para preservar o layout do relatório. As células mescladas podem causar problemas porque a funcionalidade de classificação do Excel exige a mesclagem de células de uma maneira muito específica para que a classificação funcione corretamente. Por exemplo, o Excel exige que os intervalos de células mescladas tenham o mesmo tamanho para que sejam classificados.  
  
 Se for importante a classificação dos relatórios exportados para planilhas do Excel, isto poderá ajudar a reduzir o número de células mescladas nas planilhas do Excel que é a causa mais comum de dificuldades com a funcionalidade de classificação do Excel.  
  
-   Não alinhar itens à esquerda e à direita é a causa mais comum de células mescladas. Verifique se as bordas esquerda e direita de todos os itens de relatório estão alinhadas. Alinhar itens com a mesma largura resolverá o problema na maior parte dos casos.  
  
-   Embora alinhe todos os itens com precisão, você talvez encontre, em alguns casos raros, algumas colunas ainda mescladas. Isso pode ser causado pela conversão de unidade interna e pelo arredondamento quando a planilha do Excel é renderizada. Na linguagem RDL, é possível especificar a posição e o tamanho em unidades de medida diferentes, como polegadas, pixels, centímetros e pontos. Internamente, o Excel usa pontos. Para minimizar a conversão e a potencial imprecisão do arredondamento durante a conversão de polegadas e centímetros em pontos, leve em consideração especificar todas as medidas em pontos inteiros para obter resultados mais diretos. Uma polegada tem 72 pontos.  
  
### <a name="report-row-groups-and-column-groups"></a>Grupos de linhas e grupos de colunas de relatórios  
 Os relatórios que incluem grupos de linhas ou grupos de colunas contêm células vazias quando exportados para o Excel. Imagine um relatório que agrupa linhas em canal de vendas e CEP. Cada canal inclui muitos CEPs e cada CEP lista muitos nomes de lojas. A imagem a seguir mostra o relatório.  
  
 ![rs_ExportExcelRpt](../media/rs-exportexcelrpt.gif "rs_ExportExcelRpt")  
  
 Quando o relatório é exportado para o Excel, o CEP só aparece em uma célula da coluna CEP. Dependendo do alinhamento do texto no relatório (parte superior, meio ou parte inferior) o valor estará na primeira, na célula do meio ou na última célula. As outras células estarão vazias. A coluna que contém nomes de lojas não tem nenhuma célula vazia. A imagem a seguir mostra o relatório depois de ser exportado para o Excel. As bordas de célula vermelhas foram adicionadas para dar ênfase. Elas não fazem parte do relatório exportado.  
  
 ![rs_ExportExcelBefore](../media/rs-exportexcelbefore.gif "rs_ExportExcelBefore")  
  
 Isso significa que relatórios com grupos de linhas ou grupos de colunas exigem modificação depois da exportação para o Excel e antes que você possa exibir os dados exportados em tabela dinâmica. Você deve adicionar o valor de grupo às células nas quais eles estão ausentes para transformar a planilha em uma tabela plana com valores em todas as células. A imagem a seguir mostra a planilha atualizada.  
  
 ![rs_ExportExcelAfter](../media/rs-exportexcelafter.gif "rs_ExportExcelAfter")  
  
 Se você criar um relatório com o objetivo específico de exportá-lo para o Excel para análise adicional dos dados do relatório, deverá considerar não incluir grupos de linhas ou de colunas no relatório.  
  
## <a name="excel-renderer"></a>Renderizador do Excel  
  
### <a name="excel-2007-2010-renderer"></a>Renderizador do Excel 2007-2010  
 No [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], o renderizador do Excel padrão é a versão compatível com o [!INCLUDE[ofprexcel](../../../includes/ofprexcel-md.md)] 2007-2010. Esta é a opção do **Excel** listada pelos menus **Exportando** no Gerenciador de Relatórios e no SharePoint.  
  
 Para usar o renderizador do Excel padrão em vez do renderizador anterior do Excel 2003, instale o Pacote de Compatibilidade do Microsoft Office para Word, Excel e PowerPoint, para permitir que versões anteriores do Excel abram os arquivos exportados.  
  
### <a name="excel-2003-renderer"></a>Renderizador do Excel 2003  
  
> [!IMPORTANT]  
>  A extensão de renderização [!INCLUDE[ofprexcel](../../../includes/ofprexcel-md.md)] 2003 é substituída. Para obter mais informações, consulte [recursos preteridos em SQL Server Reporting Services no SQL Server 2014](../deprecated-features-in-sql-server-reporting-services-ssrs.md).  
  
 A versão anterior do renderizador do Excel, compatível com o Excel 2003, agora é chamada Excel 2003 e listada em menus usando esse nome. O tipo de conteúdo dos arquivos gerados por este renderizador é **application/vnd.ms-excel** e a extensão de nome de arquivo dos arquivos é .xls.  
  
 Por padrão, a opção de menu **Excel 2003** não é visível. Um administrador pode torná-la visível em certas circunstâncias, atualizando o arquivo de configuração RSReportServer. Para exportar relatórios do [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] usando o renderizador do Excel 2003, atualize o arquivo de configuração RSReportDesigner.  
  
 A extensão da opção de menu **Excel 2003** nunca fica visível nos seguintes cenários:  
  
-   Construtor de Relatórios em modo desconectado e você visualiza um relatório no Construtor de Relatórios. Como o arquivo de configuração de RSReportServer reside no servidor de relatório, as ferramentas ou produtos de que onde você exporta relatórios devem estar conectados a um servidor de relatório para ler o arquivo de configuração.  
  
     Isso ocorre nas versões [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] e autônoma do Construtor de Relatórios.  
  
-   O Web Part do Visualizador de Relatórios em modo local e o farm do SharePoint não são integrados com um servidor de relatório [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte modo [local versus os relatórios do modo conectado no Visualizador de relatórios &#40;Reporting Services no modo do SharePoint&#41;](../local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md)  
  
 Se o renderizador de opção de menu **Excel 2003** estiver configurado para ficar visível, as opções Excel e Excel 2003 estarão disponíveis nos seguintes cenários:  
  
-   Gerenciador de Relatórios quando o Reporting Services está instalado no modo nativo.  
  
-   Site do SharePoint quando o Reporting Services é instalado no modo integrado do SharePoint.  
  
-   
  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] e visualização de relatórios  
  
-   Construtor de Relatórios conectado a um servidor de relatórios. Esta pode ser uma versão [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] ou autônoma do Construtor de Relatórios.  
  
-   O Web Part do Visualizador de Relatórios em modo remoto.  
  
 O seguinte XML mostra os elementos para as duas extensões de renderização do Excel nos arquivos de configuração RSReportServer e RSReportDesigner:  
  
 `<Extension Name="EXCELOPENXML" Type="Microsoft.ReportingServices.Rendering.ExcelOpenXmlRenderer.ExcelOpenXmlRenderer,Microsoft.ReportingServices.ExcelRendering"/>`  
  
 `<Extension Name="EXCEL" Type="Microsoft.ReportingServices.Rendering.ExcelRenderer.ExcelRenderer,Microsoft.ReportingServices.ExcelRendering" Visible="false"/>`  
  
 A extensão EXCELOPENXML define o renderizador do Excel para o Excel 2007-2010. A extensão EXCEL define a versão do Excel 2003. 
  `Visible = "false"` indica que o renderizador do Excel 2003 está oculto. Para obter mais informações, consulte [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md) e [RSReportDesigner Configuration File](../report-server/rsreportdesigner-configuration-file.md).  
  
### <a name="differences-between-the-excel-2007-2010-and-excel-2003-renderers"></a>Diferenças entre os renderizadores do Excel 2007-2010 e do Excel 2003  
 Relatórios, renderizando usando o renderizador do Excel ou do Excel 2003, costumam ser idênticos e apenas em raras circunstâncias você notará diferenças entre os dois formatos. A tabela a seguir compara os renderizadores do Excel e do Excel 2003.  
  
|Propriedade|Excel 2003|Excel|  
|--------------|----------------|-----------|  
|Máximo de colunas por planilha|256|16.384|  
|Máximo de linhas por planilha|65.536|1.048.576|  
|Número de cores permitido em uma planilha|56 (paleta)<br /><br /> Se mais de 56 cores forem utilizadas no relatório, a extensão de renderização corresponderá à cor necessária de uma das 56 cores já disponíveis na paleta personalizada.|Aproximadamente 16 milhões (cor de 24 bits)|  
|Arquivos compactados em ZIP|Nenhum|compactação em ZIP|  
|Família de fontes padrão|Arial|Calibri|  
|Tamanho da fonte padrão|10pt|11pt|  
|Altura de linha padrão|12,75 pt|15 pt|  
  
 Como o relatório define explicitamente a altura da linha, a altura de linha padrão só afeta linhas dimensionadas automaticamente na exportação para o Excel.  
  
##  <a name="ReportItemsExcel"></a>Itens de relatório no Excel  
 Retângulos, sub-relatórios, corpo do relatório e regiões de dados são renderizados como um intervalo de células do Excel. Caixas de texto, imagens, gráficos, barras de dados, minigráficos, mapas, medidores e indicadores devem ser renderizados dentro de uma célula do Excel, que pode ser mesclada dependendo do layout do restante do relatório.  
  
 Imagens, gráficos, minigráficos, barras de dados, mapas, medidores, indicadores e linhas são posicionados dentro de uma célula do Excel mas eles ficam sobre a grade de célula. Linhas são renderizadas como bordas de célula.  
  
 Gráficos, minigráficos, barras de dados, mapas, medidores e indicadores são exportados como imagens. Os dados que eles descrevem, como os rótulos de valor e membro para um gráfico, não são exportados com eles e não estão disponíveis na pasta de trabalho do Excel, a menos que sejam incluídos em uma coluna ou linha em uma região de dados dentro de um relatório.  
  
 Se desejar trabalhar com dados de gráfico, minigráfico, barra de dados, mapas, medidor e indicador, exporte o relatório para um arquivo .csv ou gere feeds de dados compatíveis com o Atom a partir do relatório. Para obter mais informações, consulte [Exportando para um arquivo CSV &#40;Construtor de Relatórios e SSRS&#41;](exporting-to-a-csv-file-report-builder-and-ssrs.md) e [Gerando feeds de dados com base em relatórios &#40;Construtor de Relatórios e SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md).  
  
## <a name="page-sizing"></a>Dimensionamento de página  
 A extensão de renderização do Excel usa as definições de altura e largura da página para determinar a configuração do papel a ser definida na planilha do Excel. O Excel tenta corresponder as configurações de propriedade PageHeight e PageWidth a um dos tamanhos de papel mais comuns.  
  
 Se nenhuma correspondência for encontrada, o Excel usará o tamanho de página padrão para a impressora. Se a altura do papel for maior que a largura, a orientação será definida como Retrato; caso contrário, será Paisagem.  
  
##  <a name="WorksheetTabNames"></a>Nomes de guias de planilha  
 Quando você exporta um relatório para o Excel, as páginas do relatório criadas por quebras de página são exportadas para planilhas diferentes. Se você forneceu um nome de página inicial para o relatório, cada planilha da pasta de trabalho do Excel terá seu nome por padrão. O nome aparece na guia da planilha. No entanto, como cada planilha em uma pasta de trabalho deve ter um nome exclusivo, um inteiro começando em 1 e incrementado em 1 é acrescentado ao nome da página inicial de cada planilha adicional. Por exemplo, se o nome da página inicial é **Relatório de Vendas por Ano Fiscal**, a segunda planilha será denominada **Relatório de Vendas por Ano Fiscal1**, a terceira **Relatório de Vendas por Ano Fiscal2**e assim por diante.  
  
 Se todas as páginas de relatório criadas por quebras de páginas fornecerem novos nomes de página, cada planilha terá o nome de página associado. No entanto, esses nomes de páginas talvez não sejam exclusivos. Se os nomes de páginas não forem exclusivos, as planilhas serão nomeadas da mesma maneira que as páginas iniciais. Por exemplo, se o nome de página de dois grupos for **Vendas para NW**, uma guia de planilha terá o nome **Vendas para NW**e a outra **Vendas para NW1**.  
  
 Se o relatório não fornecer um nome de página inicial, nem nomes de páginas relacionados às quebras de página, as guias de planilha terão os nomes padrão **Planilha1**, **Planilha2**e assim por diante.  
  
 O Reporting Services fornece propriedades a serem definidas em relatórios, regiões de dados, grupos e retângulos para ajudá-lo a criar relatórios que possam ser exportados para o Excel da maneira desejada. Para obter mais informações, consulte [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
##  <a name="DocumentProperties"></a>Propriedades do documento  
 O processador do Excel grava os metadados a seguir no arquivo Excel.  
  
|Propriedades do Elemento de Relatório|DESCRIÇÃO|  
|-------------------------------|-----------------|  
|Criado|Data e hora da execução do relatório como um valor ISO de data/hora.|  
|Autor|Autor do Relatório|  
|DESCRIÇÃO|Descrição do Relatório|  
|LastSaved|Data e hora da execução do relatório como um valor ISO de data/hora.|  
  
##  <a name="PageHeadersFooters"></a>Cabeçalhos e rodapés de página  
 Dependendo da configuração SimplePageHeaders das Informações do Dispositivo, o cabeçalho da página pode ser renderizado de duas maneiras: o cabeçalho da página pode ser renderizado no topo de cada grade de célula na planilha, ou na seção real do cabeçalho da planilha Excel. Por padrão, o cabeçalho é renderizado à grade de célula na planilha do Excel.  
  
 O rodapé da página é sempre renderizado na seção real do rodapé da planilha Excel, independentemente do valor da configuração SimplePageHeaders.  
  
 As seções de cabeçalho e rodapé suportam um máximo de 256 caracteres, inclusive a marcação. Se este limite for excedido, o processador do Excel removerá os caracteres de marcação iniciando pelo final da cadeia de caracteres do cabeçalho e/ou rodapé a fim de reduzir o número total de caracteres. Se todos os caracteres de marcação forem removidos e ainda assim o comprimento exceder o máximo, a cadeia de caracteres é truncada iniciando-se pela direita.  
  
### <a name="simplepageheader-settings"></a>Configurações SimplePageHeader  
 Por padrão a configuração SimplePageHeaders das Informações do Dispositivo é definido para `False`; portanto, os cabeçalhos da página são renderizados como linhas no relatório na superfície da planilha do Excel. As linhas da planilha com os cabeçalhos se tornam linhas travadas. Você pode congelar ou descongelar o painel no Excel.  
  
> [!NOTE]  
>  Se a opção **Imprimir Títulos** for selecionada, os cabeçalhos serão definidos automaticamente para serem impressos em cada página da planilha.  
>   
>  O cabeçalho da página é repetido no topo de cada planilha na pasta de trabalho exceto a página inicial do mapa do documento se a opção **Imprimir Títulos** for selecionadas na guia Layout da Página no Excel.  
  
 Se a opção **Imprimir na primeira página** ou a opção **Imprimir na última página** não for selecionada nas caixas de diálogo Propriedades do Cabeçalho do Relatório ou Propriedades do Rodapé do Relatório, o cabeçalho não será adicionado nem na primeira nem na última página respectivamente.  
  
 Os rodapés das páginas são renderizados na seção de rodapés do Excel.  
  
 Devido às limitações do Excel, as caixas de texto são o único tipo de item de relatório que pode ser renderizado na seção de cabeçalho/rodapé do Excel.  
  
##  <a name="Interactivity"></a> Interatividade  
 Alguns elementos interativos têm suporte no Excel. A seguir, uma descrição dos comportamentos específicos.  
  
### <a name="show-and-hide"></a>Mostrar e Ocultar  
 
  [!INCLUDE[ofprexcel](../../../includes/ofprexcel-md.md)] tem limitações a respeito de como administra os itens de relatório ocultos e exibidos ao serem exportados. Grupos, linhas e colunas que contêm itens de relatório que podem ser alternados são renderizados como esboços do Excel. O Excel cria esboços que expandam e recolhem linhas e colunas ao longo de toda a linha ou coluna que pode causar o recolhimento de itens de relatório que não devem ser recolhidos. Além disso, os símbolos de estrutura de tópicos do Excel podem tornar-se atravancados com esboços sobrepostos. Para tratar destes assuntos, as seguintes regras para estrutura de tópicos são aplicadas ao usar a extensão de renderização do Excel:  
  
-   O item de relatório no canto superior esquerdo que pode ser alternado pode continuar a ser alternado no Excel. Os itens de relatório que podem ser alternado e compartilham um espaço vertical ou horizontal com o item de relatório que pode ser alternado no canto superior esquerdo não pode ser alterando no Excel.  
  
-   Para determinar se a região dos dados poderá ser recolhida pelas linhas ou colunas, a posição do item de relatório que controla a alternância e a posição do item de relatório sendo alternado serão definidos. Se o item que controla a alternância aparecer antes do item a ser alternado, o item poderá ser recolhido pelas linhas. Caso contrário, o item é recolhido pelas colunas. Se o item que controla a alternância aparecer ao lado e acima da área alternada de modo igual, o item é renderizado com a linha recolhível pelas linhas.  
  
-   Para determinar se os subtotais estão colocados no relatório renderizado, a extensão de renderização examina a primeira instâncias de um membro dinâmico. Se um membro estático do mesmo nível aparecerá imediatamente sobre o mesmo, assume-se que o membro dinâmico seja os subtotais. Os esboços são definidos para indicar que estes são dados de sumários. Se não houver irmãos estáticos de um membro dinâmico, a primeira instância da instância será o subtotal.  
  
-   Devido a uma limitação do Excel, somente esboços de até 7 níveis podem ser aninhados.  
  
### <a name="document-map"></a>Mapa do documento  
 Se rótulos de mapa de documento existirem no relatório, um mapa de documento será renderizado. O mapa de documento é renderizado uma planilha de cobertura Excel inserida na primeira posição da guia na pasta de trabalho. A planilha é nomeada **Mapa do Documento**.  
  
 O texto exibido no mapa de documento é determinado pela propriedade DocumentMapLabel do item de relatório ou grupo. Os rótulos do mapa do documento estão listados na ordem em que eles aparecem no relatório, iniciando na primeira linha, na primeira coluna. Cada célula do rótulo do mapa de documento é recuada o número de níveis que aparece no relatório. Cada nível de recuo é representado colocando o rótulo em uma coluna subsequente. O Excel dá suporte a até 256 níveis de aninhamento de esboços.  
  
 O esboço de mapa de documento é renderizado como um esboço de Excel recolhível. A estrutura do esboço corresponde à estrutura aninhada do mapa de documento. O estado de expansão ou de recolhimento do esboço se inicia ao segundo nível.  
  
 O nó raiz do mapa é o nome de relatório, o \<*reportname*>.rdl e não é interativo. A fonte dos links do mapa do documento é Arial, 10pt.  
  
### <a name="drillthrough-links"></a>Links de detalhamento  
 Os links de detalhamento que aparecem nas caixas de texto são renderizados como hiperlinks Excel na célula em que o texto é renderizado. Os links de detalhamento para imagens e gráficos são renderizados como hiperlinks do Excel na imagem quando renderizada. Quando clicado, o link de detalhamento abre o navegador padrão do cliente e navega para a exibição do HTML de destino.  
  
### <a name="hyperlinks"></a>Hiperlinks  
 Os hiperlinks que aparecem nas caixas de texto são renderizados como hiperlinks Excel na célula em que o texto é renderizado. Os hiperlinks para imagens e gráficos são renderizados como hiperlinks do Excel na imagem quando renderizada. Quando clicado, o hiperlink abre o navegador padrão do cliente e navega ao URL de destino.  
  
### <a name="interactive-sorting"></a>Classificação interativa  
 O Excel não dá suporte à classificação interativa.  
  
### <a name="bookmarks"></a>Indicadores  
 Os links indicadores nas caixas de texto são renderizados como hiperlinks Excel na célula em que o texto é renderizado. Os links indicadores para imagens e gráficos são renderizados como hiperlinks Excel na imagem quando renderizada. Quando clicado, a indicação vai para a célula do Excel na qual o item de relatório indicado é renderizado.  
  
##  <a name="ConditionalFormat"></a>Alterando relatórios em tempo de execução  
 Se um relatório precisar ser renderizado em vários formatos e não for possível criar um layout de relatório que renderize da forma desejada em todos os formatos obrigatórios, você pode considerar usar o valor em RenderFormat global interno para alterar condicionalmente a aparência do relatório em tempo de execução. Dessa forma, é possível ocultar ou mostrar itens de relatório dependendo do renderizador usado para obter os melhores resultados em cada formato. Para obter mais informações, consulte [Referências de globais internas e referências de usuários &#40;Construtor de Relatórios e SSRS&#41;](../report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidade interativa para extensões de renderização de relatório diferentes &#40;Construtor de Relatórios e SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [Renderizando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
