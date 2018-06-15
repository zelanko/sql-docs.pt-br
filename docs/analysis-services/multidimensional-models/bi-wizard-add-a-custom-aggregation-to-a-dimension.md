---
title: Adicionar uma agregação personalizada a uma dimensão | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cbe5c4a1f043ccc8e7f442213b8b024a3920663e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34020703"
---
# <a name="bi-wizard---add-a-custom-aggregation-to-a-dimension"></a>Assistente de BI - adicionar uma agregação personalizada a uma dimensão
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Adicione um aprimoramento de agregação personalizada a um cubo ou dimensão para substituir as agregações padrão associadas a um membro da dimensão por outro operador unário. Esse aprimoramento especifica uma coluna de operador unário na tabela de dimensões que define o acúmulo de membros em uma hierarquia pai-filho. O operador unário age no atributo pai em uma hierarquia pai-filho.  
  
> [!NOTE]  
>  Uma agregação personalizada estará disponível somente para dimensões baseadas em fontes de dados existentes. Para dimensões que foram criadas sem usar uma fonte de dados, execute o Assistente de Geração de Esquema para criar uma exibição da fonte de dados antes de adicionar a agregação personalizada.  
  
 Para adicionar uma agregação personalizada, use o Assistente de Business Intelligence e selecione a opção **Especificar um operador unário** na página **Escolher Aprimoramento** . Esse assistente orientará você durante as etapas para selecionar a dimensão à qual você deseja aplicar uma agregação personalizada e para identificar a agregação personalizada.  
  
> [!NOTE]  
>  Antes de executar o Assistente de Business Intelligence para adicionar uma agregação personalizada, confirme se a dimensão que você deseja aprimorar contém uma hierarquia de atributo pai-filho. Para obter mais informações, consulte [Dimensões pai-filho](../../analysis-services/multidimensional-models/parent-child-dimension.md).  
  
## <a name="selecting-a-dimension"></a>Selecionando uma dimensão  
 Na primeira página **Especificar um Operador Unário** do assistente, especifique a dimensão à qual você deseja aplicar uma agregação personalizada. A agregação personalizada adicionada à dimensão selecionada fará alterações na dimensão. Essas alterações serão herdadas por todos os cubos que tiverem a dimensão selecionada.  
  
## <a name="adding-custom-aggregation-unary-operator"></a>Adicionando agregação personalizada (operador unário)  
 Na segunda página **Especificar um Operador Unário** do assistente, especifique o atributo pai desejado para a agregação personalizada e a coluna de origem da tabela de dimensões para o operador unário. O**Atributo pai** lista atributos cuja propriedade **Usage** foi configurada como **Parent**. Se houver mais de um atributo pai, escolha o atributo pai que corresponde à relação pai-filho que você deseja usar. Se não houver um atributo pai listado, a dimensão não possui uma hierarquia pai-filho válida.  
  
 Em **Coluna de origem**, selecione a coluna de cadeia de caracteres que contém os operadores unários. (Essa seleção configura a propriedade **UnaryOperatorColumn** do atributo pai.) A tabela de dimensões também deve ter uma coluna de cadeia de caracteres que especifica o operador de acúmulo unário. Os valores da cadeia de caracteres dessa coluna devem conter operadores de agregação válidos. Se houver uma linha vazia, o membro correspondente será calculado normalmente. Se a fórmula de uma coluna não for válida, ocorrerá um erro de tempo de execução quando o valor de uma célula que usa o membro for recuperado. Para obter mais informações, consulte [Operadores unários nas dimensões pai-filho](../../analysis-services/multidimensional-models/parent-child-dimension-attributes-unary-operators.md).  
  
  
