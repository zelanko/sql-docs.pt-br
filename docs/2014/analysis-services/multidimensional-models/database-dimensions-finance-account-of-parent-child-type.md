---
title: Criar uma conta de Finanças de dimensão de tipo de pai-filho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], account
- account dimensions [Analysis Services]
- adding account intelligence
- account intelligence [Analysis Services]
ms.assetid: 2ba74e81-5b4b-407e-acdf-deb2f6accf0a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 321e64d62b1ef1a564496366409dc0a5104cedec
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52523076"
---
# <a name="create-a-finance-account-of-parent-child-type-dimension"></a>Criar uma Conta de Finanças de Dimensão de tipo pai-filho
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], uma dimensão de tipo de conta é aquela cujos atributos representam um plano de contas para uso em relatórios financeiros.  
  
 Uma dimensão de conta permite o gerenciamento seletivo do comportamento de agregação entre contas no decorrer do tempo. Uma dimensão de conta também possibilita o uso de mecanismos padrão para resolver a maioria das questões de agregação não padrão geralmente encontradas em soluções de business intelligence que lidam com dados financeiros. Sem esse tipo de mecanismo padrão, a resolução dessas questões de agregação não padrão requer fórmulas de acúmulo personalizado, membros calculados ou scripts de expressões multidimensionais (MDX).  
  
 Para identificar uma dimensão como dimensão de conta, defina sua propriedade `Type` como `Accounts`.  
  
## <a name="dimension-structure"></a>Estrutura da Dimensão  
 Uma dimensão de conta contém, no mínimo, dois atributos:  
  
-   Um atributo de um atributo de chave que identifica contas individuais na tabela de dimensões para a dimensão de conta.  
  
-   Um atributo pai de um atributo de conta que descreve como as contas são organizadas hierarquicamente na dimensão de conta.  
  
     Para identificar um atributo como atributo de conta, defina sua propriedade `Type` como `Account` e a propriedade `Usage` como `Parent`.  
  
 Opcionalmente, as dimensões de conta podem conter os seguintes atributos:  
  
-   Uma conta de tipo de atributo de um atributo que define o tipo de conta para cada conta na dimensão. Os nomes de membros do atributo de tipo de conta são mapeados para os tipos de conta definidos para o banco de dados ou projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e indicam a função de agregação usada pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para essas contas. Também é possível usar operadores unários ou fórmulas de acúmulo personalizado para determinar o comportamento de agregação dos atributos de conta, mas, com os tipos de conta, é possível aplicar facilmente ao plano de contas um comportamento consistente sem precisar fazer alterações no banco de dados relacional subjacente.  
  
     Para identificar um atributo de tipo de conta, defina sua propriedade `Type` como `AccountType`.  
  
-   Um nome atributo um atributo de conta que é usado para fins de relatório. Para identificar um atributo de nome de conta, configure sua propriedade `Type` como `AccountName`.  
  
-   Uma conta de número de atributo de um atributo que é usado para fins de relatório. Para identificar um atributo de número de conta, configure sua propriedade `Type` como `AccountNumber`.  
  
 Para obter mais informações sobre tipos de atributos, consulte [Configurar tipos de atributo](attribute-properties-configure-attribute-types.md).  
  
## <a name="adding-account-intelligence-with-the-business-intelligence-wizard"></a>Adicionando inteligência de conta com o Assistente de Business Intelligence  
 Depois de configurar a dimensão de conta e adicioná-la a um cubo, você pode usar o Assistente de Business Intelligence para adicionar à dimensão funcionalidades de inteligência de conta, como identificação e mapeamento de tipos de conta. Para obter mais informações, consulte [Adicionar inteligência de conta a uma dimensão](bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="see-also"></a>Consulte também  
 [Atributos e hierarquias de atributos](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Ajuda F1 do Assistente de Business Intelligence](../business-intelligence-wizard-f1-help.md)   
 [Tipos de dimensão](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
