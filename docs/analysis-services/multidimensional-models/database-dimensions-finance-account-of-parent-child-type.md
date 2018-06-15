---
title: Criar uma conta de Finanças de dimensão de tipo de pai-filho | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 39c08417c421a39c15ab995a5e5d2f9ca26d5c95
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34023253"
---
# <a name="database-dimensions---finance-account-of-parent-child-type"></a>Dimensões de banco de dados - conta de finanças do tipo pai-filho
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], uma dimensão de tipo de conta é aquela cujos atributos representam um plano de contas para uso em relatórios financeiros.  
  
 Uma dimensão de conta permite o gerenciamento seletivo do comportamento de agregação entre contas no decorrer do tempo. Uma dimensão de conta também possibilita o uso de mecanismos padrão para resolver a maioria das questões de agregação não padrão geralmente encontradas em soluções de business intelligence que lidam com dados financeiros. Sem esse tipo de mecanismo padrão, a resolução dessas questões de agregação não padrão requer fórmulas de acúmulo personalizado, membros calculados ou scripts de expressões multidimensionais (MDX).  
  
 Para identificar uma dimensão como dimensão de conta, defina sua propriedade **Type** como **Contas**.  
  
## <a name="dimension-structure"></a>Estrutura da Dimensão  
 Uma dimensão de conta contém, no mínimo, dois atributos:  
  
-   Um atributo de chave – um atributo que identifica contas individuais na tabela de dimensões para a dimensão de conta.  
  
-   Um atributo de conta – um atributo pai que descreve como as contas são organizadas hierarquicamente na dimensão de conta.  
  
     Para identificar um atributo como atributo de conta, defina sua propriedade **Type** como **Conta** e a propriedade **Usage** como **Pai**.  
  
 Opcionalmente, as dimensões de conta podem conter os seguintes atributos:  
  
-   Um atributo tipo de conta – um atributo que define o tipo de cada conta da dimensão. Os nomes de membros do atributo de tipo de conta são mapeados para os tipos de conta definidos para o banco de dados ou projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e indicam a função de agregação usada pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para essas contas. Também é possível usar operadores unários ou fórmulas de acúmulo personalizado para determinar o comportamento de agregação dos atributos de conta, mas, com os tipos de conta, é possível aplicar facilmente ao plano de contas um comportamento consistente sem precisar fazer alterações no banco de dados relacional subjacente.  
  
     Para identificar um atributo de tipo de conta, defina sua propriedade **Type** como **AccountType**.  
  
-   Um atributo de nome de conta – um atributo usado nos relatórios. Para identificar um atributo de tipo de conta, defina sua propriedade **Type** como **AccountName**.  
  
-   Um atributo de número de conta – um atributo usado nos relatórios. Para identificar um atributo de tipo de conta, defina sua propriedade **Type** como **AccountNumber**.  
  
 Para obter mais informações sobre tipos de atributos, consulte [Configurar tipos de atributo](../../analysis-services/multidimensional-models/attribute-properties-configure-attribute-types.md).  
  
## <a name="adding-account-intelligence-with-the-business-intelligence-wizard"></a>Adicionando inteligência de conta com o Assistente de Business Intelligence  
 Depois de configurar a dimensão de conta e adicioná-la a um cubo, você pode usar o Assistente de Business Intelligence para adicionar à dimensão funcionalidades de inteligência de conta, como identificação e mapeamento de tipos de conta. Para obter mais informações, consulte [Adicionar inteligência de conta a uma dimensão](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="see-also"></a>Consulte também  
 [Atributos e hierarquias de atributo](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Ajuda de F1 do Assistente do Business Intelligence](http://msdn.microsoft.com/library/155ac80c-63ae-47aa-9e86-9396e3d920eb)   
 [Tipos de dimensão](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
