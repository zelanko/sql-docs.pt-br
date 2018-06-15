---
title: Exportando para XML (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-builder
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 11d72068-2d97-495e-948f-12d1e8c1957d
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aef21b126ae81b8821943f70594f04c5118e8446
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33023103"
---
# <a name="exporting-to-xml-report-builder-and-ssrs"></a>Exportando para XML (Construtor de Relatórios e SSRS)
  A extensão XML de renderização retorna um relatório paginado no formato XML. O esquema para o XML do relatório é específico para este relatório e contém somente dados. As informações de layout não são renderizadas e a paginação não é mantida pela extensão XML de renderização. O XML gerado por esta extensão pode ser importado para um banco de dados, usado como uma mensagem de dados XML ou enviado para um aplicativo personalizado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="ReportItems"></a> Itens de relatório  
 A tabela a seguir descreve como os itens de relatório são renderizados.  
  
|Item|Comportamento da renderização|  
|----------|------------------------|  
|Relatório|Renderiza como elemento de nível superior do documento XML.|  
|Regiões de dados|Renderiza como um elemento dentro do elemento do respectivo contêiner. Regiões de dados incluem tabela, matriz e lista que exibem dados como texto e gráfico, barras de dados, minigráficos, indicadores e indicadores que visualizam dados.|  
|Seções de grupo e de detalhes|Cada instância renderiza como um elemento dentro do elemento do respectivo contêiner.|  
|Caixa de texto|Renderiza como um atributo ou elemento do respectivo contêiner.|  
|Retângulo|Renderiza como um elemento dentro do respectivo contêiner.|  
|Grupos de colunas de matriz|Renderiza como elementos dentro de grupos de linhas.|  
|Mapeamento|Renderiza como um elemento dentro do elemento do respectivo contêiner. As camadas do mapa são elementos filho do mapa e cada uma delas contém elementos para seus membros de mapa e atributos de membros de mapa.|  
|Gráfico|Renderiza como um elemento dentro do elemento do respectivo contêiner. Séries são elementos filho do gráfico e categorias são elementos filho de uma série. Renderiza todos os rótulos de gráfico para cada valor de gráfico. Rótulos e valores são incluídos como atributos.|  
|Barra de dados|Renderiza como um elemento dentro do elemento do respectivo contêiner, semelhante a um gráfico. Normalmente, uma barra de dados não inclui hierarquias ou rótulos, apenas valores.|  
|Minigráficos|Renderiza como um elemento dentro do elemento do respectivo contêiner, semelhante a um gráfico. Normalmente, um minigráfico não inclui hierarquias ou rótulos, apenas valores.|  
|Medidor|Renderiza como um elemento dentro do elemento do respectivo contêiner. Renderiza como um único elemento com os valores mínimo e máximo da escala, valores de início e fim do intervalo e o valor do ponteiro como atributos.|  
|Indicador|Renderiza como um elemento dentro do elemento do respectivo contêiner, semelhante a um medidor. Renderiza como um único elemento com o nome do estado ativo, estados disponíveis e o valor de dados como atributos.|  
  
 Os relatórios renderizados usando a extensão de renderização XML também seguem estas regras:  
  
-   Os elementos e atributos XML são renderizados na ordem em que aparecem na definição do relatório.  
  
-   A paginação é ignorada.  
  
-   Cabeçalhos e rodapés nas páginas não são renderizados.  
  
-   Os itens ocultos que não podem se tornar visíveis pela alternância não são renderizados. Inicialmente, os itens visíveis e os ocultos que podem tornar-se visíveis por meio da alternância são renderizados.  
  
-   **Images, lines, and custom report items** são ignorados.  
  
  
##  <a name="DataTypes"></a> Tipos de dados  
 Ao elemento ou atributo da caixa de texto é atribuído um tipo de dados XSD baseado nos valores que a caixa de texto exibe.  
  
|Se todos os valores da caixa de texto forem:|O tipo de dados atribuído será:|  
|--------------------------------|---------------------------|  
|**Int16**, **Int32**, **Int64**, **UInt16**, **UInt32**, **UInt64**, **Byte**, **SByte**|**xsd:integer**|  
|**Decimal** (ou **Decimal** e qualquer tipo de dados inteiro ou byte)|**xsd:decimal**|  
|**Float** (ou **Decimal** e qualquer tipo de dados inteiro ou byte)|**xsd:float**|  
|**Double** (ou **Decimal** e qualquer tipo de dados inteiro ou byte)|**xsd:double**|  
|**DateTime ou DataTime Offset**|**xsd:dateTime**|  
|**Time**|**xsd:string**|  
|**Booliano**|**xsd:boolean**|  
|**String**, **Char**|**xsd:string**|  
|Outro|**xsd:string**|  
  
  
##  <a name="XMLSpecificRenderingRules"></a> Regras de renderização específicas de XML  
 As seções a seguir descrevem como as extensões de renderização XML interpretam os itens dentro do relatório.  
  
### <a name="report-body"></a>Corpo do relatório  
 Um relatório é renderizado como elemento raiz do documento XML. O nome do elemento é obtido do conjunto de propriedades DataElementName no painel Propriedades.  
  
 As definições do namespace XML e os atributos de referência do esquema também estão incluídos no elemento do relatório. As variáveis estão destacadas em negrito:  
  
 <**Report** xmlns="**SchemaName**" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:**schemaLocation**="**SchemaNameReportURL**&amp;rc%3aSchema=true" Name="ReportName">  
  
 Os valores das variáveis são os seguintes:  
  
|Nome|Valor|  
|----------|-----------|  
|Relatório|Report.DataElementName|  
|ReportURL|URLEncoded URL absoluto para o relatório no servidor.|  
|SchemaName|Report.SchemaName. Se nulo, então Report.Name. Se o Report.Name for usado, ele será codificado primeiro com XmlConvert.EncodeLocalName.|  
|ReportName|O nome do relatório.|  
  
### <a name="text-boxes"></a>Caixas de texto  
 Caixas de texto são renderizadas como elementos ou atributos de acordo com a propriedade RDL DataElementStyle. O nome do elemento ou atributo é obtido da propriedade RDL TextBox.DataElementName.  
  
### <a name="charts-data-bars-and-sparklines"></a>Gráficos, barras de dados e minigráficos  
 Gráficos, barras de dados e minigráficos são renderizados em XML. Os dados são estruturados.  
  
### <a name="gauges-and-indicators"></a>Indicadores  
 Indicadores são renderizados em XML. Os dados são estruturados.  
  
### <a name="subreports"></a>Sub-relatórios  
 Um sub-relatório é renderizado como um elemento. O nome do elemento é obtido da propriedade RDL DataElementName. A configuração da propriedade TextBoxesAsElements do relatório substitui aquela do sub-relatório. Namespace e atributos XSLT não são adicionados ao elemento de sub-relatório.  
  
### <a name="rectangles"></a>Retângulos  
 Um retângulo é renderizado como um elemento. O nome do elemento é obtido da propriedade RDL DataElementName.  
  
### <a name="custom-report-items"></a>Itens de Relatório Personalizados  
 CRI (CustomReportItems) não são visíveis para a extensão de renderização. Se um item de relatório personalizado existir no relatório, a extensão de renderização o executa como um item de relatório convencional.  
  
### <a name="images"></a>Imagens  
 As imagens não são renderizadas.  
  
### <a name="lines"></a>Linhas  
 As linhas não são renderizadas.  
  
  
### <a name="tables-matrices-and-lists"></a>Tabelas, matrizes e listas  
 Tabelas, matrizes e listas são renderizadas como um elemento. O nome do elemento é obtido da propriedade RDL DataElementName do Tablix.  
  
#### <a name="rows-and-columns"></a>Linhas e Colunas  
 As colunas são renderizadas dentro das linhas.  
  
#### <a name="tablix-corner"></a>Canto do Tablix  
 O canto não é renderizado. Apenas o conteúdo do canto é renderizado.  
  
#### <a name="tablix-cells"></a>Células Tablix  
 As células Tablix são renderizadas como elementos. O nome do elemento é obtido da propriedade RDL DataElementName da célula.  
  
#### <a name="automatic-subtotals"></a>Subtotais automáticos  
 Os subtotais automáticos do Tablix não são renderizados.  
  
#### <a name="row-and-column-items-that-do-not-repeat-with-a-group"></a>Itens de linha e de coluna que não se repetem com um grupo  
 Os itens que não se repetem com um grupo, como os rótulos, subtotais e totais são renderizados como elementos. O nome do elemento é obtido da propriedade RDL TablixMember.DataElementName.  
  
 A propriedade TablixMember.DataElementOutput RDL controla se um item não repetido é renderizado.  
  
 Se a propriedade DataElementName do membro do Tablix não for fornecida, um nome para o item não repetido será gerado dinamicamente neste formulário:  
  
 RowX   Para linhas não repetidas, em que X é um índice de linha baseado em zero no pai atual.  
  
 ColumnY   Para as colunas não repetidas, em que Y é um índice de coluna baseado em zero no pai atual.  
  
 Um cabeçalho não repetente é renderizado como um filho da linha ou coluna que não se repete em um grupo.  
  
 Se um membro não repetitivo não tiver nenhuma Tablix célula correspondente, ele não será renderizado. Isto pode ocorrer no case de uma célula Tablix onde atravessa mais de uma coluna.  
  
#### <a name="rows-and-columns-that-repeat-with-a-group"></a>Linhas e Colunas que se repetem com um grupo  
 Linhas e colunas que se repetem em um grupo são renderizadas de acordo com as regras Tablix.DataElementOutput. O nome do elemento é obtido da propriedade DataElementName.  
  
 Cada valor exclusivo dentro de um grupo é renderizado como um elemento filho do grupo. O nome para o elemento é obtido da propriedade Group.DataElementName.  
  
 Se o valor da propriedade DataElementOutput for igual à Saída, o cabeçalho de um item repetido será renderizado com um filho do elemento de detalhes.  
  
  
##  <a name="CustomFormatsXSLTransformations"></a> Formatos personalizados e transformações XSL  
 Os arquivos XML produzidos pela extensão de renderização XML podem ser transformados em qualquer formato que utiliza as Transformações de XSL (XSLT). Esta funcionalidade pode ser usada para produzir dados em formatos que já não têm suporte pelas extensões de renderização existentes. Considere o uso da extensão de renderização XML e o XSLT antes de tentar criar sua própria extensão de renderização.  
  
  
##  <a name="DuplicateName"></a> Nomes duplicados  
 Se houver nomes de elemento de dados duplicados dentro do mesmo escopo, o processador exibirá uma mensagem de erro.  
  
  
##  <a name="XSLTTransformations"></a> Transformações XSLT  
 O processador XML pode aplicar uma transformação XSLT do lado de servidor para os dados de XML originais. Quando um XSLT é aplicado, o processador emite o conteúdo transformado ao invés dos dados XML originais. A transformação ocorre no servidor, não no cliente.  
  
 O XSLT a ser aplicado à saída é definido no arquivo de definição do relatório com a propriedade DataTransform do relatório ou com o parâmetro XSLT *DeviceInfo* . Se nenhum desses valores for definido, a transformação ocorre sempre que o processador XML é usado. Ao usar assinaturas, o XSLT deve ser definido na propriedade RDL DataTransform.  
  
 Se um arquivo XSLT for especificado, tanto pela propriedade de definição DataTransform como pela definição das informações do dispositivo, o XSLT especificado no DataTransform ocorrerá primeiro, seguido do XSLT definido pelas configurações das informações do dispositivo.  
  
  
###  <a name="DeviceInfo"></a> Configurações de informações de dispositivo  
 Você pode alterar algumas configurações padrão para este processador alterando as configurações de informações de dispositivo, incluindo:  
  
-   Uma transformação (XSLT) para aplicar ao XML.  
  
-   O tipo MIME do documento XML.  
  
-   Se for aplicar cadeias de caracteres de formato aos dados.  
  
-   Se recuar a saída do XML.  
  
-   Se incluir o nome de esquema XML.  
  
-   A codificação para o documento XML.  
  
-   A extensão de arquivo do documento XML.  
  
 Para obter mais informações, consulte [XML Device Information Settings](../../reporting-services/xml-device-information-settings.md).  
  
  
## <a name="see-also"></a>Consulte Também  
 [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidade interativa para extensões de renderização de relatório diferentes &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Renderizando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
