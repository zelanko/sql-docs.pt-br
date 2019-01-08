---
title: Relações de atributo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f9eddac84f4db92770daa2bbf32b51597f84eb3f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52542758"
---
# <a name="attribute-relationships"></a>Relações de Atributo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Na [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], atributos dentro de uma dimensão sempre estão relacionados diretamente ou indiretamente ao atributo de chave. Quando você define uma dimensão com base em um esquema em estrela, onde todos os atributos de dimensão são derivados da mesma tabela relacional, uma relação de atributo é automaticamente definida entre o atributo de chave e cada atributo não chave da dimensão. Quando você define uma dimensão com base em um esquema de floco de neve, onde todos os atributos de dimensão derivam de várias tabelas relacionadas, uma relação de atributo é automaticamente definida da seguinte maneira:  
  
-   Entre o atributo de chave e cada atributo não chave vinculado às colunas na tabela de dimensões principal.  
  
-   Entre o atributo de chave e atributo vinculado à chave estrangeira na tabela secundária que vincula as tabelas de dimensões subjacentes.  
  
-   Entre o atributo vinculado à chave estrangeira na tabela secundária e cada atributo não chave vinculado às colunas da tabela secundária.  
  
 Porém, há vários motivos pelos quais talvez queira alterar essas relações de atributo padrão. Por exemplo, você pode querer definir uma hierarquia natural, uma ordem de classificação personalizada ou uma granularidade de dimensão com base em um atributo não chave. Para obter mais informações, consulte [referência de propriedades de atributo de dimensão](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md).  
  
> [!NOTE]  
>  Relações de atributo são conhecidas em MDX como propriedades do membro.  
  
## <a name="natural-hierarchy-relationships"></a>Relações de hierarquia natural  
 Uma hierarquia é uma hierarquia natural quando cada atributo incluído na hierarquia definida pelo usuário possui uma relação um para muitos com o atributo imediatamente abaixo dele. Por exemplo, considere uma dimensão Cliente com base em uma tabela fonte relacional com oito colunas:  
  
-   CustomerKey  
  
-   CustomerName  
  
-   Idade  
  
-   Gênero  
  
-   Email  
  
-   Cidade  
  
-   País  
  
-   Região  
  
 A dimensão Analysis Services correspondente tem sete atributos:  
  
-   Cliente (com base em CustomerKey, com CustomerName que fornece os nomes dos membros)  
  
-   Idade, Sexo, Email, Cidade, Região, País  
  
 As relações representando hierarquias naturais são impostas pela criação de uma relação de atributo entre o atributo para um nível e o atributo para o nível abaixo dele. Para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], isso especifica uma relação natural e agregação de potencial. Na dimensão Cliente, uma hierarquia natural existe para os atributos País, Região, Cidade e Cliente. A hierarquia natural para `{Country, Region, City, Customer}` é descrita adicionando-se as seguintes relações de atributo:  
  
-   O atributo País como uma relação com o atributo Região.  
  
-   O atributo Região como uma relação com o atributo Cidade.  
  
-   O atributo Cidade como uma relação com o atributo Cliente.  
  
 Para navegar por dados no cubo, você também pode criar uma hierarquia definida pelo usuário que não representa uma hierarquia natural nos dados (que é chamado um *ad-hoc* ou *reporting* hierarquia). Por exemplo, você pode criar uma hierarquia definida pelo usuário com base em `{Age, Gender}`. Os usuários não percebem diferenças em como as duas hierarquias se comportam, embora a hierarquia natural se beneficia da agregação e indexação estruturas - ocultadas do usuário - dessa conta das relações naturais nos dados de origem.  
  
 O **SourceAttribute** propriedade de um nível determina qual atributo é usado para descrever o nível. O **KeyColumns** propriedade no atributo especifica a coluna na exibição da fonte de dados que fornece os membros. O **NameColumn** propriedade do atributo pode especificar um nome de coluna diferente para os membros.  
  
 Para definir um nível em uma hierarquia definida pelo usuário usando [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], o **Designer de dimensão** permite que você selecione um atributo de dimensão, uma coluna em uma tabela de dimensões ou uma coluna de uma tabela relacionada incluída na exibição da fonte de dados para o cubo. Para obter mais informações sobre como criar hierarquias definidas pelo usuário, consulte [hierarquias definidas pelo usuário](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md).  
  
 No Analysis Services, uma suposição é normalmente feita sobre o conteúdo dos membros. Os membros folha não têm nenhum descendente e contêm dados derivados de fontes de dados subjacentes. Os membros não folha têm descendentes e contêm dados derivados de agregações executadas em membros filhos. Em níveis de agregação, os membros são com base em agregações de níveis subordinados. Portanto, quando o **IsAggregatable** estiver definida como **falso** em um atributo de origem para um nível, nenhum atributo agregável deve ser adicionado como nível acima dele.  
  
## <a name="defining-an-attribute-relationship"></a>Definindo uma relação de atributo  
 A principal restrição ao criar uma relação de atributo é certificar-se de que o atributo referenciado pela relação de atributo, não possui mais que um valor para qualquer membro no atributo ao qual a relação de atributo pertence. Por exemplo, se você definir uma relação entre um atributo Cidade e um atributo Estado, cada cidade pode apenas estar relacionada a um único estado.  
  
## <a name="attribute-relationship-queries"></a>Consultas de relação de atributo  
 Você pode usar consultas MDX para recuperar dados de relações de atributo na forma de propriedades do membro, com o **propriedades** palavra-chave do MDX **selecione** instrução. Para obter mais informações sobre como usar MDX para recuperar propriedades do membro, consulte [usando propriedades de membro &#40; MDX &#41; ](../../analysis-services/multidimensional-models/mdx/mdx-member-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Atributos e hierarquias de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Referência de propriedades de atributo de dimensão](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)   
 [Hierarquias do usuário](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Propriedades de hierarquia do usuário](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  
