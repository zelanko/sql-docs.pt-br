---
title: Visão geral da arquitetura lógica (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], examples
- cubes [Analysis Services], about cubes
ms.assetid: 1a547bce-dacf-4d32-bc0f-3829f4b026e1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b945aa26f0cd9137763a3a8d84b0f74c7d2311bc
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "68889606"
---
# <a name="logical-architecture-overview-analysis-services---multidimensional-data"></a>Visão geral da arquitetura lógica (Analysis Services-dados multidimensionais)
  Analysis Services opera em um modo de implantação de servidor que determina a arquitetura de memória e o ambiente de tempo de execução usados por diferentes tipos de modelos de Analysis Services. O modo de servidor é determinado durante a instalação. O **modo multidimensional e de mineração de dados** dá suporte a OLAP e Data Mining tradicionais. O **modo de tabela** dá suporte a modelos de tabela. O **modo integrado do SharePoint** refere-se a uma instância do Analysis Services que foi instalado como PowerPivot para SharePoint, usado para carregar e consultar modelos de dados do Excel ou PowerPivot dentro de uma pasta de trabalho.  
  
 Este tópico explica a arquitetura básica do Analysis Services ao operar em modo multidimensional e de mineração de dados. Para obter mais informações sobre outros modos, consulte tabular [ &#40;SSAS&#41; tabular](../../tabular-models/tabular-models-ssas.md) e [comparando as soluções &#40;tabulares e multidimensionais SSAS&#41;](https://docs.microsoft.com/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas).  
  
## <a name="basic-architecture"></a>Arquitetura básica  
 Uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] pode conter vários bancos de dados e um banco de dados pode ter objetos OLAP e objetos Data Mining ao mesmo tempo. Os aplicativos se conectam a uma instância especificada do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e um banco de dados especificado. Um computador servidor pode hospedar várias instâncias do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. As instâncias de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] são nomeadas como "\<ServerName > \\ < InstanceName \>". A ilustração a seguir mostra todas as relações mencionadas entre [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] objetos.  
  
 ![Relações do AMO em execução de objetos](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/amo-runningobjects.gif "Relações do AMO em execução de objetos")  
  
 As classes básicas são o conjunto mínimo de objetos que são necessários para criar um cubo. Esse conjunto mínimo de objetos é uma dimensão, um grupo de medidas e uma partição. Uma agregação é opcional.  
  
 As dimensões são criadas a partir de atributos e hierarquias. As hierarquias são formadas por um conjunto ordenado de atributos, onde cada atributo do conjunto corresponde a um nível na hierarquia.  
  
 Os cubos são criados a partir de dimensões e grupos de medidas. As dimensões na coleção Dimensions de um cubo pertencem à coleção Dimensions do banco de dados. Grupos de medidas são coleções de medidas que têm a mesma exibição da fonte de dados e têm o mesmo subconjunto de dimensões do cubo. Um grupo de medidas tem uma ou mais partições para gerenciar os dados físicos. Um grupo de medidas pode ter um design de agregação padrão. O design de agregação padrão pode ser usado por todas as partições no grupo de medidas; Além disso, cada partição pode ter seu próprio design de agregação.  
  
 Objetos de servidor  
 Cada instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] é vista como um objeto de servidor diferente no AMO; cada instância diferente é conectada a um objeto <xref:Microsoft.AnalysisServices.Server> por uma conexão diferente. Cada objeto de servidor contém uma ou mais fontes de dados, exibições de fonte de dados e objetos de banco de dados, bem como assemblies e funções de segurança.  
  
 Objetos de dimensão  
 Cada objeto de banco de dados contém vários objetos de dimensão. Cada objeto de dimensão contém um ou mais atributos, que são organizados em hierarquias.  
  
 Objetos de cubo  
 Cada objeto de banco de dados contém um ou mais objetos de cubo. Um cubo é definido por suas medidas e dimensões. As medidas e dimensões em um cubo são derivadas das tabelas e exibições na exibição da fonte de dados na qual o cubo se baseia, ou que é gerado a partir das definições de medida e dimensão.  
  
## <a name="object-inheritance"></a>Herança de objeto  
 O modelo de objeto ASSL contém muitos grupos de elementos repetidos. Por exemplo, o grupo de elementos, "`Dimensions` conter `Hierarchies`", define a hierarquia de dimensão de um elemento. Tanto `Cubes` quanto `MeasureGroups` contêm o grupo de elementos, "`Dimensions` contêm `Hierarchies`".  
  
 A menos que seja substituído explicitamente, um elemento herda os detalhes desses grupos de elementos repetidos do nível superior. Por exemplo, o `Translations` para um `CubeDimension` é o mesmo que o `Translations` para seu elemento ancestral, `Cube`.  
  
 Para substituir explicitamente as propriedades herdadas de um objeto de nível superior, um objeto não precisa repetir explicitamente a estrutura inteira e as propriedades do objeto de nível superior. As únicas propriedades que um objeto precisa declarar explicitamente são as propriedades que o objeto deseja substituir. Por exemplo, um `CubeDimension` pode listar somente os `Hierarchies` que precisam ser desabilitados no `Cube`, ou para os quais a visibilidade precisa ser alterada, ou para os quais alguns detalhes de `Level` não foram fornecidos no nível de `Dimension`.  
  
 Algumas propriedades especificadas em um objeto fornecem valores padrão para a mesma propriedade em um objeto filho ou descendente. Por exemplo, `Cube.StorageMode` fornece o valor padrão para `Partition.StorageMode`. Para valores padrão herdados, o ASSL aplica essas regras para valores padrão herdados:  
  
-   Quando a propriedade do objeto filho é nula no XML, o valor da propriedade usa como padrão o valor herdado. No entanto, se você consultar o valor do servidor, o servidor retornará o valor nulo do elemento XML.  
  
-   Não é possível determinar programaticamente se a propriedade de um objeto filho foi definida diretamente no objeto filho ou herdada.  
  
## <a name="example"></a>Exemplo  
 O cubo Imports contém duas medidas, pacotes e por último, e três dimensões, rota, origem e hora relacionadas.  
  
 ![Exemplo de cubo 1](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/cubeintro1.gif "Exemplo de cubo 1")  
  
 Os valores alfanuméricos menores em relação ao cubo são os membros das dimensões. Os membros de exemplo são terra (membro da dimensão de rota), África (membro da dimensão de origem) e 1º trimestre (membro da dimensão de tempo).  
  
### <a name="measures"></a>Determina  
 Os valores nas células do cubo representam as duas medidas, os pacotes e o último. A medida pacotes representa o número de pacotes importados e a função `Sum` é usada para agregar os fatos. A última medida representa a data de recebimento e a função `Max` é usada para agregar os fatos.  
  
### <a name="dimensions"></a>As  
 A dimensão de rota representa o meio pelo qual as importações atingem seu destino. Os membros dessa dimensão incluem terra, não terrestre, ar, mar, estrada ou trilho. A dimensão de origem representa os locais em que as importações são produzidas, como a África ou a Ásia. A dimensão de tempo representa os trimestres e as metades de um único ano.  
  
### <a name="aggregates"></a>Agregações  
 Os usuários empresariais de um cubo podem determinar o valor de qualquer medida para cada membro de cada dimensão, independentemente do nível do membro dentro da dimensão, porque [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] agrega valores em níveis superiores, conforme necessário. Por exemplo, os valores de medida na ilustração anterior podem ser agregados de acordo com uma hierarquia de calendário padrão usando a hierarquia de tempo de calendário na dimensão de tempo, conforme ilustrado no diagrama a seguir.  
  
 ![Diagrama de medidas organizadas ao longo da dimensão de tempo](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/cubeintro2.gif "Diagrama de medidas organizadas ao longo da dimensão de tempo")  
  
 Além de agregar medidas usando uma única dimensão, você pode agregar medidas usando combinações de membros de dimensões diferentes. Isso permite que os usuários empresariais avaliem medidas em várias dimensões simultaneamente. Por exemplo, se um usuário empresarial quiser analisar importações trimestrais que chegaram pelo ar da hemisfério oriental e da hemisfério ocidental, o usuário comercial poderá emitir uma consulta no cubo para recuperar o conjunto de os seguintes.  
  
||||Packages|||última|||  
|-|-|-|--------------|-|-|----------|-|-|  
||||Todas as fontes|Hemisfério oriental|Hemisfério Ocidental|Todas as fontes|Hemisfério oriental|Hemisfério Ocidental|  
|Todo o tempo|||25110|6547|18563|Dec-29-99|Dec-22-99|Dec-29-99|  
||1º semestre||11173|2977|8196|Jun-28-99|Jun-20-99|Jun-28-99|  
|||1º trimestre|5108|1452|3656|Março de 30-99|Março de 19-99|Março de 30-99|  
|||2º trimestre|6065|1525|4540|Jun-28-99|Jun-20-99|Jun-28-99|  
||2ª metade||13937|3570|10367|Dec-29-99|Dec-22-99|Dec-29-99|  
|||terceiro trimestre|6119|1444|4675|Setembro de 30-99|Setembro de 18-99|Setembro de 30-99|  
|||4º trimestre|7818|2126|5692|Dec-29-99|Dec-22-99|Dec-29-99|  
  
 Depois que um cubo é definido, você pode criar novas agregações ou pode alterar as agregações existentes para definir opções como, por exemplo, se as agregações são pré-calculados durante o processamento ou calculadas no momento da consulta. **Tópico relacionado:** [agregações e designs de agregação](../../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md).  
  
### <a name="mapping-measures-attributes-and-hierarchies"></a>Mapeando medidas, atributos e hierarquias  
 As medidas, os atributos e as hierarquias no cubo de exemplo são derivados das colunas a seguir nas tabelas de fatos e de dimensão do cubo.  
  
|Medida ou atributo (nível)|Membros|Tabela de origem|Coluna de origem|Valor da coluna de exemplo|  
|------------------------------------|-------------|------------------|-------------------|-------------------------|  
|Medida de pacotes|Não aplicável|ImportsFactTable|Packages|12|  
|Última medida|Não aplicável|ImportsFactTable|última|Maio de 03-99|  
|Nível de categoria de rota na dimensão de rota|aterramento, terra|RouteDimensionTable|Route_Category|Não terrestre|  
|Atributo de rota na dimensão de rota|ar, mar, estrada, trilho|RouteDimensionTable|Rota|Sea|  
|Atributo hemisfério na dimensão de origem|Hemisfério oriental, hemisfério ocidental|SourceDimensionTable|Hemisfério|Hemisfério oriental|  
|Atributo continente na dimensão de origem|África, Ásia, AustraliaEurope, N. América, S. Estados|SourceDimensionTable|Continente|Européia|  
|Meio atributo na dimensão de tempo|1º semestre, 2º semestre|Timedimensiontable|Centímetro|2ª metade|  
|Atributo Quarter na dimensão de tempo|1º trimestre, 2º trimestre, 3º trimestre, 4º trimestre|Timedimensiontable|Distribuição|terceiro trimestre|  
  
 Os dados em uma única célula de cubo geralmente são derivados de várias linhas na tabela de fatos. Por exemplo, a célula de cubo na interseção do membro aéreo, o membro da África e o membro 1º trimestre contêm um valor que é derivado pela agregação das linhas a seguir na tabela de fatos **ImportsFactTable** .  
  
|||||||  
|-|-|-|-|-|-|  
|Import_ReceiptKey|RouteKey|SourceKey|TimeKey|Packages|última|  
|3516987|uma|6|uma|15|10-99 de janeiro|  
|3554790|uma|6|uma|40|19-99 de janeiro|  
|3572673|uma|6|uma|34|27-99 de janeiro|  
|3600974|uma|6|uma|45|Fev-02-99|  
|3645541|uma|6|uma|20|Fev-09-99|  
|3674906|uma|6|uma|36|Fev-17-99|  
  
 Na tabela anterior, cada linha tem os mesmos valores para as colunas **RouteKey**, **SourceKey**e **TimeKey** , indicando que essas linhas contribuem para a mesma célula do cubo.  
  
 O exemplo mostrado aqui representa um cubo muito simples, no qual o cubo tem um único grupo de medidas, e todas as tabelas de dimensões são unidas à tabela de fatos em um esquema em estrela. Outro esquema comum é um esquema floco de neve, no qual uma ou mais tabelas de dimensão se unem a outra tabela de dimensão, em vez de ingressar diretamente na tabela de fatos. **Tópico relacionado:** [dimensões &#40;Analysis Services-dados&#41;multidimensionais](../../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md).  
  
 O exemplo mostrado aqui contém apenas uma única tabela de fatos. Quando um cubo tem várias tabelas de fatos, as medidas de cada tabela de fatos são organizadas em grupos de medidas e um grupo de medidas está relacionado a um conjunto específico de dimensões por relações de dimensão definidas. Essas relações são definidas especificando as tabelas participantes na exibição da fonte de dados e a granularidade da relação. **Tópico relacionado:** [relações de dimensão](../../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
## <a name="see-also"></a>Consulte também  
 [Bancos de dados de modelo multidimensional &#40;SSAS&#41;](../multidimensional-model-databases-ssas.md)  
  
  
