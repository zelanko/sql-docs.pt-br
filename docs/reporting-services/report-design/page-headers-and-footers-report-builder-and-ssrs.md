---
title: Cabeçalhos e rodapés de página (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10125"
- sql13.rtp.rptdesigner.pagefooter.border.f1
- "10121"
- "10120"
- "10122"
- sql13.rtp.rptdesigner.pageheader.general.f1
- "10123"
- sql13.rtp.rptdesigner.pageheader.fill.f1
- sql13.rtp.rptdesigner.pageheader.border.f1
- sql13.rtp.rptdesigner.pagefooter.fill.f1
- sql13.rtp.rptdesigner.pagefooter.general.f1
- "10124"
ms.assetid: 4fb9faac-511e-404a-b8d7-1f2e3cb47b11
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1835b4d7a6ede5de5d442f36fe2ea7c85e9e330d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33027033"
---
# <a name="page-headers-and-footers-report-builder-and-ssrs"></a>Cabeçalhos e rodapés de página (Construtor de Relatórios e SSRS)
  Um relatório pode conter um cabeçalho e um rodapé nas partes superior e inferior de cada página, respectivamente. Os cabeçalhos e rodapés podem conter texto estático, imagens, linhas, retângulos, bordas, cor e imagens de plano de fundo e expressões. Expressões incluem referências a campos de conjunto de dados de relatórios com exatamente um conjunto de dados e chamadas de função de agregação que incluem o conjunto de dados como um escopo.  
  
> [!NOTE]  
>  Cada extensão de processamento processa as páginas de maneira diferente. Para obter mais informações sobre extensões de renderização e paginação de relatório, consulte [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
 Por padrão, relatórios têm rodapés de página, mas não cabeçalhos de página. Para obter mais informações sobre como adicionar ou removê-los, consulte [Adicionar ou remover um cabeçalho ou rodapé de página &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md).  
  
 Em geral, cabeçalhos e rodapés contêm números de página, títulos de relatório e outras propriedades de relatório. Para obter mais informações sobre como adicionar esses itens ao cabeçalho ou rodapé do relatório, consulte [Exibir números de página ou outras propriedades do relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/display-page-numbers-or-other-report-properties-report-builder-and-ssrs.md).  
  
 Depois que você criar um cabeçalho de página ou rodapé, ele será exibido em cada página do relatório. Para obter mais informações sobre como suprimir cabeçalhos e rodapés de página da primeira e da última página, consulte [Ocultar um cabeçalho ou rodapé de página na primeira ou na última página &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/hide-a-page-header-or-footer-on-the-first-or-last-page-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-headers-and-footers"></a>Cabeçalhos e rodapés de relatórios  
 Cabeçalhos e rodapés de página não são iguais aos cabeçalhos e rodapés de relatório. Os relatórios não têm uma área especial para cabeçalho ou rodapé de relatório. Um cabeçalho de relatório consiste nos itens de relatório que são colocados na parte superior do corpo do relatório na superfície de design de relatório. Eles aparecem somente uma vez como o primeiro conteúdo no relatório. Um rodapé de relatório consiste de itens de relatório que são colocados na parte inferior do corpo de relatório. Eles aparecem somente uma vez como o último conteúdo no relatório.  
  
## <a name="displaying-variable-data-in-a-page-header-or-footer"></a>Exibindo dados variáveis em um cabeçalho ou rodapé de página  
 Os cabeçalhos e rodapés de página podem incluir conteúdo estático, porém o mais comum é a exibição de conteúdo variável, como números de página ou informações sobre o conteúdo da página. Para exibir dados variáveis que são diferentes em cada página,use uma expressão.  
  
 Se houver apenas um conjunto de dados definido no relatório, você poderá adicionar expressões simples, como `[FieldName]` a um cabeçalho ou rodapé de página. Arraste o campo da coleção de campos do conjunto de dados do painel de dados do relatório ou da coleção Campos Internos para o cabeçalho ou rodapé da página. Uma caixa de texto com a expressão apropriada será adicionada automaticamente.  
  
 Para calcular somas ou outras agregações para os valores da página, é possível usar expressões de agregação que especifiquem ReportItems ou o nome de um conjunto de dados. A coleção ReportItems é a coleção de caixas de texto de cada página depois da renderização do relatório. O nome do conjunto de dados deve existir na definição do relatório. A tabela a seguir exibe os itens suportados em cada tipo de expressão de agregação:  
  
|Suportado na expressão|Agregações de ReportItems|Agregações de conjunto de dados (o escopo deve ser o nome do conjunto de dados)|  
|-----------------------------|----------------------------|----------------------------------------------------------|  
|Caixas de texto no corpo do relatório|Sim|não|  
|&PageNumber|Sim|não|  
|&TotalPages|Sim|não|  
|Função de agregação|Sim. Por exemplo,<br /><br /> `=First(ReportItems!TXT_LastName.Value)`|Sim. Por exemplo,<br /><br /> `=Max(Quantity.Value,"DataSet1")`|  
|Coleção de campos para itens da página|Indiretamente. Por exemplo,<br /><br /> `=Sum(ReportItems!Textbox1.Value)`|Sim. Por exemplo,<br /><br /> `=Sum(Fields!Quantity.Value,"DataSet1")`|  
|Imagem vinculada a dados|Indiretamente. Por exemplo, `=ReportItems!TXT_Photo.Value`|Sim. Por exemplo,<br /><br /> `=First(Fields!Photo.Value,"DataSet1")`|  
  
 As seções seguintes deste tópico apresentam expressões prontas para uso que obtêm dados variáveis geralmente usados em cabeçalhos e rodapés. Também há uma seção sobre como a extensão de renderização do Excel processa cabeçalhos e rodapés. Para obter mais informações sobre expressões, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
### <a name="adding-calculated-page-totals-to-a-header-or-footer"></a>Adicionando totais da página calculados a um cabeçalho ou rodapé  
 Em alguns relatórios, é útil incluir um valor calculado no cabeçalho ou no rodapé de cada relatório; por exemplo, uma soma do total por página se a página contiver valores numéricos. Como não é possível fazer referência aos campos diretamente, a expressão inserida no cabeçalho ou no rodapé deve fazer referência ao nome do item do relatório (por exemplo, uma caixa de texto) e não ao campo de dados:  
  
 `=Sum(ReportItems!Textbox1.Value)`  
  
 Se a caixa de texto estiver em uma tabela ou lista que contém linhas de dados repetidas, o valor exibido no cabeçalho ou no rodapé no tempo de execução será a soma de todos os valores de todos os dados da instância `TextBox1` da tabela ou lista da página atual.  
  
 Ao calcular totais de página, podem haver diferenças nos totais se você usar extensões de renderização diferentes para exibir o relatório. A saída paginada é calculada de forma diferente para cada extensão de renderização. A mesma página exibida em HTML pode mostrar totais diferentes quando exibida em PDF se o volume de dados na página do PDF for diferente. Para obter mais informações, consulte [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
### <a name="for-reports-with-multiple-datasets"></a>Para relatórios com vários conjuntos de dados  
 Para relatórios com mais de um conjunto de dados, não é possível adicionar campos ou imagens vinculadas a dados diretamente a um cabeçalho ou rodapé. No entanto, você pode escrever uma expressão que, indiretamente, faz referência a um campo ou a uma imagem vinculada a dados que você deseja usar em um cabeçalho ou rodapé.  
  
 Para colocar dados variáveis em um cabeçalho ou rodapé:  
  
-   Adicione uma caixa de texto ao cabeçalho ou rodapé.  
  
-   Na caixa de texto, escreva uma expressão que gere os dados variáveis que você deseja exibir.  
  
-   Na expressão, inclua referências a itens do relatório da página; por exemplo, você pode fazer referência a uma caixa de texto que contém dados de um campo em particular. Não inclua uma referência direta a campos de um conjunto de dados. Por exemplo, não é possível usar a expressão `[LastName]`. Você pode usar a expressão seguinte para exibir o conteúdo da primeira instância de uma caixa de texto chamada `TXT_LastName`:  
  
     `=First(ReportItems!TXT_LastName.Value)`  
  
 Não é possível usar funções de agregação em campos no cabeçalho ou rodapé de página. Você só pode usar uma função de agregação em itens de relatório no corpo de relatório. Para obter expressões comuns em cabeçalhos e rodapés de página, consulte [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md).  
  
#### <a name="adding-a-data-bound-image-to-a-header-or-footer"></a>Adicionando uma imagem vinculada a dados a um cabeçalho ou rodapé  
 Você pode usar dados de imagem armazenados em um banco de dados em um cabeçalho ou rodapé. No entanto, não pode fazer referência a campos do banco de dados diretamente do item de relatório Imagem. Em vez disso, adicione uma caixa de texto ao corpo do relatório e, em seguida, defina a caixa de texto para o campo de dados que contém a imagem (observe que o valor deve ser codificado para base64). Você pode ocultar a caixa de texto do corpo do relatório para evitar mostrar a imagem codificada em base64. Em seguida, é possível fazer referência ao valor da caixa de texto oculta do item de relatório Imagem no cabeçalho ou rodapé de página.  
  
 Por exemplo, suponha que haja um relatório composto por páginas de informações de produto. No cabeçalho de cada página, você deseja exibir uma fotografia do produto. Para imprimir uma imagem armazenada no cabeçalho do relatório, defina uma caixa de texto oculta chamada `TXT_Photo` no corpo do relatório que recupere a imagem do banco de dados e use uma expressão para conferir a ela um valor:  
  
 `=Convert.ToBase64String(Fields!Photo.Value)`  
  
 No cabeçalho, adicione um item de relatório Imagem que usa a caixa de texto `TXT_Photo` , decodificada para mostrar a imagem:  
  
 `=Convert.FromBase64String(ReportItems!TXT_Photo.Value)`  
  
## <a name="using-headers-and-footers-to-position-text"></a>Usando cabeçalhos e rodapés para posicionar texto  
 É possível usar cabeçalhos e rodapés para posicionar texto em uma página. Por exemplo, suponha você esteja criando um relatório que você deseja enviar aos clientes. Você pode usar um cabeçalho ou rodapé para posicionar o endereço do cliente de forma que ele apareça na janela do envelope quando dobrado.  
  
 Se você estiver usando a caixa de texto apenas para popular um cabeçalho ou rodapé, poderá ocultá-la no corpo de relatório. O posicionamento da caixa de texto no corpo do relatório pode definir se o valor aparecerá no cabeçalho ou no rodapé da primeira ou da última página do relatório. Por exemplo, se houver tabelas, matrizes ou listas que fazem com que o relatório tenha várias páginas, o valor da caixa de texto oculta aparecerá na última página. Para que ele apareça na primeira página, posicione a caixa de texto oculta na parte superior do corpo de relatório.  
  
## <a name="designing-reports-with-page-headers-and-footers-for-specific-renderers"></a>Criando relatórios com cabeçalhos e rodapés de página para processadores específicos  
 Quando um relatório é processado, os dados e as informações de layout são combinados. Quando você exibir um relatório, a informações combinadas serão transmitidas a um processador que determinará a quantidade de dados do relatório que caberá em cada página.  
  
 Se você usar um navegador para exibir um relatório do servidor de relatório, o processador de HTML controlará o conteúdo das páginas do relatório que você verá. Se você planeja entregar os relatórios em formatos diferentes daquele usado na exibição ou se planeja imprimir os relatórios em um formato específico, convém otimizar o layout do relatório para o processador que você pretende usar para gerar o formato final. Para obter mais informações sobre a paginação de relatório, consulte [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
### <a name="working-with-page-headers-and-footers-in-excel"></a>Trabalhando com cabeçalhos e rodapés de página no Excel  
 Ao definir cabeçalhos e rodapés de página para relatórios que se destinam à extensão de renderização do Excel, siga estas diretrizes para obter os melhores resultados:  
  
-   Use rodapés de página para exibir números de página.  
  
-   Use cabeçalhos de página para exibir imagens, títulos ou outro texto. Não coloque números de página no cabeçalho.  
  
 No Excel, rodapés de página têm um layout limitado. Se você definir um relatório que contenha itens de relatório complexos no rodapé da página, o rodapé da página não será processado como previsto quando o relatório for exibido no Excel.  
  
 A extensão de renderização do Excel pode acomodar imagens e o posicionamento absoluto de itens de relatório simples ou complexos no cabeçalho de página. Um efeito colateral do suporte a um layout de cabeçalho de página mais rico é o suporte reduzido para o cálculo de números de página no cabeçalho. Na extensão de renderização do Excel, as configurações padrão fazem com que os números de página sejam calculados de acordo com o número de planilhas. Dependendo de como você definir o relatório, isso pode gerar números de página incorretos. Por exemplo, suponha que um relatório seja processado como uma única planilha grande impressa em quatro páginas. Se você incluir informações de número de página no cabeçalho, cada página impressa mostrará "Página 1 de 1" no cabeçalho.  
  
 Uma contagem de páginas mais precisa baseia-se em páginas lógicas que se correlacionam às dimensões de uma página impressa. No Excel, o rodapé de página usa números de página lógicos automaticamente. Para posicionar a contagem de página lógica no cabeçalho da página, defina as configurações de informações de dispositivo para usar cabeçalhos simples. Lembre-se de que, ao usar cabeçalhos simples, você elimina a capacidade de lidar com layout de relatório complexo na região de cabeçalho.  
  
 Para obter mais informações, consulte [Exportando para o Microsoft Excel &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Inserir uma imagem em um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [Retângulos e linhas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)  
  
  
