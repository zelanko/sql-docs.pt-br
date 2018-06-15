---
title: Grupos de medidas e | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 04eb5a41bec6e9abb62cfde516f2dad2ff820521
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024243"
---
# <a name="measures-and-measure-groups"></a>Medidas e Grupos de Medidas
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Um cubo inclui *medidas* em *grupos de medidas*, lógica de negócios, além de um conjunto de dimensões que fornecem contexto para avaliar os dados numéricos que uma medida fornece. Medidas e grupos de medidas são um componente essencial de um cubo. Um cubo não pode existir sem pelo menos uma delas.  
  
 Este tópico descreve [medidas](#bkmk_measure) e [grupos de medidas](#bkmk_mg). Ele também contém a tabela a seguir, com links para procedimentos para medidas de criação e configuração e grupos de medidas.  
  
|**Link**|**Description**|  
|--------------|---------------------|  
|[Criar medidas e grupos de medidas em modelos multidimensionais](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)|Escolha uma das várias abordagens para criar medidas e grupos de medidas.|  
|[Configurar propriedades de medida](../../analysis-services/multidimensional-models/configure-measure-properties.md)|Se você usou o Assistente de cubo para iniciar seu cubo, talvez seja necessário alterar o método de agregação, aplicar um formato de dados, definir a visibilidade da medida em aplicativos cliente ou possivelmente adicionar uma expressão de medida para manipular os dados antes de os valores serem agregados.|  
|[Configurar propriedades do grupo de medidas](../../analysis-services/multidimensional-models/configure-measure-group-properties.md)|Em um modelo multidimensional, um grupo de medidas é igual a uma tabela de fatos no armazém de dados de origem. Propriedades em um grupo de medidas permitem especificar comportamentos de cache, armazenamento e diretivas de processamento que operam coletivamente no nível do grupo de medidas. A configuração de partição é parcialmente determinada pelas propriedades definidas em objetos do grupo de medidas.|  
|[Use as funções de agregação](../../analysis-services/multidimensional-models/use-aggregate-functions.md)|Compreenda os métodos de agregação que podem ser atribuídos a uma medida.|  
|[Definir comportamento Semiaditivo](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md)|Comportamento semiaditivo se refere a agregações que são válidas para algumas dimensões, mas não para outras. Um exemplo comum é um saldo da conta bancária. Talvez você deseje agregar saldos por cliente e região, mas não por tempo. Por exemplo, não convém adicionar saldos da mesma conta por dias consecutivos. Para definir o comportamento semiaditivo, use o Assistente para Adicionar Business Intelligence.|  
|[Grupos de medidas vinculados](../../analysis-services/multidimensional-models/linked-measure-groups.md)|Reutilizar um grupo de medidas existente em outros cubos no mesmo banco de dados ou em bancos de dados diferentes do Analysis Services.|  
  
##  <a name="bkmk_measure"></a> Measures  
 Uma medida representa uma coluna que contém dados quantificáveis, normalmente numéricos, que podem ser agregados. As medidas representam algum aspecto da atividade organizacional, expressa em termos monetários (tal como receita, margens ou custos), como conta (níveis de estoque, número de funcionários, clientes ou pedidos) ou como um cálculo mais complexo que incorpora a lógica de negócios.  
  
 Cada cubo deve ter pelo menos uma medida, mas a maioria tem muitos, às vezes, centenas. Estruturalmente, uma medida é geralmente mapeada para uma coluna de origem em uma tabela de fatos, com a coluna que fornece os valores usados para carregar a medida. Como alternativa, você também pode definir uma medida usando MDX.  
  
 As medidas são contextuais, operando em dados numéricos em um contexto que é determinado por quaisquer membros de dimensão que sejam incluídos na consulta. Por exemplo, uma medida que calcula **Vendas do Revendedor** será feita por um operador **Sum** , e ele adicionará os valores de vendas a cada membro da dimensão incluído na consulta. Se a consulta especifica produtos individuais, acumula em uma categoria, ou é dividida por tempo ou geografia, ela deverá produzir uma operação que seja válida para as dimensões incluídas na consulta.  
  
 Neste exemplo, **Vendas do Revendedor** agrega em vários níveis na hierarquia de **Região de Vendas** .  
  
 ![Tabela dinâmica com medidas e dimensões destacadas](../../analysis-services/multidimensional-models/media/ssas-keyconcepts-pivot1-measures-dimensions.png "tabela dinâmica com medidas e dimensões destacadas")  
  
 Medidas produzem resultados válidos quando a tabela de fatos que contém os dados de origem numéricos também contém ponteiros para as tabelas de dimensão que são usados na consulta. Usando o exemplo de Vendas do revendedor, se cada linha armazenar um valor de vendas também armazenará um ponteiro para uma tabela de produtos, uma tabela de data ou uma tabela de territórios de vendas; em seguida, as consultas que incluem membros desses dimensão serão interpretadas corretamente.  
  
 O que acontece se a medida não estiver relacionada às dimensões usadas na consulta? Normalmente, o Analysis Services mostrará a medida padrão e o valor será o mesmo para todos os membros. Neste exemplo, **Vendas pela Internet**, que mede vendas diretas feitas por clientes que usam o catálogo online, não tem relação com a organização de vendas.  
  
 ![Valores de medida de tabela dinâmica mostrando repetidas](../../analysis-services/multidimensional-models/media/ssas-unrelatedmeasure.PNG "valores de medida de tabela dinâmica mostrando repetidas")  
  
 Para minimizar a possibilidade de encontrar esses comportamentos em um aplicativo cliente, você poderia compilar vários cubos ou perspectivas no mesmo banco de dados e verificar se cada cubo ou perspectiva contém apenas os objetos relacionados. As relações que você precisa verificar estão entre o grupo de medidas (mapeado para a tabela de fatos) e as dimensões.  
  
##  <a name="bkmk_mg"></a> Measure Groups  
 Em um cubo, as medidas são agrupadas pelas tabelas de fatos subjacentes em grupos de medidas. Os grupos de medidas são usados para associar dimensões a medidas. Os grupos de medidas também são usados para medidas com conta distinta como o comportamento de agregação. Colocar cada medida de contagem distinta em seu próprio grupo de medidas otimiza o processamento da agregação.  
  
 Um simples objeto <xref:Microsoft.AnalysisServices.MeasureGroup> é composto por informações básicas, como o nome do grupo, o modo de armazenamento e o modo de processamento. Ele também contém suas partes constituintes; as medidas, dimensões e partições que formam a composição do grupo de medidas.  
  
## <a name="see-also"></a>Consulte também  
 [Cubos em modelos multidimensionais](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)   
 [Criar medidas e grupos de medidas em modelos multidimensionais](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)  
  
  
