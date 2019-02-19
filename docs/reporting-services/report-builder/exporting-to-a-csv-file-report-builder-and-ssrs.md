---
title: Exportando para um arquivo CSV (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 68ec746e-8c82-47f5-8c3d-dbe403a441e5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f7f0033a5ed81cb21d7c77038cf95ec8123c3d64
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56297595"
---
# <a name="exporting-to-a-csv-file-report-builder-and-ssrs"></a>Exportando para um arquivo CSV (Construtor de Relatórios e SSRS)
  A extensão de renderização CSV (Comma-Separated Value) renderiza relatórios paginados como uma representação mesclada dos dados de um relatório padronizado, em formato de texto simples que pode ser facilmente lido e que também permite a troca com vários aplicativos.  
  
 A extensão de renderização do CSV usa um delimitador de caracteres da cadeia de caracteres para separar campos e linhas, um delimitador configurável para ser um caractere diferente de uma vírgula. O arquivo resultante pode ser aberto em um programa de planilha como o [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] ou pode ser utilizado como um formato de importação para outros programas. O relatório exportado torna-se um arquivo .csv e retorna um tipo MIME de **text/csv**.  
  
 Se você quiser trabalhar com dados relacionados a gráficos, barras de dados, minigráficos, medidores e indicadores no [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)], exporte o relatório para um arquivo CSV e abra o arquivo no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  
  
 Consulte [Exportar relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) para obter detalhes sobre como exportar para o formato CSV.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="CSVRendering"></a> Renderização de CSV  
 Quando renderizado usando as configurações padrão, um relatório de CSV tem as seguintes características:  
  
-   A cadeia de caracteres delimitadora de campo padrão é uma vírgula (,).  
  
    > [!NOTE]  
    >  Você pode alterar o delimitador de campo para qualquer caractere que desejar, inclusive o TAB, alterando as configurações de informações de dispositivo. Para obter mais informações, consulte [CSV Device Information Settings](../../reporting-services/csv-device-information-settings.md).  
  
-   A cadeia de caracteres delimitadora de registro é o retorno de carro e a alimentação de linha (\<cr>\<lf>).  
  
-   A cadeia de caracteres qualificadora de texto é formada por aspas (").  
  
     O renderizador de CSV não adiciona qualificadores ao redor de todas as cadeias de caracteres de texto. Os qualificadores de texto são adicionados apenas quando o valor contém o caractere delimitador ou uma quebra de linha.  
  
-   Se o texto contiver uma cadeia de caracteres delimitadora inserida ou uma cadeia de caracteres qualificadora, o qualificador de texto será posicionado ao redor do texto e as cadeias de caracteres qualificadoras inseridas serão duplicadas.  
  
-   A formatação e o layout são ignorados.  
  
 Os seguintes itens são ignorados durante a renderização:  
  
-   Cabeçalho da página  
  
-   Rodapé  
  
-   Itens de relatório personalizados  
  
-   Linha  
  
-   image  
  
-   Retângulo  
  
-   Subtotais automáticos  
  
 Os demais itens do relatório são classificados de cima para baixo e da esquerda para a direita. Cada item é renderizado em uma coluna. Se o relatório aninhou itens de dados como listas ou tabelas, os itens pai serão repetidos em cada registro.  
  
 A tabela a seguir indica a aparência de itens de relatório quando renderizados:  
  
|Item|Comportamento da renderização|  
|----------|------------------------|  
|Caixa de texto|Renderiza o conteúdo da caixa de texto. No modo padrão, os itens são formatados com base nas propriedades de formatação do item. No modo compatível, a formatação pode ser alterada pelas configurações das informações do dispositivo. Para obter mais informações sobre os modos de renderização de CSV, consulte as informações a seguir.|  
|Table|Renderiza expandindo a tabela e criando uma linha e uma coluna para cada linha e coluna no nível mais baixo de detalhe. As linhas e colunas de subtotal não têm cabeçalhos de coluna ou de linha. Não há suporte para relatórios detalhados.|  
|Matriz|Renderiza expandindo a matriz e criando uma linha e uma coluna para cada linha e coluna no nível mais baixo de detalhe. As linhas e colunas de subtotal não têm cabeçalhos de coluna ou de linha.|  
|Lista|Renderiza um registro para cada linha de detalhes ou instância na lista.|  
|Sub-relatório|O item pai é repetido para cada instância de conteúdos.|  
|Gráfico|Renderiza criando uma linha para cada valor de gráfico e rótulos de membro. Os rótulos de séries e categorias em hierarquias são mesclados e incluídos na linha para obter um valor de gráfico.|  
|Barra de dados|Renderiza como um gráfico. Normalmente, uma barra de dados não inclui hierarquias ou rótulos.|  
|Minigráficos|Renderiza como um gráfico. Normalmente, um minigráfico não inclui hierarquias ou rótulos.|  
|Medidor|Renderiza como um único registro com os valores mínimo e máximo da escala linear, valores de início e fim do intervalo e valor do ponteiro.|  
|Indicador|Renderiza como um único registro com o nome do estado ativo, estados disponíveis e o valor de dados.|  
|Mapeamento|Renderiza uma linha com os rótulos e os valores para cada membro do mapa de uma camada do mapa.<br /><br /> Se o mapa tiver várias camadas, os valores nas linhas variarão, dependendo do fato de as camadas do mapa usarem as mesmas regiões de dados do mapa ou regiões de dados do mapa diferentes. Se várias camadas do mapa usarem a mesma região de dados, as linhas conterão dados de todas as camadas.|  
  
### <a name="hierarchical-and-grouped-data"></a>Dados hierárquicos e agrupados  
 Os dados hierárquicos e agrupados devem ser para ser mesclados para que possam ser representados no formato CSV.  
  
 A extensão de renderização mescla o relatório em uma estrutura de árvores que representa os grupos aninhados dentro da região de dados. Para mesclar o relatório:  
  
-   Uma hierarquia de linha é mesclada antes de uma hierarquia de coluna.  
  
-   As colunas são ordenadas da seguinte forma: caixas de texto ordenadas da esquerda para a direita, de cima para baixo, seguida pelas regiões de dados ordenadas da esquerda para a direita, de cima para baixo.  
  
-   Dentro da região de dados, as colunas são ordenadas da seguinte maneira: membros do canto, membros da hierarquia de linha, membros da hierarquia de coluna e, em seguida, as células.  
  
-   As regiões de dados semelhantes são grupos de regiões de dados ou grupos dinâmicos que compartilham uma região de dados comum ou o ancestral dinâmico. Os dados pares são identificados pela ramificação da árvore mesclada.  
  
 Para obter mais informações, consulte [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
  
##  <a name="RenderingModes"></a> Modos do renderizador  
 A extensão de renderização CSV pode operar em dois modos: um otimizado para o Excel e o outro otimizado para aplicativos de terceiros que requerem total compatibilidade com a especificação CSV no RFC 4180. Dependendo do modo usado, as regiões de dados semelhantes são controladas de maneira diferente.  
  
### <a name="default-mode"></a>Modo Padrão  
 O modo Padrão é otimizado para Excel. Quando renderizado no modo padrão, o relatório é renderizado como um arquivo CSV com várias seções de dados renderizados por CSV. Cada região de dados semelhante é delimitada por uma linha vazia. As regiões de dados semelhantes dentro do corpo do relatório são renderizadas como blocos de dados separados dentro do arquivo CSV. O resultado é um arquivo CSV em que:  
  
-   As caixas de texto individuais do relatório são renderizadas como o primeiro bloco de dados dentro do arquivo CSV.  
  
-   Cada região de dados semelhante de nível superior no corpo do relatório é renderizada em seu próprio bloco de dados.  
  
-   As regiões de dados aninhadas são renderizadas diagonalmente no mesmo bloco de dados.  
  
#### <a name="formatting"></a>Formatação  
 Os valores numéricos são renderizados em seus estados de formatação. O Excel pode reconhecer os valores numéricos formatados, como moeda, porcentagem e data, e formatar as células de maneira adequada quando importar o arquivo CSV.  
  
### <a name="compliant-mode"></a>Modo Compatível  
 O modo Compatível é otimizado para aplicativos de terceiros.  
  
#### <a name="data-regions"></a>Regiões de Dados  
 Apenas a primeira linha do arquivo contém os cabeçalhos de coluna e cada linha tem o mesmo número de colunas.  
  
#### <a name="formatting"></a>Formatação  
 Os valores não são formatados.  
  
##  <a name="Interactivity"></a> Interatividade  
 A interatividade não é suportada por formatos de CSV gerados por este renderizador. Os elementos interativos a seguir não são renderizados:  
  
-   Hiperlinks  
  
-   Mostrar ou ocultar  
  
-   Mapa do documento  
  
-   Links de detalhamento ou de clique  
  
-   Classificação de usuário final  
  
-   Cabeçalhos fixos  
  
-   Indicadores  
  
  
##  <a name="DeviceInfo"></a> Configurações de informações de dispositivo  
 Você pode alterar algumas configurações padrão deste renderizador, incluindo qual o modo de processamento, quais caracteres serão usados como delimitadores e quais caracteres serão usados como a cadeia de caracteres padrão do qualificador de texto, alterando as configurações de informações de dispositivo. Para obter mais informações, consulte [CSV Device Information Settings](../../reporting-services/csv-device-information-settings.md).  
  
  
## <a name="see-also"></a>Consulte Também  
 [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidade interativa para extensões de renderização de relatório diferentes &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Renderizando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
