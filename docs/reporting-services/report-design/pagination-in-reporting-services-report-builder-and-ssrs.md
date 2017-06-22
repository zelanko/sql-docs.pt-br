---
title: "Paginação no Reporting Services (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e0894b0d-dc5b-4a75-8142-75092972a034
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b9e295143b577d99732186b0cefda5be908c1c34
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="pagination-in-reporting-services-report-builder--and-ssrs"></a>Paginação no Reporting Services (Construtor de Relatórios e SSRS)
  A paginação se refere ao número de páginas dentro de um relatório e ao modo como os itens de relatório são organizados nessas páginas. A paginação no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] varia, dependendo da extensão de renderização que você usa para exibir e entregar o relatório. Ao executar um relatório no servidor de relatórios, o relatório usa o processador HTML. O HTML segue um conjunto específico de regras de paginação. Por exemplo, se exportar o mesmo relatório para o PDF, o processador do PDF será utilizado e um conjunto de regras diferente será aplicado, portanto, o relatório será paginado de modo diferente. Para desenvolver com êxito um relatório que seja facilmente lido pelos seus usuários bem como que seja otimizado para o processador que pretende usar na entrega do relatório, você deve entender as regras utilizadas para controlar a paginação no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Este tópico abrange o impacto do tamanho físico da página e o layout to relatório sobre como os processadores de quebras de página não flexíveis renderizam o relatório. Você pode configurar as propriedades para modificar o tamanho físico da página e as margens, além de dividir o relatório em colunas, usando o painel **Propriedades do Relatório** , o painel **Propriedades** ou a caixa de diálogo **Configurar Página** . Você pode acessar o painel **Propriedades do Relatório** clicando na área azul fora do corpo do relatório. Além disso, pode acessar a caixa de diálogo **Configurar Página** clicando em **Executar** na guia Página Inicial e depois clicar em **Configurar Página** na guia Executar.  
  
> [!NOTE]  
>  Se você desenvolveu um relatório com a largura de uma página, mas ele se renderiza em várias páginas, verifique se a largura do corpo do relatório, inclusive as margens, não é maior que a largura física do tamanho da página. Para impedir que páginas vazias sejam adicionadas ao relatório, você pode reduzir o tamanho do contêiner arrastando o canto para a esquerda.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="the-report-body"></a>Corpo do relatório  
 O corpo de relatório é um contêiner retangular exibido como espaço branco na superfície do design. Ele pode aumentar ou encolher para acomodar os itens de relatório contidos nele. O corpo do relatório não reflete o tamanho físico da página e, de fato, o corpo do relatório pode aumentar além dos limites do tamanho físico da página para abranger várias páginas do relatório. Alguns processadores, como o [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)], Word, HTML e MHTML, renderizam relatórios que aumentam ou encolhem dependendo do conteúdo da página. Os relatórios renderizados nesses formatos são otimizados para exibição em tela, como no navegador da Web. Quando necessário, esses processadores adicionam quebras de página verticais.  
  
 É possível formatar o corpo do relatório de modo que haja uma cor de borda, um estilo de borda e uma largura de borda. Você também pode adicionar uma cor de fundo e uma imagem em segundo plano.  
  
## <a name="the-physical-page"></a>A página física  
 O tamanho físico da página é o tamanho do papel. O tamanho do papel que você especifica para o relatório controla como o relatório é renderizado. Os relatórios renderizados em formatos de quebra de página não flexível inserem quebras de páginas horizontais e verticais com base no tamanho físico da página a fim de fornecer uma experiência de leitura otimizada quando impresso ou exibido em formato de arquivo com quebras de página não flexíveis. Os relatórios renderizados em formatos de quebra de página flexível inserem quebras de páginas horizontais com base no tamanho físico a fim de fornecer uma experiência de leitura otimizada quando exibido em um navegador da Web.  
  
 Por padrão, o tamanho da página é de 8,5 x 11 polegadas, mas você pode alterar esse tamanho usando o painel **Propriedades do Relatório** , a caixa de diálogo **Configurar Página** ou alterando as propriedades PageHeight e PageWidth no painel **Propriedades** . O tamanho de página não aumenta nem encolhe para acomodar o conteúdo do corpo de relatório. Se desejar que o relatório seja exibido em uma única página, todo o conteúdo dentro do corpo do relatório deve encaixar na página física. Se não couber e usar o formato de quebra de página não flexível, então o relatório necessitará de páginas adicionais. Se o corpo do relatório aumentar além da borda direita da página física, então uma quebra de página serão inserida horizontalmente. Se o corpo do relatório aumentar além da borda inferior da página física, então uma quebra de página serão inserida verticalmente.  
  
 Se quiser substituir o tamanho da página física definida no relatório, você pode especificar o tamanho da página física usando as configurações das Informações de Dispositivo para o processador específico que está sendo usado para exportar o relatório. Para obter mais informações, consulte [Configurações de Informações de Dispositivo do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=102515).  
  
### <a name="margins"></a>Margens  
 As margens são retiradas da borda das dimensões físicas da página para dentro da configuração da margem especificada. Se um item de relatório se estender para dentro da área da margem, ele é anexado de modo que a área sobreposta não seja renderizada. Se especificar tamanho de margens que fazem com que a largura horizontal ou vertical da página se iguala a zero, as configurações da margem se tornarão zero por padrão. As margens são especificadas usando o painel **Propriedades do Relatório** , a caixa de diálogo **Configurar Página** ou alterando as propriedades TopMargin, BottomMargin, LeftMargin e RightMargin no painel **Propriedades** . Se quiser substituir o tamanho da margem definida no relatório, você pode especificar o tamanho da margem usando as configurações das Informações de Dispositivo para o processador específico que está sendo usado para exportar o relatório.  
  
 A área da página física que resta após a alocação do espaço para as margens, espaçamento das colunas e o cabeçalho e rodapé da página, é chamada de *área utilizável da página*. As margens só são aplicadas quando renderizar e imprimir os relatórios em formatos de processador de quebra de página não flexível. A imagem a seguir indica a margem e área utilizável da página de uma página física.  
  
 ![Página física com margens e área utilizável. ] (../../reporting-services/report-design/media/rspagemargins.gif "Página física com margens e área utilizável.")  
  
### <a name="newsletter-style-columns"></a>Colunas com estilo de boletim informativo  
 Seu relatório pode ser dividido em colunas, como as colunas de um jornal, mas são tratadas como páginas lógicas renderizadas na mesma página física. Elas são organizadas da esquerdo para direita, da parte superior para a parte inferior e são separadas por uma espaço em branco entre cada coluna. Se o relatório estiver dividido em mais de uma coluna, cada página física será dividida verticalmente em colunas, cada qual considerada uma página lógica. Por exemplo, suponhamos que você tenha duas colunas em uma página física. O conteúdo de seu relatório preenche a primeira coluna e em seguida a segunda coluna. Se o relatório não couber completamente dentro das duas primeiras colunas, o relatório preenche a primeira coluna e em seguida a segunda coluna na página seguinte. As colunas continuam sendo preenchidas, da esquerda para a direita, da parte superior para a parte inferior até que todos os itens do relatório sejam renderizadas. Se especificar tamanho de colunas que fazem com que a largura horizontal ou vertical se iguala a zero, o espaçamento das colunas se tornará zero por padrão.  
  
 As colunas são especificadas usando o painel **Propriedades do Relatório** , a caixa de diálogo **Configurar Página** ou alterando as propriedades TopMargin, BottomMargin, LeftMargin e RightMargin no painel **Propriedades** . Se quiser usar um tamanho de margem que não está definida, você pode especificar o tamanho da margem usando as configurações das Informações de Dispositivo para o processador específico que está sendo usado para exportar o relatório. As colunas só são aplicadas quando você renderizar e imprimir os relatórios em PDF ou em formatos de Imagem. A imagem a seguir indica a área de página utilizável de uma página que contém colunas.  
  
 ![Página física com colunas representadas. ] (../../reporting-services/report-design/media/rspagecolumns.gif "Página física com colunas representadas.")  
  
## <a name="page-breaks-and-page-names"></a>Quebras de páginas e nomes de página  
 Um relatório pode ser mais legível e seus dados mais fáceis de auditar e exportar quando ele tem nomes de página. O Reporting Services fornece propriedades para relatórios e regiões de dados do tablix (tabela, matriz e lista), grupos e retângulos do relatório para controlar a paginação, reiniciar números de página e fornecer novos nomes de página de relatório em quebras de páginas. Estes recursos podem aprimorar relatórios independentemente do formato no qual eles são renderizados, mas são especialmente úteis ao exportar relatórios para pastas de trabalho do Excel.  
  
 A propriedade InitialPageName fornece o nome da página inicial do relatório. Se seu relatório não incluir nomes de página para quebras de páginas, o nome de página inicial será usado para todas as novas páginas criadas por quebras de páginas. Não é necessário usar um nome de página inicial.  
  
 Um relatório renderizado pode fornecer um novo nome de página para a nova página que uma quebra de página causa. Para fornecer o nome de página, defina a propriedade PageName de uma tabela, matriz, lista, grupo ou retângulo. Não é necessário especificar nomes de página em quebras. Se não fizer, o valor de InitialPageName será usado. Se InitialPageName também for deixado em branco, a nova página não terá nenhum nome.  
  
 Regiões de dados do tablix (tabela, matriz e lista), grupos e retângulos dão suporte a quebras de páginas.  
  
 A quebra de página inclui as seguintes propriedades:  
  
-   BreakLocation fornece o local da quebra para o elemento de relatório habilitado para quebra de página: no início, no fim, ou no início e no fim. Em grupos, BreakLocation pode ser localizado entre grupos.  
  
-   Disabled indica se uma quebra de página está aplicada ao elemento de relatório. Se esta propriedade for avaliada como True, a quebra de página será ignorada. Esta propriedade é usada para desabilitar quebras de páginas dinamicamente com base em expressões quando o relatório é executado.  
  
-   ResetPageNumberindicates indica se o número de página deve ser redefinido para 1 quando uma quebra de página ocorre. Se esta propriedade for avaliada como True, o número da página será redefinido.  
  
 Você pode definir a propriedade BreakLocation nas caixas de diálogo **Propriedades do Tablix**, **Propriedades do Retângulo**ou **Propriedades de Grupo** , mas é necessário definir as propriedades Disabled, ResetPageNumber e PageName no painel Propriedades do Construtor de Relatórios. Se as propriedades no painel Propriedades estiverem organizadas por categoria, você encontrará as propriedades na categoria **PageBreak** . Para grupos, a categoria **PageBreak** está dentro da categoria **Grupo** .  
  
 Você pode usar constantes e expressões simples ou complexas para definir o valor das propriedades Disabled e ResetPageNumber. Contudo, você não pode usar expressões com a propriedade BreakLocation. Para obter mais informações sobre gravar e usar expressões, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
 Em seu relatório, você pode escrever expressões que referenciam os nomes da página atual ou os números de página ao usar a coleção **Globals** . Para obter mais informações, consulte [Referências de globais internas e referências de usuários &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
### <a name="naming-excel-worksheet-tabs"></a>Nomeando guias de planilhas do Excel  
 Estas propriedades são úteis quando você exporta relatórios para pastas de trabalho do Excel. Use a propriedade InitialPage para especificar um nome padrão para o nome da guia da planilha quando você exportar o relatório, e use quebras de páginas e a propriedade PageName para atribuir nomes diferentes a cada planilha. Cada nova página de relatório, definida por uma quebra de página, é exportada para uma planilha diferente nomeada pelo valor da propriedade PageName. Se PageName ficar em branco, mas o relatório tiver um nome de página inicial, todas as planilhas na pasta de trabalho do Excel usarão o mesmo nome, o nome de página inicial.  
  
 Para obter mais informações sobre como essas propriedades funcionam quando os relatórios são exportados para o Excel, consulte [Exportando para o Microsoft Excel &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Layout da página e renderização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/page-layout-and-rendering-report-builder-and-ssrs.md)  
  
  
