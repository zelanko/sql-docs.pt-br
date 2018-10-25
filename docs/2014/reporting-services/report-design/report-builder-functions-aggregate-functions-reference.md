---
title: Referência de funções de agregação (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: db6542ee-02d0-4073-90e6-cba8f9510fbb
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 7d3a6843ea643ac447e42a1d78f5f2e7b3bc09da
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48194107"
---
# <a name="aggregate-functions-reference-report-builder-and-ssrs"></a>Referência de funções de agregação (Construtor de Relatórios e SSRS)
  Para incluir valores agregados no relatório, é possível usar funções de agregação internas em expressões. A função de agregação padrão para campos numéricos é SUM. É possível editar a expressão e usar uma função de agregação interna diferente ou especificar outro escopo. O escopo identifica qual conjunto de dados deve ser usado no cálculo.  
  
 À medida que o processador de relatório combina os dados e o layout do relatório, as expressões de cada item do relatório são avaliadas. Ao exibir cada página do relatório, você vê os resultados de cada expressão nos itens de relatório renderizados.  
  
 A seguinte tabela lista as categorias de funções internas a serem incluídas em uma expressão:  
  
-   [Funções de agregação internas](#CalculatingAggregates)  
  
-   [Restrições em campos internos, coleções e funções de agregação](#Restrictions)  
  
-   [Restrições em agregações aninhadas](#NestedRestrictions)  
  
-   [Calculando valores em uso](#CalculatingRunningValues)  
  
-   [Recuperando contagens de linhas](#RetrievingRowCounts)  
  
-   [Procurando valores de outro conjunto de dados](#LookupFunctions)  
  
-   [Recuperando valores dependentes de classificação](#RetrievingPostsortValues)  
  
-   [Recuperando agregações do servidor](#RetrievingServerAggregates)  
  
-   [Recuperando nível recursivo](#RetrievingRecursiveLevel)  
  
-   [Testando para escopo](#TestingforScope)  
  
 Para determinar os escopos válidos para uma função, consulte o tópico de referência da função individual. Para obter mais informações e exemplos, consulte [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="CalculatingAggregates"></a> Funções de agregação internas  
 As seguintes funções internas calculam valores resumidos para um conjunto de dados numéricos não nulos no escopo padrão ou no escopo nomeado.  
  
|**Função**|**Descrição**|  
|------------------|---------------------|  
|[Avg](report-builder-functions-avg-function.md)|Retorna a média de todos os valores numéricos não nulos especificados pela expressão, avaliados no escopo fornecido.|  
|[Contagem](report-builder-functions-count-function.md)|Retorna uma contagem de valores não nulos especificados pela expressão, avaliados no contexto do escopo fornecido.|  
|[CountDistinct](report-builder-functions-countdistinct-function.md)|Retorna uma contagem de todos os valores não nulos distintos especificados pela expressão, avaliados no contexto do escopo fornecido.|  
|[Max](report-builder-functions-max-function.md)|Retorna o valor máximo de todos os valores numéricos não nulos especificados pela expressão, no contexto do escopo fornecido. É possível usar essa função para especificar o valor máximo de um eixo do gráfico para controlar a escala.|  
|[Min](report-builder-functions-min-function.md)|Retorna o valor mínimo de todos os valores numéricos não nulos especificados pela expressão, no contexto do escopo fornecido. É possível usar essa função para especificar o valor mínimo de um eixo do gráfico para controlar a escala.|  
|[StDev](report-builder-functions-stdev-function.md)|Retorna o desvio padrão de todos os valores numéricos não nulos especificados pela expressão, avaliados no escopo fornecido.|  
|[StDevP](report-builder-functions-stdevp-function.md)|Retorna o desvio padrão da população de todos os valores numéricos não nulos especificados pela expressão, avaliados no contexto do escopo fornecido.|  
|[Sum](report-builder-functions-sum-function.md)|Retorna a soma de todos os valores numéricos não nulos especificados pela expressão, avaliados no escopo fornecido.|  
|[Union](report-builder-functions-union-function.md)|Retorna a união de todos os valores de dados espaciais não nulos do tipo `SqlGeometry` or `SqlGeography` especificados pela expressão e avaliados no contexto do escopo fornecido.|  
|[Var](report-builder-functions-var-function.md)|Retorna a variação de todos os valores numéricos não nulos especificados pela expressão, avaliados no escopo fornecido.|  
|[VarP](report-builder-functions-varp-function.md)|Retorna a variação da população de todos os valores numéricos não nulos especificados pela expressão, avaliados no contexto do escopo fornecido.|  
  
##  <a name="Restrictions"></a> Restrições em campos internos, coleções e funções de agregação  
 A tabela a seguir resume as restrições em locais no relatório em que é possível adicionar expressões que contêm referências a coleções internas globais.  
  
|Local no relatório|Campos|Parâmetros|ReportItems|PageNumber<br /><br /> TotalPages|DataSource<br /><br /> DataSet|Variáveis|RenderFormat|  
|------------------------|------------|----------------|-----------------|-------------------------------|----------------------------|---------------|------------------|  
|Cabeçalho de página<br /><br /> Rodapé de página|Sim|Sim|No máximo um<br /><br /> Observação 1|Sim|Sim|Sim|Sim|  
|Corpo|Sim<br /><br /> Observação 2|Sim|Apenas itens no escopo atual ou em um escopo contentor<br /><br /> Observação 3|não|Sim|Sim|Sim|  
|Parâmetro de relatório|não|Apenas parâmetros anteriores da lista<br /><br /> Observação 4|não|não|não|não|não|  
|Campo|Sim|Sim|não|não|não|não|não|  
|Parâmetro de consulta|não|Sim|não|não|não|não|não|  
|Expressão de grupo|Sim|Sim|não|não|Sim|não|não|  
|Expressão de classificação|Sim|Sim|não|não|Sim|Sim<br /><br /> Observação 5|não|  
|Expressão de filtro|Sim|Sim|não|não|Sim|Sim<br /><br /> Observação 6|não|  
|Código|não|Sim<br /><br /> Observação 7|não|não|não|não|não|  
|Report.Language|não|Sim|não|não|não|não|não|  
|Variáveis|Sim|Sim|não|não|Sim|Escopo atual ou contentor|não|  
|Agregações|Sim|Sim|Apenas cabeçalho da página/rodapé da página|Apenas em agregações de item de relatório|Sim|não|não|  
|Funções de Lookup|Sim|Sim|Sim|não|Sim|não|não|  
  
-   **Observação 1.** ReportItems deve existir na página de relatório renderizada ou o seu valor será Nulo. Se a visibilidade de um item de relatório depender de uma expressão que é avaliada como False, o item de relatório não existirá na página.  
  
-   **Observação 2.** Se uma referência de campo usada em um escopo de grupo não estiver incluída na expressão de grupo, o valor do campo será indefinido, a menos que haja apenas um valor no escopo. Para especificar um valor, use Primeiro ou Último e o escopo de grupo.  
  
-   **Observação 3.** Expressões que incluem uma referência a ReportItems podem especificar valores para outros ReportItems no mesmo escopo de grupo ou em um escopo de grupo contentor.  
  
-   **Observação 4.** Os valores de propriedade de parâmetros anteriores podem ser nulos.  
  
-   **Observação 5.** Somente em classificações de Membro. Não é possível usar em expressões de classificação de região de dados.  
  
-   **Observação 6.** Somente em filtros de Membro. Não é possível usar em região de dados ou em expressões de filtro de conjunto de dados.  
  
-   **Observação 7.** A coleção Parâmetros não é inicializada até o bloco de Código ser processado. Portanto, os métodos não podem ser usados para controlar parâmetros na inicialização.  
  
-   **Observação 8.** O tipo de dados de todas as agregações - exceto Count e CountDistinct - deve ser o mesmo, ou nulo, para todos os valores.  
  
##  <a name="NestedRestrictions"></a> Restrições em agregações aninhadas  
 A tabela a seguir resume as restrições nas quais as funções de agregação podem especificar outras funções de agregação como agregações aninhadas.  
  
|Contexto|RunningValue|RowNumber|First<br /><br /> Last|Previous|Sum e outras funções de classificação prévia|Agregações de ReportItem|Funções de Lookup|Função de agregação|  
|-------------|------------------|---------------|--------------------|--------------|-------------------------------------|---------------------------|----------------------|------------------------|  
|Valor em uso|não|não|não|não|Sim|não|Sim|não|  
|Primeiro<br /><br /> Last|não|não|não|não|Sim|não|não|não|  
|Previous|Sim|Sim|Sim|não|Sim|não|Sim|não|  
|Sum e outras funções de classificação prévia|não|não|não|não|Sim|não|Sim|não|  
|Agregações de ReportItem|não|não|não|não|não|não|não|não|  
|Funções de Lookup|Sim|Sim<br /><br /> Observação 1|Sim<br /><br /> Observação 1|Sim<br /><br /> Observação 1|Sim<br /><br /> Observação 1|Sim<br /><br /> Observação 1|não|não|  
|Função de agregação|não|não|não|não|não|não|não|não|  
  
-   **Observação 1.** As funções de agregação só serão permitidas na expressão *Source* de uma função Lookup se a função Lookup não estiver contida em uma agregação. As funções de agregação não são permitidas nas expressões *Destination* ou *Result* de uma função Lookup.  
  
##  <a name="CalculatingRunningValues"></a> Calculando valores em uso  
 As funções internas a seguir calculam os valores em uso de um conjunto de dados. `RowNumber` é semelhante a `RunningValue` pois retorna o valor em uso de uma contagem que é incrementada para cada linha no escopo contentor. O parâmetro do escopo dessas funções deve especificar um escopo de contenção que controle quando a contagem é reiniciada.  
  
|**Função**|**Descrição**|  
|------------------|---------------------|  
|[RowNumber](report-builder-functions-rownumber-function.md)|Retorna uma contagem contínua do número de linhas para o escopo especificado. O `RowNumber` função reinicia a contagem em 1, não em 0.|  
|[RunningValue](report-builder-functions-runningvalue-function.md)|Retorna uma agregação contínua de todos os valores numéricos não nulos especificados pela expressão, avaliados para o escopo fornecido.|  
  
##  <a name="RetrievingRowCounts"></a> Recuperando contagens de linhas  
 A função interna a seguir calcula o número de linhas no escopo fornecido. Use esta função para contar todas as linhas, inclusive as linhas com valores nulos.  
  
|**Função**|**Descrição**|  
|------------------|---------------------|  
|[CountRows](report-builder-functions-countrows-function.md)|Retorna o número de linhas no escopo especificado, inclusive as linhas com valores nulos.|  
  
##  <a name="LookupFunctions"></a> Procurando valores de outro conjunto de dados  
 As funções de pesquisa a seguir recuperam valores de um conjunto de dados especificado.  
  
|**Função**|**Descrição**|  
|------------------|---------------------|  
|[Função Lookup](report-builder-functions-lookup-function.md)|Retorna um valor de um conjunto de dados para uma expressão especificada.|  
|[Função LookupSet](report-builder-functions-lookupset-function.md)|Retorna um conjunto de valores de um conjunto de dados para uma expressão especificada.|  
|[Função Multilookup](report-builder-functions-multilookup-function.md)|Retorna o conjunto de primeiros valores correspondentes para um conjunto de nomes de um conjunto de dados que contém pares de nome/valor.|  
  
##  <a name="RetrievingPostsortValues"></a> Recuperando valores dependentes de classificação  
 As funções internas a seguir retornam o primeiro, o último ou o valor anterior de um escopo fornecido. Estas funções dependem da ordem de classificação dos valores dos dados. Use estas funções, por exemplo, para localizar o primeiro e o último valor em uma página para criar um cabeçalho de página em estilo de dicionário. Use `Previous` para comparar um valor em uma linha com o valor da linha anterior dentro de um escopo específico, por exemplo, para localizar porcentagem ano valores de ano em uma tabela.  
  
|**Função**|**Descrição**|  
|------------------|---------------------|  
|[Primeiro](report-builder-functions-first-function.md)|Retorna o primeiro valor no escopo fornecido da expressão especificada.|  
|[Last](report-builder-functions-last-function.md)|Retorna o último valor no escopo fornecido da expressão especificada.|  
|[Anterior](report-builder-functions-previous-function.md)|Retorna o valor ou o valor de agregação especificado para a instância anterior de um item do escopo especificado.|  
  
##  <a name="RetrievingServerAggregates"></a> Recuperando agregações do servidor  
 A função interna a seguir recupera agregações personalizadas do provedor de dados. Por exemplo, usando um tipo de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , é possível recuperar agregações calculadas no servidor de fonte de dados para uso em um cabeçalho de grupo.  
  
|**Função**|**Descrição**|  
|------------------|---------------------|  
|[Agregado](report-builder-functions-aggregate-function.md)|Retorna uma agregação personalizada da expressão especificada, conforme definido pelo provedor de dados.|  
  
##  <a name="TestingforScope"></a> Testando para escopo  
 A função interna a seguir testa o contexto atual de um item de relatório para verificar se ele é membro de um escopo específico.  
  
|Função|Description|  
|--------------|-----------------|  
|[InScope](report-builder-functions-inscope-function.md)|Indica se a instância atual de um item está dentro do escopo especificado.|  
  
##  <a name="RetrievingRecursiveLevel"></a> Recuperando nível recursivo  
 A função interna a seguir recupera o nível atual quando uma hierarquia recursiva é processada. Usar o resultado dessa função com o `Padding` propriedade em uma caixa de texto para controlar o nível de recuo de uma hierarquia visual para um grupo recursivo. Para obter mais informações, consulte [Criar grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
|Função|Description|  
|--------------|-----------------|  
|[Level](report-builder-functions-level-function.md)|Retorna o nível atual de profundidade em uma hierarquia recursiva.|  
  
## <a name="see-also"></a>Consulte também  
 [Usos de expressões em relatórios &#40;relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
