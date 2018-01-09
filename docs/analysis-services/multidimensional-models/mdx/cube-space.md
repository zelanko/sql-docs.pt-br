---
title: "Espaço de cubo | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c3a012b4-9ca0-4fb8-9c26-5ecc0e2e2b2b
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 316809a9fa0b00a04dd6cee85eceb3d9a0349801
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="cube-space"></a>Espaço de cubo
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Espaço de cubo é o produto dos membros de hierarquias de atributo de um cubo com as medidas do cubo. Portanto, o espaço de cubo é determinado pelo produto combinatório de todos os membros de hierarquia de atributo no cubo e as medidas do cubo e define o tamanho máximo do cubo. É importante observar que esse espaço inclui todas as possíveis combinações de membros de hierarquia de atributo, inclusive combinações que poderiam ser consideradas impossíveis no mundo real, como combinações onde a cidade é Paris e os países são Inglaterra, Espanha, Japão, Índia ou qualquer outro.  
  
## <a name="autoexists-and-cube-space"></a>Autoexists e espaço de cubo  
 O conceito de *autoexists* limita esse espaço de cubo às células que realmente existem. É possível que membros de uma hierarquia de atributo em uma dimensão não existam com membros de outra hierarquia de atributo na mesma dimensão.  
  
 Por exemplo, se você tiver um cubo com uma hierarquia de atributo Cidade, uma hierarquia de atributo País, e uma medida Valor de Vendas pela Internet, o espaço desse cubo somente vai incluir os membros que existem um com o outro. Por exemplo, se a hierarquia de atributo Cidade incluir as cidades de Nova Iorque, Londres, Paris, Tóquio e Melbourne; e a hierarquia de atributo País incluir os países Estados Unidos, Reino Unido, França, Japão e Austrália; o espaço do cubo não incluirá o espaço (célula) na interseção Paris e Estados Unidos.  
  
 Ao consultar células que não existem, as células inexistentes retornarão nulas; ou seja, elas não poderão conter cálculos e você não poderá definir um cálculo que seja gravado nesse espaço. Por exemplo, a instrução a seguir inclui células que não existem.  
  
```  
SELECT [Customer].[Gender].[Gender].Members ON COLUMNS,  
{[Customer].[Customer].[Aaron A. Allen]  
   ,[Customer].[Customer].[Abigail Clark]} ON ROWS   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  Essa consulta usa a função [Membros (Conjunto) (MDX)](../../../mdx/members-set-mdx.md) para retornar o conjunto de membros da hierarquia de atributo Sexo no eixo da coluna, e cruza esse conjunto com o conjunto especificado de membros da hierarquia de atributo Cliente no eixo de linhas.  
  
 Quando você executa a consulta anterior, a célula na interseção Aaron A. Allen e Feminino exibe um valor nulo. Similarmente, a célula na interseção Abigail Clark e Masculino exibe um valor nulo. Essas células não existem e não podem conter um valor, mas as células que não existem podem aparecer no resultado retornado por uma consulta.  
  
 Quando você usa a função [Crossjoin (MDX)](../../../mdx/crossjoin-mdx.md) para retornar o produto vetorial de membros de hierarquia de atributo de hierarquias de atributo na mesma dimensão, o Autoexists limita as tuplas que são retornadas ao conjunto de tuplas que realmente existem, em vez de retornar um produto Cartesiano completo. Por exemplo, execute e examine os resultados da execução da consulta a seguir.  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[State-Province].Members  
  ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  Note que 0 é usado para designar o eixo da coluna, que é a forma abreviada de eixo (0) – que é o eixo da coluna.  
  
 A consulta anterior somente retorna células para membros de cada hierarquia de atributo na consulta que existe um com o outro. A consulta anterior também pode ser escrita usando a nova * variante da função [* (Crossjoin) (MDX)](../../../mdx/crossjoin-mdx-operator-reference.md) .  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 A consulta anterior também poderia ser escrita da seguinte forma:  
  
```  
SELECT [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
 Os valores das células retornadas serão idênticos, apesar de os metadados no conjunto de resultados serem diferentes. Por exemplo, com a consulta anterior, a hierarquia País foi movida para o eixo do slicer (na cláusula WHERE) e, portanto, não aparece explicitamente no conjunto de resultados.  
  
 Cada uma dessas três consultas anteriores demonstra o efeito do comportamento Autoexists no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="user-defined-hierarchies-and-cube-space"></a>Hierarquias definidas pelo usuário e espaço do cubo  
 Os exemplos anteriores deste tópico definem posições no espaço do cubo, usando hierarquias de atributo. Porém, você também pode definir uma posição no espaço do cubo usando hierarquias definidas pelo usuário que foram definidas com base em hierarquias de atributo em uma dimensão. Uma hierarquia definida pelo usuário é uma hierarquia das hierarquias de atributo planejada para facilitar a procura de dados de cubo pelos usuários.  
  
 Por exemplo, a consulta **CROSSJOIN** na seção anterior também poderia ter sido escrita conforme apresentado a seguir:  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[Customer Geography].[State-Province].Members  
   )   
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 Na consulta anterior, a hierarquia Geografia do Cliente definida pelo usuário dentro da dimensão Cliente é usada para definir a posição no espaço do cubo que foi anteriormente definida usando uma hierarquia de atributo. A posição idêntica no espaço do cubo pode ser definida usando hierarquias de atributo ou hierarquias definidas pelo usuário.  
  
##  <a name="AttribRelationships"></a> Relações de atributo e espaço de cubo  
 Definindo relações de atributo entre atributos relacionados aprimora o desempenho da consulta (facilitando a criação de agregações apropriadas) e afeta o membro de uma hierarquia de atributo relacionada que aparece com um membro de hierarquia de atributo. Por exemplo, quando você define uma tupla que inclui um membro da hierarquia de atributo Cidade e a tupla não define explicitamente o membro da hierarquia de atributo País, você poderia esperar que o membro padrão da hierarquia de atributo País seria o membro relacionado da hierarquia de atributo País. Porém, isso só ocorrerá se uma relação de atributo estiver definida entre a hierarquia de atributo Cidade e a hierarquia de atributo País.  
  
 O exemplo a seguir retorna o membro de uma hierarquia de atributo relacionada que não está explicitamente incluído na consulta.  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Country.CurrentMember.Name  
SELECT Measures.x ON 0,  
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Note que a palavra-chave **WITH** é usada com as funções [CurrentMember (MDX)](../../../mdx/currentmember-mdx.md) e [Name (MDX)](../../../mdx/name-mdx.md) para criar um membro calculado para uso na consulta. Para obter mais informações, consulte [A consulta MDX básica &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md).  
  
 Na consulta anterior, o nome do membro da hierarquia de atributo País que está associado a cada membro da hierarquia de atributo Estado é retornado. O membro País esperado é exibido (porque uma relação de atributo está definida entre os atributos Cidade e País). Porém, se nenhuma relação de atributo estivesse definida entre hierarquias de atributo na mesma dimensão, o membro (All) seria retornado, conforme ilustrado na consulta a seguir.  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Education.Currentmember.Name  
SELECT Measures.x  ON 0,   
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
 Na consulta anterior, é retornado o membro (All) ("Todos os Clientes"), porque não existe nenhuma relação entre Educação e Cidade. Portanto, o membro (All) da hierarquia de atributo Educação seria o membro padrão da hierarquia de atributo Educação usado em qualquer tupla envolvendo a hierarquia de atributo Cidade onde um membro Educação não é explicitamente fornecido.  
  
## <a name="calculation-context"></a>Contexto de cálculo  
  
## <a name="see-also"></a>Consulte Também  
 [Principais conceitos em MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Tuplas](../../../analysis-services/multidimensional-models/mdx/tuples.md)   
 [Autoexists](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [Trabalhando com membros, tuplas e conjuntos &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [Totais visuais e totais não visuais](../../../analysis-services/multidimensional-models/mdx/visual-totals-and-non-visual-totals.md)   
 [Referência da linguagem MDX &#40;MDX&#41;](../../../mdx/mdx-language-reference-mdx.md)   
 [Referência de expressões multidimensionais &#40;MDX&#41;](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
