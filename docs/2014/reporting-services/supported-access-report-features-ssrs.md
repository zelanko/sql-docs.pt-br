---
title: Suporte para recursos de relatório do Access (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], Access reports
- functions [Reporting Services]
- controls [Reporting Services]
- Access reports [Reporting Services]
- properties [Reporting Services], Access reports
- importing reports
- modules [Reporting Services]
ms.assetid: 7ffec331-6365-4c13-8e58-b77a48cffb44
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0d3c218b5e72e231179443c146a6ea3c23747d4e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180606"
---
# <a name="supported-access-report-features-ssrs"></a>Recursos de relatórios do Access com suporte (SSRS)
  Quando você importa um relatório no Designer de Relatórios, o processo de importação converte o relatório do [!INCLUDE[msCoName](../includes/msconame-md.md)] Access em um arquivo de Linguagem RDL do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte a vários recursos do Access. No entanto, devido às diferenças entre o Access e o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], alguns itens são ligeiramente modificados ou não têm suporte. Este tópico descreve como os recursos de relatórios do Access são convertidos em RDL.  
  
## <a name="importing-access-reports"></a>Importando relatórios de acesso  
 Algumas consultas contêm código que é específico ao Access. O código do Access não é importado com o relatório. Além disso, se uma consulta contiver cadeias de caracteres internas, o relatório talvez não seja importado corretamente. Para corrigir isto, substitua as cadeias de caracteres por um código de caracteres. Por exemplo, substitua o caractere de vírgula (,) por CHAR (34).  
  
 O processo de importação não passa corretamente o ponto e vírgula (;) ou caracteres de marcação XML (\<, >, etc.) nas informações de cadeia de caracteres de conexão. Se uma cadeia de conexão contiver um ponto-e-vírgula ou um caractere de marcação XML, você precisará definir manualmente a senha no novo relatório após a importação do relatório.  
  
 O processo de importação não importa as configurações de conexão ou tempo limite geral na cadeia de conexão. Talvez seja necessário ajustar essas configurações depois que o relatório for importado.  
  
 Se você importar um relatório que tenha uma consulta contendo parâmetros de consulta, esta não será convertida quando o relatório for importado. Para importar a consulta com o relatório, substitua temporariamente os parâmetros de consulta no relatório do Access por valores embutidos em código e, em seguida, substitua-os por parâmetros de consulta depois que o relatório for importado.  
  
## <a name="page-layout"></a>Layout da página  
 O layout de página no Access é diferente do layout no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. O Access organiza os itens na página usando "faixas", ou seja, seções organizadas verticalmente na página. Essas seções podem incluir o cabeçalho do relatório, o rodapé do relatório, o cabeçalho da página, o rodapé da página, grupos e detalhes. O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] fornece um layout mais flexível. As regiões de dados fornecem agrupamento e detalhes, e você pode colocar várias regiões de dados em qualquer lugar no corpo do relatório, até mesmo lado a lado. O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] também inclui um cabeçalho e um rodapé da página em tiras, semelhantes ao cabeçalho e ao rodapé do Access.  
  
 Quando um relatório é importado do Access para o Designer de Relatórios, o cabeçalho e o rodapé de página do relatório do Access são convertidos em cabeçalho e rodapé de página de relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Os grupos e detalhes são convertidos em uma região de dados de lista. O cabeçalho e o rodapé são colocados no corpo do relatório, e não em uma faixa separada. Isso pode resultar em posicionamento de itens um pouco diferente do que no relatório do Access.  
  
> [!NOTE]  
>  Em alguns relatórios do Access, os itens de relatório que parecem estar adjacentes podem na verdade estar sobrepostos. Quando o relatório é importado com o Designer de Relatórios, essa sobreposição não é corrigida e pode levar a resultados inesperados quando o relatório é executado.  
  
## <a name="data-sources"></a>Fontes de dados  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte a fontes de dados OLE DB, como [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se você estiver importando relatórios de um arquivo de projeto do Access (.adp), a cadeia de conexão para a fonte de dados será obtida da cadeia de conexão no arquivo .adp. Se você estiver importando relatórios de um arquivo de banco de dados do Access (.mdb ou .accdb), a cadeia de conexão poderá apontar para o banco de dados do Access e talvez seja necessário corrigi-la após a importação dos relatórios. Se a fonte de dados para o relatório do Access for uma consulta, as informações da consulta serão armazenadas sem modificações no RDL. Se a fonte de dados para o relatório do Access for uma tabela, o processo de conversão criará uma consulta baseada no nome da tabela e nos campos da tabela.  
  
## <a name="reports-with-custom-modules"></a>Relatórios com módulos personalizados  
 Se não houver personalizado [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] código contido nos módulos, ele não será convertido. Se o Designer de relatórios encontrar código durante o processo de importação, um aviso será gerado e exibido na **lista de tarefas** janela.  
  
## <a name="report-controls"></a>Controles de relatório  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte aos controles do Access a seguir e os inclui em definições do relatório convertidas.  
  
|||||  
|-|-|-|-|  
|image|Rótulo|Linha|Retângulo|  
|SubForm|SubReport<br /><br /> **Observação** enquanto um controle SubReport seja convertido dentro do relatório principal, o sub-relatório em si é convertido separadamente.|TextBox||  
  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não dá suporte aos seguintes controles:  
  
|||||  
|-|-|-|-|  
|BoundObjectFrame|CheckBox|ComboBox|CommandButton|  
|CustomControl|ListBox|ObjectFrame|OptionButton|  
|TabControl|ToggleButton|||  
  
 Se o Designer de relatórios encontrar qualquer um desses controles durante o processo de importação, um aviso será gerado e exibido na **lista de tarefas** janela.  
  
 Outros controles, como o ActiveX e Office Web Components, não serão importados. Por exemplo, se um relatório do Access contiver um controle OWC Chart, ele não será convertido quando o relatório for importado.  
  
## <a name="report-properties"></a>Propriedades de relatório  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte às propriedades a seguir, que estão disponíveis através da interface do usuário do Access. As propriedades disponíveis apenas no código não são suportadas e não são listadas aqui.  
  
|||||  
|-|-|-|-|  
|BackColor|BackStyle|BorderColor|BorderStyle|  
|BorderWidth|BottomMargin|CanGrow (caixa de texto)|CanShrink (caixa de texto)|  
|Legenda|FontBold|FontItalic|FontName|  
|FontSize|FontUnderline|FontWeight|ForceNewPage|  
|ForeColor|Altura|HideDuplicates|Hyperlink|  
|IsHyperlink|IsVisible|KeepTogether (grupo)|Left (à esquerda)|  
|LeftMargin|LineSlant|LineSpacing|LinkChildFields|  
|LinkMasterFields|NewRowOrCol|PageFooter|PageHeader|  
|Páginas|Imagem|PictureTiling (relatório)|ReadingOrder|  
|RepeatSection|RightMargin|RunningSum|SizeMode|  
|TextAlign|TOP|TopMargin|Largura|  
  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não dá suporte às propriedades a seguir, que estão disponíveis através da interface do usuário do Access.  
  
|||||  
|-|-|-|-|  
|CanGrow (seção)|CanShrink (seção)|DecimalPlaces|FastLaserPrinting|  
|Filtrar|FilterOn|Formato|FormatConditions|  
|GrpKeepTogether|KeepTogether (seção)|NumeralShapes|Orientação|  
|PaintPalette|PaletteSource|PictureAlignment|PicturePages|  
|PictureSizeMode|PictureTiling (imagem)|ScrollBars|SpecialEffect|  
|Vertical||||  
  
## <a name="grouping"></a>Agrupamento  
 O Access define um nível de grupo usando uma combinação de três propriedades: a expressão de grupo, a propriedade `GroupOn` e a propriedade `GroupInterval`. Um grupo que não tenha um cabeçalho ou rodapé de grupo é mesclado com o grupo contido nele. Se o grupo não contiver outro grupo, a classificação será aplicada à seção de detalhes e o grupo será descartado.  
  
## <a name="expressions"></a>Expressões  
 O Access usa expressões para especificar valores que aparecem em caixas de texto. O Access usa o [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] como sua linguagem de expressão, além de algumas funções de agregação. O Designer de Relatórios converte essas expressões do Access em expressões de relatório.  
  
### <a name="functions"></a>Funções  
 Uma definição de relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] usa o [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET como linguagem de expressão nativa, enquanto o Access 2002 usa o Visual Basic. As listas a seguir descrevem as funções suportadas pelo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
#### <a name="array-functions"></a>Funções de matriz  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte às seguintes funções de matriz:  
  
-   LBound  
  
-   UBound  
  
#### <a name="conversion-functions"></a>Funções de conversão  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte às seguintes funções de conversão:  
  
|||||  
|-|-|-|-|  
|Asc|CBool|CByte|CCur|  
|CDate|CDbl|CDec|Chr|  
|Chr$|CInt|CLng|CSng|  
|CStr|CVar|CVDate|Formato|  
|FormatCurrency|FormatDateTime|FormatNumber|FormatPercent|  
|Hex|Hex$|Nz|Oct|  
|Oct$|Str|Str$|StrConv|  
|Val||||  
  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não dá suporte às seguintes funções de conversão:  
  
-   GUIDFromString  
  
-   StringFromGUID  
  
#### <a name="database-functions"></a>Funções de banco de dados  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte às funções de banco de dados a seguir.  
  
|||||  
|-|-|-|-|  
|CreateReport|GetObject|HyperlinkPart|Partition|  
  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não dá suporte às funções de banco de dados a seguir.  
  
|||||  
|-|-|-|-|  
|CodeDb|CreateControl|CreateForm|CreateGroupLevel|  
|CreateObject|CreateReportControl|CurrentDb|CurrentUser|  
|DeleteControl|DeleteReportControl|Eval|IMEStatus|  
|SysCmd||||  
  
#### <a name="datetime-functions"></a>Funções Data/Hora  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte às funções de data/hora a seguir.  
  
|||||  
|-|-|-|-|  
|data|Date$|DateAdd|DateDiff|  
|DatePart|DateSerial|DateValue|Day|  
|Hora|Minuto|Month|MonthName|  
|Agora|Segundo|Hora|Time$|  
|Timer|TimeSerial|TimeValue|Dia de semana|  
|WeekdayName|Year|||  
  
#### <a name="ddeole-functions"></a>Funções DDE/OLE  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não dá suporte às funções DDE/OLE a seguir.  
  
|||||  
|-|-|-|-|  
|DDE|DDEIntitate|DDERequest|DDESend|  
|LoadPicture||||  
  
#### <a name="domain-aggregate-functions"></a>Funções de agregação de domínio  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não dá suporte às funções de agregação de domínio a seguir.  
  
|||||  
|-|-|-|-|  
|DAvg|DCount|DFirst|DLast|  
|DLookup|DMax|DMin|DStDev|  
|DStDevP|DSum|DVar|DVarP|  
  
#### <a name="error-handling-functions"></a>Funções de tratamento de erros  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte às funções de tratamento de erros a seguir.  
  
|||||  
|-|-|-|-|  
|Err|Erro|Error$|IsError|  
  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não dá suporte à seguinte função de tratamento de erros:  
  
-   CVErr  
  
#### <a name="financial-functions"></a>Funções financeiras  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte às funções financeiras a seguir.  
  
|||||  
|-|-|-|-|  
|DDB|FV|IPmt|IRR|  
|MIRR|NPer|NPV|Pmt|  
|PPmt|PV|Rate|SLN|  
|SYD||||  
  
#### <a name="interaction-functions"></a>Funções de interação  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte às funções de interação a seguir.  
  
|||||  
|-|-|-|-|  
|Comando|Command$|CurDir|CurDir$|  
|DeleteSetting|Dir|Dir$|Environ|  
|Environ$|EOF|FileAttr|FileDateTime|  
|FileLen|FreeFile|GetAllSettings|GetAttr|  
|GetSetting|Loc|LOF|QBColor|  
|RGB|SaveSetting|Seek|SetAttr|  
|Shell|Spc|Tab||  
  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não dá suporte às funções de interação a seguir.  
  
|||||  
|-|-|-|-|  
|DoEvents|Entrada|Entrada|Input$|  
  
#### <a name="inspection-functions"></a>Funções de inspeção  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte às funções de inspeção a seguir.  
  
|||||  
|-|-|-|-|  
|IsArray|IsDate|IsEmpty|IsError|  
|IsNull|IsNumeric|IsObject|TypeName|  
|VarType||||  
  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não dá suporte à seguinte função de inspeção:  
  
-   IsMissing  
  
#### <a name="math-functions"></a>Funções matemáticas  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte às funções matemáticas a seguir.  
  
|||||  
|-|-|-|-|  
|Abs|Atn|Cos|Exp|  
|Fix|Int|Log|Rnd|  
|Arredondamento|Sgn|Sin|Sqr|  
|Tan||||  
  
#### <a name="message-functions"></a>Funções de mensagem  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não dá suporte às funções de mensagem a seguir.  
  
|||||  
|-|-|-|-|  
|InputBox|InputBox$|MsgBox||  
  
#### <a name="program-flow-functions"></a>Funções de fluxo de programa  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte às funções de fluxo de programa a seguir.  
  
|||||  
|-|-|-|-|  
|Choose|IIf|Opção||  
  
#### <a name="sql-aggregate-functions"></a>Funções de agregação SQL  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte às funções de agregação SQL a seguir.  
  
|||||  
|-|-|-|-|  
|Avg|Count|Max|Mín|  
|StDev|StDevP|SUM|Var|  
|VarP||||  
  
#### <a name="text-functions"></a>Funções de texto  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte às funções de texto a seguir.  
  
|||||  
|-|-|-|-|  
|Formato|Format$|InStr|InStrRev|  
|LCase|LCase$|Left (à esquerda)|Left$|  
|Len|LTrim|LTrim$|Mid|  
|Mid$|Substituir|Right (à direita)|Right$|  
|RTrim|Space|Space$|StrComp|  
|StrConv|Cadeia de caracteres|String$|StrReverse|  
|Trim|Trim$|UCase|UCase$|  
  
### <a name="constants"></a>Constantes  
 O Access não dá suporte a constantes especiais do [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] (por exemplo, `vbTrue`) em expressões, assim nenhuma conversão é necessária. Porém, há uma exceção: a palavra-chave `Null` é convertida em `System.DbNull.Value`.  
  
### <a name="parameters"></a>Parâmetros  
 Durante o processo de importação, o Designer de Relatórios verifica cada expressão em um relatório à procura de variáveis que não correspondam a controles ou nomes de campos. Essas variáveis são adicionadas a parâmetros de relatório.  
  
 O tipo de dados para parâmetros de procedimento armazenado é sempre importado como cadeia de caracteres. Depois que o relatório é importado, você deve alterar o parâmetro manualmente para usar o tipo de dados correto.  
  
### <a name="object-names"></a>Nomes de objeto  
 O Access permite que os campos tenham o mesmo nome que os controles; o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não permite. O [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 6.0 permite espaços em nomes de variáveis; o .NET de Visual Basic não permite. O processo de importação substitui os nomes de todos esses objetos por nomes válidos e atribui nomes exclusivos, caso mais de um objeto tenha o mesmo nome. Cada expressão é verificada, e os nomes de variáveis que correspondem a objetos renomeados são substituídos pelos novos nomes.  
  
## <a name="rectangles-and-containment"></a>Retângulos e confinamento  
 Em uma definição de relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], retângulos podem conter outros itens de relatório. Qualquer retângulo maior do que o item de relatório e que sobreponha mais de 90 por cento de sua área se torna um contêiner do item de relatório.  
  
## <a name="bitmaps"></a>Bitmaps  
 Todos os bitmaps inseridos em um relatório são convertidos no formato .bmp quando o relatório é importado, independentemente de seus formatos iniciais. Por exemplo, se o seu relatório incluir arquivos .jpg e .gif, os recursos resultantes importados com o relatório serão arquivos .bmp. Os bitmaps são armazenados como imagens inseridas no relatório. Para obter informações sobre imagens inseridas, consulte [imagens &#40;construtor de relatórios e SSRS&#41;](report-design/images-report-builder-and-ssrs.md).  
  
## <a name="other-considerations"></a>Outras considerações  
 Além dos itens anteriores, as seguintes informações se aplicam a relatórios importados do Access:  
  
-   A formatação condicional não é convertida.  
  
-   O campo de descrição em propriedades de relatório no Access não é convertido.  
  
  
