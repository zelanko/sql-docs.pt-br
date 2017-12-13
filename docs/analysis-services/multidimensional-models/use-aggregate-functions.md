---
title: "Use as funções de agregação | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: aggregate functions [Analysis Services]
ms.assetid: c42166ef-b75c-45f4-859c-09a3e9617664
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 7a146e6be066f8669757d15f5fe76ac67c5c172b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="use-aggregate-functions"></a>Usar funções de agregação
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Quando uma dimensão é usada para fatiar uma medida, a medida é resumida juntamente com hierarquias contidas nessa dimensão. O comportamento da soma depende da função de agregação especificada para a medida. Para mais medidas contendo dados numéricos, a função de agregação é **Soma**. O valor da medida totalizará valores diferentes, dependendo de qual nível da hierarquia está ativo.  
  
 No Analysis Services, cada medida que você cria é apoiada por uma função de agregação que determina a operação da medida. Os tipos de agregação predefinidos incluem **Soma**, **Mín**, **Máx**, **Contagem**, **Contagem Distinta**e várias outras funções mais especializadas. Como alternativa, se você precisar de agregações com base em fórmulas complexas ou personalizadas, poderá criar um cálculo de MDX em vez de usar uma função de agregação pré-compilada. Por exemplo, se você quiser definir uma medida para um valor de porcentagem, faria isso no MDX, usando uma medida calculada. Consulte [Instrução CREATE MEMBER &#40;MDX&#41;](../../mdx/mdx-data-definition-create-member.md).  
  
 Medidas criadas por meio do Assistente de cubo são atribuídas a um tipo de agregação como parte da definição da medida. O tipo de agregação é sempre **Soma**, supondo que a coluna de origem contém dados numéricos. **Soma** é atribuída, independentemente do tipo de dados da coluna de origem. Por exemplo, se você tiver usado o Assistente de cubo para criar medidas e preenchido todas as colunas por meio de uma tabela de fatos, notará que todas as medidas resultantes têm uma agregação de **Soma**, mesmo que a origem seja uma coluna de data e hora. Sempre examine os métodos de agregação pré-atribuídos para medidas criadas por meio do assistente para se certificar de que a função de agregação seja adequada.  
  
 Você pode atribuir ou alterar o método de agregação na definição do cubo, por meio de [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] ou por meio do MDX. Consulte [Criar medidas e grupos de medidas em modelos multidimensionais](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md) ou [Agregação &#40;MDX&#41;](../../mdx/aggregate-mdx.md) para obter mais instruções.  
  
##  <a name="AggFunction"></a> Funções de agregação  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece funções para agregar medidas às dimensões contidas em grupos de medidas. A *capacidade aditiva* de uma função de agregação determina como a medida é agregada entre todas as dimensões no cubo. As funções de agregação enquadram-se em três níveis de capacidade aditiva:  
  
 Aditiva  
 Uma medida aditiva, também chamada de medida totalmente aditiva, pode ser agregada a todas as dimensões incluídas no grupo de medidas que contém a medida, sem restrição.  
  
 Semiaditiva  
 Uma medida semiaditiva pode ser agregada a algumas das dimensões, mas não a todas, incluídas no grupo de medidas que contém a medida. Por exemplo, uma medida que representa a quantidade disponível em estoque pode ser agregada à dimensão geográfica para produzir a quantidade total disponível para todos os armazéns, mas a medida não pode ser agregada a uma dimensão de tempo porque ela representa um instantâneo periódico de quantidades disponíveis. Agregar essa medida a uma dimensão de tempo produziria resultados incorretos. Consulte [Definir comportamento semiaditivo](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md) para ver os detalhes.  
  
 Não aditiva  
 Uma medida não aditiva não pode ser agregada a nenhuma das dimensões incluídas no grupo de medidas que contém a medida. Em vez disso, ela deve ser calculada individualmente para cada célula do cubo que representa a medida. Por exemplo, uma medida calculada que retorna uma porcentagem, como margem de lucro, não pode ser agregada a partir dos valores de porcentagem de membros filho de qualquer dimensão.  
  
 A tabela a seguir lista as funções de agregação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e descreve a capacidade aditiva e a saída prevista da função.  
  
|Função de agregação|capacidade aditiva|Valor retornado|  
|--------------------------|----------------|--------------------|  
|**Soma**|Aditiva|Calcula a soma de valores de todos os membros filho. Essa é a função de agregação padrão.|  
|**Contagem**|Aditiva|Recupera a contagem de todos os membros filho.|  
|**Mín**|Semiaditiva|Recupera o valor mais baixo de todos os membros filho.|  
|**Máx**|Semiaditiva|Recupera o valor mais alto de todos os membros filho.|  
|**DistinctCount**|Não aditiva|Recupera a contagem de todos os membros filho exclusivos. Para obter mais detalhes, consulte [Sobre medidas de contagem distintas](../../analysis-services/multidimensional-models/use-aggregate-functions.md#bkmk_distinct) na próxima seção.|  
|**Nenhum.**|Não aditiva|Nenhuma agregação é executada e todos os valores de membros folha e não folha de uma dimensão são fornecidos diretamente da tabela de fatos para o grupo de medidas que contém a medida. Se não for possível ler um valor da tabela de fatos para um membro, o valor desse membro será definido como nulo.|  
|**ByAccount**|Semiaditiva|Calcula a agregação de acordo com a função de agregação atribuída ao tipo de conta de um membro em uma dimensão de conta. Se não existir uma dimensão de tipo de conta no grupo de medidas, será tratada como a função de agregação **None** .<br /><br /> Para obter mais informações sobre dimensões de conta, consulte [Criar uma Conta de Finanças de dimensão de tipo pai-filho](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md).|  
|**AverageOfChildren**|Semiaditiva|Calcula a média de valores de todos os membros filho não vazios.|  
|**FirstChild**|Semiaditiva|Recupera o valor do primeiro membro filho.|  
|**LastChild**|Semiaditiva|Recupera o valor do último membro filho.|  
|**FirstNonEmpty**|Semiaditiva|Recupera o valor do primeiro membro filho não vazio.|  
|**LastNonEmpty**|Semiaditiva|Recupera o valor do último membro filho não vazio.|  
  
##  <a name="bkmk_distinct"></a> Sobre medidas de contagem distintas  
 Uma medida com o valor da propriedade **Função Aggregate** de **Contagem Distinta** é chamada de medida de contagem distinta. Uma medida de contagem distinta pode ser usada para contar ocorrências dos membros de nível mais baixo de uma dimensão da tabela de fatos. Como a contagem é distinta, se um membro ocorrer várias vezes, ele será contado apenas uma vez. Uma medida de contagem distinta é sempre colocada em um grupo de medidas dedicado. Colocar uma medida de contagem distinta em seu próprio grupo de medidas é uma prática recomendada que foi criada no designer como uma técnica de otimização do desempenho.  
  
 Normalmente, as medidas de contagem distinta são usadas para determinar para cada membro de uma dimensão quantos membros de nível inferior e distintos de outra dimensão compartilham linhas da tabela de fatos. Por exemplo, em um cubo Vendas, para cada cliente e grupo de clientes, quantos produtos distintos foram comprados? (Quer dizer, para cada membro da dimensão Clientes, quantos membros distintos, em nível inferior da dimensão Produtos, compartilham linhas na tabela de fatos?) Por exemplo, em um cubo Visitas ao Site da Internet, para cada visitante de site e grupo de visitantes de site, quantas páginas distintas no site da Internet foram visitadas? (Quer dizer, para cada membro da dimensão Visitantes de Site, quantos membros distintos, em nível inferior da dimensão Páginas, compartilham linhas na tabela de fatos?) Em cada um desses exemplos, os membros em nível inferior da segunda dimensão são contados por uma medida de contagem distinta.  
  
 Esse tipo de análise não precisa ser limitada a duas dimensões. Na verdade, uma medida de contagem distinta pode ser separada e dividida em qualquer combinação de dimensões do cubo, incluindo dimensões que contêm membros contados.  
  
 Uma medida de contagem distinta que conta membros baseia-se m uma coluna de chave estrangeira da tabela de fatos. (Ou seja, a propriedade **Source Column** da medida identifica essa coluna.) Essa coluna une a coluna da tabela de dimensões que identifica os membros contados pela medida de contagem distinta.  
  
## <a name="see-also"></a>Consulte também  
 [Medidas e Grupos de Medidas](../../analysis-services/multidimensional-models/measures-and-measure-groups.md)   
 [Referência de função MDX &#40; MDX &#41;](../../mdx/mdx-function-reference-mdx.md)   
 [Definir um comportamento semiaditivo](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md)  
  
  
