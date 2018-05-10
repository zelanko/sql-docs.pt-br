---
title: rsProcessingError – erro do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: troubleshooting
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- rsProcessingError
ms.assetid: 414ee58a-8251-4367-9a8e-10c068d17280
caps.latest.revision: 29
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d00747808949e7814ecd87c640d10ca3b8e54e97
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="rsprocessingerror---reporting-services-error"></a>rsProcessingError - Erro do Reporting Services
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|rsProcessingError|  
|Origem do evento|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Texto da mensagem|Ocorreram erros em processamento de relatório.|  
  
## <a name="explanation"></a>Explicação  
 Um ou mais erros foram encontrados durante a publicação, o processamento, a visualização local, a exibição a partir do servidor de relatórios ou a criação de uma assinatura para um relatório. Essa mensagem de erro indica que pelo menos um erro foi detectado.  
  
### <a name="possible-causes"></a>Causas possíveis  
 As possíveis causas incluem:  
  
-   Erro de processamento no servidor de relatórios.  
  
-   Erro de processamento durante o processamento de relatório local ao visualizar um relatório.  
  
-   Expressão de grupo avaliada para um tipo de dados incorreto.  
  
-   Definição de filtro que especificou duas expressões avaliadas para tipos de dados que não puderam ser comparados.  
  
-   Expressão que fez referência a um campo que não existe na coleção Campos.  
  
-   Expressão que incluiu uma chamada de função de agregação com um escopo inválido ou conflitante.  
  
-   Expressão que fez referência a um parâmetro que não existe na coleção Parâmetros de Relatório.  
  
-   Assembly personalizado ou assembly do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que foi implantado incorretamente falhou no carregamento.  
  
-   Um parâmetro que tem o conjunto de propriedades Nullable definido como **False** detectou um valor nulo no parâmetro.  
  
-   Uma expressão da propriedade Hidden de uma região de dados que contém um erro: a referência do objeto não foi definida para uma instância de um objeto.  
  
-   Expressão que incluiu uma chamada de função inválida ou erro de sintaxe.  
  
## <a name="user-action"></a>Ação do usuário  
  
### <a name="finding-more-information"></a>Descobrindo mais informações  
 Proceda de acordo com uma ou mais das seguintes ações:  
  
-   Se você estiver visualizando o relatório a partir de um servidor de relatórios ou se estiver visualizando-o como uma assinatura, procure pelo texto completo da mensagem de erro. Informações adicionais são fornecidas no texto expandido.  
  
-   Se você estiver criando um relatório no Designer de Relatórios e vir esse erro ao visualizar ou publicar o relatório, informações adicionais serão fornecidas na janela Lista de Erros.  
  
-   Se você estiver criando um relatório na Visualização do Designer de Relatórios, procure pelo texto completo da mensagem de erro. Informações adicionais são fornecidas no texto expandido.  
  
-   Se você estiver exibindo um relatório no servidor de relatório e estiver conectado como administrador local no servidor de relatório, poderá exibir a pilha de chamadas clicando com o botão direito do mouse na página e selecionando **Exibir Código-Fonte**. Informações adicionais são fornecidas na pilha de chamadas.  
  
-   Se você estiver conectado como um administrador local no servidor de relatórios, pesquise por `ReportProcessingException`no arquivo de log. As entradas de log contêm mais informações. Normalmente, o arquivo de log do servidor de relatório está localizado em \<*drive*>:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles\ReportServerService__*datetimestamp*.log. Para obter mais informações, consulte [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
### <a name="failed-to-load-expression-host-assembly"></a>Falha ao carregar o assembly de host de expressão  
 Assemblies personalizados devem ter uma assinatura de nome forte e o atributo AllowPartiallyTrustedCallers definido. Para obter mais informações, consulte [Using Custom Assemblies with Reports](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md) e [Understanding Security Policies](../../reporting-services/extensions/secure-development/understanding-security-policies.md).  
  
### <a name="a-built-in-global-name-does-not-exist"></a>Um nome global incorporado não existe  
 Verifique a ortografia nas expressões. Os nomes de campos e parâmetros globais e incorporados fazem distinção entre maiúsculas e minúsculas. Se a expressão estiver causando o erro, verifique se o nome real já existe no relatório e se ele está escrito corretamente. Para obter mais informações, consulte [Coleções internas em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
### <a name="parameter-properties-and-null"></a>Valor nulo e propriedades de parâmetro  
 Um parâmetro de vários valores não pode ser Nulo. Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
### <a name="main-report-with-subreport-could-not-be-processed"></a>Relatório principal com sub-relatório que não possa ser processado  
 Um relatório com sub-relatórios deve ser processado pela mesma versão do processador de relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Durante a atualização de relatórios para a versão atual do esquema de definição de relatórios, o relatório principal e os sub-relatórios poderão ou não ser atualizados ao mesmo tempo. Se a versão não for compatível entre um relatório e seus sub-relatórios, a mensagem a seguir será exibida: "Não foi possível processar o sub-relatório".  
  
 Você deve alterar o relatório principal ou os sub-relatórios de forma que todos os relatórios possam ser processados pela mesma versão do processador de relatórios. Para obter informações sobre o motivo pelo qual um relatório falha ao ser atualizado, consulte [Atualizar relatórios](../../reporting-services/install-windows/upgrade-reports.md).  
  
### <a name="verify-function-calls-are-visual-basic-and-not-sql"></a>Verifique se as chamadas de função são do Visual Basic e não do SQL  
 Você pode usar as funções do SQL em texto de consulta em um banco de dados relacional. As funções do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] não podem ser usadas em texto de consulta.  
  
 No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], as expressões podem usar as funções do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] , funções System.Math ou System.String, funções do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] completamente qualificada ou funções personalizadas que você tenha fornecido em um código ou assembly personalizado. Você não pode usar as funções do SQL em uma expressão.  
  
 Verifique se as chamadas de função feitas na consulta e nas expressões são válidas.  
  
### <a name="cannot-compare-data-types-for-a-filter"></a>Não é possível comparar tipos de dados para um filtro  
 Em uma equação de filtro, a expressão de filtro que define o que filtrar e o valor do filtro devem ser do mesmo tipo de dados a ser comparado. Se ocorrer um dos seguintes erros, modifique a expressão do campo ou o valor do filtro de forma que os tipos de dados se correspondam:  
  
-   O processamento do *\<report item type>* para o *\<report item name>* não pode ser executado. Não é possível comparar dados dos tipos *\<type>* e *\<type>*. Verifique o tipo de dados retornado pelo *\<report item name>*.  
  
-   Falha ao avaliar o *\<property name>*.  
  
-   Falha ao avaliar o *\<property name>*. Isso referencia um campo de conjunto de dados que tem um erro: *\<error string>*.  
  
 Para obter mais informações, consulte [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
### <a name="invalid-or-conflicting-scope-specification-in-an-aggregate-function-call"></a>Especificação de escopo inválida ou conflitante em uma chamada de função de agregação  
 Ao incluir chamadas de função de agregação a uma expressão em uma célula Tablix, o processador do relatório avalia a expressão no escopo de grupos mais internos aos quais a célula pertence.  
  
 Você também pode passar o nome de um escopo específico para uma função de agregação. O escopo pode se referir ao nome de um conjunto de dados, uma região de dados ou ao nome de um escopo superior na hierarquia de dados. Isso se aplica às seguintes mensagens:  
  
-   O '*\<report item name>*' do *\<report item type>* tem um escopo inválido “*\<scope name>*”. O escopo deve ser o escopo atual ou estar contido no escopo atual.  
  
-   A expressão *\<property name>* do '*\<report item name>*' do *\<report item type>* tem um parâmetro de escopo que não é válido para uma função de agregação. O parâmetro de escopo deve ser definido para uma constante de cadeia de caracteres que seja igual ao nome de um grupo que a contenha, ao nome de uma região de dados que a contenha ou ao nome de um conjunto de dados.  
  
 Para funções de agregação que calculam os totais de execução (**Previous**, **RunningValue**ou **RowNumber**), você pode especificar um parâmetro de escopo que seja um nome de grupo de linha ou de coluna, mas não ambos. Isso se aplica à seguinte mensagem de erro:  
  
-   As funções de agregação **Previous**, **RunningValue** ou **RowNumber** usadas nas células de dados do '*\<report item name>*' do *\<report item type>* referenciam escopos de agrupamento nas colunas e linhas do *\<report item type>*. Os parâmetros de escopo de todas as funções de agregação **Previous**, **RunningValue** ou **RowNumber** em um *\<report item type>* podem referenciar agrupamentos de linhas ou agrupamentos de colunas de dados, mas não ambos.  
  
 Para obter mais informações, consulte [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) e [Coleções internas em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
### <a name="default-dataset-scope-for-a-top-level-text-box"></a>Escopo de conjunto de dados padrão para uma caixa de texto de nível superior  
 Não use um escopo padrão para uma caixa de texto adicionada à superfície do design de relatórios quando o relatório tiver mais de um conjunto de dados. Use uma expressão que inclui o nome do conjunto de dados como o escopo e uma função de agregação. Por exemplo, `=First(Fields!FieldName.Value, "DataSet2")`.  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Filtros geralmente usados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md)   
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [Referências de coleções de parâmetros &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
