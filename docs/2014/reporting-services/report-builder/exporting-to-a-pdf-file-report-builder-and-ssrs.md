---
title: Exportando para um arquivo PDF (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f22497b7-f6c1-4c7b-b831-8c731e26ae37
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a52a828227c316c37e90f6d2ecc95b3bce85747d
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56295214"
---
# <a name="exporting-to-a-pdf-file-report-builder-and-ssrs"></a>Exportando para um arquivo PDF (Construtor de Relatórios e SSRS)
  A extensão de renderização PDF renderiza um relatório para os arquivos que podem ser abertos no Adobe Acrobat e em outros visualizadores em PDF de terceiros que dão suporte ao PDF 1.3. Embora o PDF 1.3 seja compatível com o Adobe Acrobat 4.0 e versões posteriores, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dá suporte ao Adobe Acrobat 6 ou posterior. A extensão de renderização não requer que o software Adobe renderize o relatório. Porém, os visualizadores de PDF, como o Adobe Acrobat, são necessários para exibir ou imprimir um relatório em formato PDF.  
  
 A extensão de renderização PDF suporta caracteres ANSI e pode traduzir caracteres Unicode do japonês, coreano, chinês tradicional, chinês simplificado, cirílico, hebraico e árabe com certas limitações. Para obter mais informações sobre as limitações, consulte [exportando relatórios &#40;construtor de relatórios e SSRS&#41;](export-reports-report-builder-and-ssrs.md).  
  
 O renderizador PDF é um renderizador físico de páginas e, portanto, tem um comportamento de paginação que difere dos demais renderizadores, tais como o HTML e o Excel. Este tópico fornece informações específicas sobre o renderizador PDF e descreve as exceções às regras.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="FontRequirements"></a> Inserção de fonte  
 Quando possível, a extensão de renderização de PDF insere o subconjunto de cada fonte necessária para exibir o relatório no arquivo PDF. As fontes usadas no relatório devem ser instaladas no servidor de relatório. Quando o servidor de relatórios gera um relatório no formato PDF, ele usa as informações armazenadas nas fontes referenciadas no relatório para criar mapeamentos de caracteres no arquivo PDF. Se a fonte usada não estiver instalada no servidor de relatório, o arquivo PDF resultante talvez não contenha os mapeamentos corretos, e não seja exibido corretamente no momento da visualização.  
  
 As fontes são inseridas no arquivo PDF quando as condições seguintes se aplicam:  
  
-   Privilégios de inserção de fontes são concedidos pelo autor da fonte. As fontes instaladas incluem uma propriedade que indica se o autor da fonte pretende permitir sua inserção em um documento. Se o valor de propriedade for EMBED_NOEMBEDDING, a fonte não será inserida no arquivo PDF. Para obter mais informações, consulte "TTGetEmbeddingType" no msdn.microsoft.com.  
  
-   A fonte é TrueType.  
  
-   As fontes são referenciadas por itens visíveis em um relatório. Se uma fonte for referenciada por um item que tem a propriedade Hidden definida como True, a fonte não será necessária para exibir dados renderizados e não será incluída no arquivo. As fontes somente são inseridas quando necessárias para exibir os dados de relatório renderizados.  
  
 Se todas essas condições forem atendidas para uma fonte, ela será inserida no arquivo PDF. Se uma ou mais dessas condições não forem atendidas para uma fonte, ela não será inserida no arquivo PDF.  
  
> [!NOTE]  
>  Embora as condições sejam atendidas, há uma circunstância em que as fontes não são inseridas no arquivo PDF. Se as fontes usadas constarem na especificação de PDF geralmente conhecida como fontes do tipo padrão 1 ou as quatorzes fontes básicas, as fontes não serão inseridas para o conteúdo ANSI.  
  
  
  
### <a name="fonts-on-the-client-computer"></a>Fontes no computador cliente  
 Quando uma fonte é inserida no arquivo, o computador usado para exibir o relatório (o computador cliente) não precisa ter a fonte certa instalada para que o relatório seja exibido corretamente.  
  
 Quando uma fonte não é inserida no arquivo PDF, o computador cliente precisa ter a fonte correta instalada para que o relatório seja devidamente exibido. Se a fonte não estiver instalada no computador cliente, o arquivo PDF exibirá um caractere de ponto de interrogação (?) para os caracteres não suportados.  
  
### <a name="verifying-fonts-in-a-pdf-file"></a>Verificando fontes em um arquivo PDF  
 As diferenças na saída PDF ocorrem frequentemente quando uma fonte que não suporta caracteres não latinos é usada em um relatório e então são adicionados caracteres não latinos ao relatório. Você deve testar a saída de renderização do PDF no servidor de relatório e nos computadores do cliente para verificar se o relatório é renderizado corretamente.  
  
 Não dependa da exibição do relatório na Visualização ou exportação para HTML porque o relatório parecerá correto devido à substituição de fontes automática executada pela interface de design gráfico ou pelo Microsoft Internet Explorer, respectivamente. Se houver marcas visuais Unicode faltando no servidor, você poderá ver os caracteres substituídos por um ponto de interrogação (?). Se houver uma fonte ausente no cliente, você verá os caracteres substituídos por caixas (□).  
  
 As fontes incorporadas no arquivo PDF são incluídas na propriedade Fonts salva com o arquivo, como metadados.  
  
##  <a name="Metadata"></a> Metadados  
 Além do layout do relatório, a extensão de renderização do PDF grava os seguintes metadados no Dicionário de Informações do Documento PDF.  
  
|Propriedade do PDF|Criado em|  
|------------------|------------------|  
|`Title`|O atributo `Name` do elemento RDL `Report`.|  
|`Author`|O elemento RDL `Author`.|  
|`Subject`|O elemento RDL `Description`.|  
|`Creator`|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|`Producer`|Nome e versão da extensão de renderização.|  
|`CreationDate`|Tempo de execução do relatório no formato PDF `datetime`.|  
  
  
  
##  <a name="Interactivity"></a> Interatividade  
 Alguns elementos interativos têm suporte em PDF. A seguir, uma descrição dos comportamentos específicos.  
  
### <a name="show-and-hide"></a>Mostrar e Ocultar  
 Os elementos dinâmicos de exibição e ocultação não tem suporte no PDF. O documento PDF é renderizado para corresponder o estado atual dos itens no relatório. Por exemplo, se o item for exibido quando o relatório é executado inicialmente, então o item será renderizado. As imagens que podem ser alternadas não são renderizadas, se elas forem ocultadas quando o relatório é exportado.  
  
### <a name="document-map"></a>Mapa do documento  
 Se houver rótulos de mapas de documento presentes no relatório, um esboço do documento será adicionando ao arquivo PDF. Cada rótulo do mapa do documento aparece como uma entrada no esboço do documento para que apareça no relatório. No Acrobat, um indicador de destino é adicionado ao esboço do documento somente se a página onde ele está for renderizada.  
  
 Se apenas uma única página for renderizada, nenhum esboço de documento será adicionado. O mapa do documento é organizado hierarquicamente para refletir o nível de aninhamento no relatório. O esboço de documento é acessível em Acrobat sob a guia Marcadores. Clicando em uma entrada dentro do esboço de documento faz com que o documento seja enviado para o local indicado.  
  
### <a name="bookmarks"></a>Indicadores  
 Os indicadores são têm suportes na renderização do PDF.  
  
### <a name="drillthrough-links"></a>Links de detalhamento  
 Os links de detalhamento não têm suporte na renderização do PDF. Os links de detalhamento não são renderizados como links clicáveis e relatórios detalhados não podem se conectar ao destino do detalhamento.  
  
### <a name="hyperlinks"></a>Hiperlinks  
 Hiperlinks em relatórios são renderizados como links no arquivo em PDF. Quando você clica no Acrobat, ele abre o navegador de cliente padrão e navega até o URL do hiperlink.  
  
  
  
##  <a name="Compression"></a> Compactação  
 A compactação de imagens se baseia no tipo original do arquivo da imagem. A extensão de renderização do PDF compacta os arquivos em PDF por padrão.  
  
 Para preservar a compactação de imagens incluídas no arquivo em PDF, quando possível, as imagens JPEG são armazenadas como JPEG e todos os demais tipos de imagens são armazenados como BMP.  
  
> [!NOTE]  
>  Os arquivos PDF não têm suporte para a incorporação de imagens PNG.  
  
  
  
##  <a name="DeviceInfo"></a> Configurações de informações de dispositivo  
 Você pode alterar algumas configurações padrão desse renderizador alterando as configurações de informações de dispositivo. Para obter mais informações, consulte [PDF Device Information Settings](../pdf-device-information-settings.md).  
  
  
  
## <a name="see-also"></a>Consulte também  
 [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidade interativa para extensões de renderização de relatório diferentes &#40;Construtor de Relatórios e SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [Renderizando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
