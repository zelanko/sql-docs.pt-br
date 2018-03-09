---
title: "Partições (Analysis Services - dados multidimensionais) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- storage [Analysis Services], partitions
- incremental updates [Analysis Services]
- data sources [Analysis Services], partitions
- data storage [Analysis Services]
- aggregations [Analysis Services], partitions
- OLAP objects [Analysis Services], partitions
- storing data [Analysis Services], partitions
- partitions [Analysis Services], about partitions
- cubes [Analysis Services], partitions
- partitions [Analysis Services]
- remote partitions [Analysis Services]
- measure groups [Analysis Services], partitions
ms.assetid: cd10ad00-468c-4d49-9f8d-873494d04b4f
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 1a44581e828d92756c46b897d9e7c9be69144c5b
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="partitions-analysis-services---multidimensional-data"></a>Partições (Analysis Services – Dados Multidimensional)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Uma partição é um contêiner de uma parte dos dados de grupo de medidas. As partições não são vistas a partir das consultas MDX; todas as consultas refletem o conteúdo completo do grupo de medidas, independentemente de quantas partições são definidas para o grupo de medidas. O conteúdo de dados de uma partição é definido pelas associações de consulta da partição e pela divisão da expressão.   
  
 Um objeto simples <xref:Microsoft.AnalysisServices.Partition> é composto de: informações básicas, definição de divisão, design de agregação e outros. As informações básicas incluem o nome da partição, o modo de armazenamento, o modo de processamento e outros. A definição de divisão é uma expressão MDX que especifica uma tupla ou um conjunto. A definição de divisão tem as mesmas restrições que a função MDX StrToSet. Juntamente com o parâmetro CONSTRAINED, a definição de divisão pode usar dimensão, hierarquia, nomes de nível e de membro, chaves, nomes exclusivos e outros objetos nomeados no cubo, mas não pode usar as funções MDX. O design de agregação é uma coleção de definições de agregação que podem ser compartilhadas por várias partições. O padrão é obtido do design de agregação do cubo pai.  
  
 As partições são usadas pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para gerenciar e armazenar dados e agregações para um grupo de medidas em um cubo. Todo grupo de medidas tem pelo menos uma partição e essa partição é criada quando o grupo de medidas é definido. Ao criar uma nova partição para um grupo de medidas, a nova partição é adicionada ao conjunto de partições que já existem para o grupo de medidas. O grupo de medidas reflete os dados combinados contidos em todas as suas partições. Isso significa que você deve assegurar que os dados de uma partição em um grupo de medidas são exclusivos, em relação a qualquer outra partição no grupo de medidas para garantir que os dados não sejam refletidos no grupo de medidas mais de uma vez. A partição original do grupo de medidas tem base em uma única tabela de fatos na exibição da fonte de dados do cubo. Quando há várias partições para o grupo de medidas, cada partição pode fazer referência a uma tabela diferente na exibição da fonte dados ou em uma fonte de dados relacional subjacente do cubo. Mais de uma partição em um grupo de medidas pode fazer referência à mesma tabela, se cada partição estiver restrita a diferentes linhas na tabela.  
  
 As partições são poderosas e flexíveis para gerenciar cubos, especialmente cubos grandes. Por exemplo, um cubo que contém informações de vendas pode conter uma partição de dados para cada ano passado e também partições para cada trimestre do ano atual. Apenas a partição do trimestre atual precisa ser processada quando as informações atuais são adicionadas ao cubo; processar uma quantidade menor de dados aprimorará o desempenho reduzindo o tempo de processamento. No final do ano, as quatro partições de trimestres podem ser mescladas em uma única partição para cada ano e uma nova partição é criada para o primeiro trimestre do novo ano. Além disso, o processo de criação dessa nova partição pode ser automatizado como parte dos procedimentos de carregamento de data warehouse e processamento do cubo.  
  
 As partições não são visíveis para usuários empresariais do cubo. Porém, os administradores podem configurar, adicionar ou descartar partições. Cada partição é armazenada em um conjunto separado de arquivos. Os dados de agregação de cada partição podem ser armazenados na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] onde a partição é definida, em outra instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], ou na fonte de dados usada para fornecer os dados de origem da partição. As partições permitem que os dados de origem e os dados de agregação do cubo sejam distribuídos por vários discos rígidos e entre diversos computadores. De um cubo moderado a grande, as partições podem aprimorar o desempenho da consulta, desempenho de carregamento e facilitar a manutenção do cubo.  
  
 O modo de armazenamento de cada partição pode ser configurado independentemente de outras partições no grupo de medidas. As partições podem ser armazenadas, usando qualquer combinação de opções para o local de dados de fonte, modo de armazenamento, cache pró-ativo e projeto de agregação. As opções para OLAP em tempo real e cache pró-ativo permitem equilibrar a velocidade de consulta em relação à latência ao projetar uma partição. As opções de armazenamento também podem ser aplicadas às dimensões relacionados e aos fatos no grupo de medidas. Essa flexibilidade permite projetar estratégias de armazenamento de cubo adequadas às suas necessidades. Para obter mais informações, consulte [modos de armazenamento de partição e processamento](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md), [agregações e Designs de agregação](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md) e [cache pró-ativo &#40; Partições &#41; ](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="partition-structure"></a>Estrutura de partição  
 A estrutura da partição deve corresponder à estrutura de seu grupo de medidas, o que significa que as medidas, que definem o grupo de medidas, devem ser definidas na partição juntamente com todas as dimensões relacionadas. Portanto, quando uma partição é criada, ela herda automaticamente o mesmo conjunto de medidas e dimensões relacionadas definidas para o grupo de medidas.  
  
 Entretanto, cada partição em um grupo de medidas pode ter uma tabela de fatos diferente e essas tabelas de fatos podem ser diferentes de suas fontes de dados. Quando partições diferentes em um grupo de medidas têm tabelas de fatos diferentes, as tabelas devem ser suficientemente similares para manter a estrutura do grupo de medidas, o que significa que a consulta de processamento retorna as mesmas colunas e os mesmos tipos de dados de todas as tabelas de fatos para todas as partições.  
  
 Quando tabelas de fatos de diferentes partições forem provenientes de diferentes fontes de dados, as tabelas de fonte de qualquer dimensão relacionada e, também, qualquer tabela de fatos intermediária deve estar presentes em todas as fontes de dados e devem ter a mesma estrutura em todos os bancos de dados. Além disso, todas as colunas de tabelas de dimensões usadas para definir atributos para dimensões do cubo relacionadas ao grupo de medidas devem estar presentes em todas as fontes de dados. Não há necessidade de definir todas as associações entre a tabela fonte de uma partição e a tabela de dimensões relacionada, se a tabela fonte da partição tiver estrutura idêntica à tabela fonte do grupo de medidas.  
  
 As colunas não usadas para definir medidas no grupo de medidas podem estar presentes em algumas tabelas de fatos, mas ausente em outras. Da mesma maneira, as colunas não usadas para definir atributos nas tabelas de dimensões relacionadas podem estar presentes em alguns bancos de dados, mas ausentes em outros. As tabelas não usadas por tabelas de fatos ou tabelas de dimensões relacionadas podem estar presentes em alguns bancos de dados, mas ausentes em outros.  
  
## <a name="data-sources-and-partition-storage"></a>Fontes de dados e armazenamento de partição  
 Uma partição tem base em uma tabela, em uma exibição da fonte de dados, em uma tabela ou em uma consulta nomeada na exibição da fonte de dados. O local onde os dados de partição são armazenados é definido pela associação da fonte de dados. Geralmente, você pode particionar um grupo de medidas horizontal ou verticalmente:  
  
-   Em um grupo de medidas particionado horizontalmente, cada partição em um grupo de medidas tem base em uma tabela separada. Esse tipo de particionamento é apropriado quando os dados são separados em várias tabelas. Por exemplo, alguns bancos de dados relacionais têm uma tabela separada para os dados de cada mês.  
  
-   Em um grupo de medidas particionado verticalmente, um grupo de medidas tem base em uma única tabela e cada partição é baseada em uma consulta do sistema fonte que filtra os dados da partição. Por exemplo, se uma única tabela contiver dados de diversos meses, o grupo de medidas ainda poderá ser particionado por mês aplicando-se uma cláusula WHERE Transact-SQL que retorna os dados do mês separados para cada partição.  
  
 Cada partição possui configurações de armazenamento que determinam se os dados e agregações para a partição são armazenados no instância local do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou em uma partição remota usando outras instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. As configurações de armazenamento podem também especificar o modo de armazenamento e se o cache pró-ativo for usado para controlar a latência de uma partição. Para obter mais informações, consulte [modos de armazenamento de partição e processamento](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md), [cache pró-ativo &#40; Partições &#41; ](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md), e [partições remotas](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md).  
  
## <a name="incremental-updates"></a>Atualizações incrementais  
 Ao criar e gerenciar partições em grupos de medidas de várias partições, você deve tomar precauções especiais para garantir que os dados do cubo sejam precisos. Apesar dessas precauções não se aplicarem geralmente a grupos de medidas de uma única partição, eles se aplicam quando você atualiza as partições incrementalmente. Quando você atualiza uma partição incrementalmente, uma nova partição temporária é criada com a estrutura idêntica à da partição fonte. A partição temporária é processada e então mesclada com a partição fonte. Portanto, você deve assegurar que a consulta de processamento que popula a partição temporária não duplique os dados já presentes em uma partição existente.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar propriedades de medida](../../analysis-services/multidimensional-models/configure-measure-properties.md)   
 [Cubos em modelos multidimensionais](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
