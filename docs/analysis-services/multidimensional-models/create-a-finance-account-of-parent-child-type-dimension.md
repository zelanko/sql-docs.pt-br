---
title: "Criar uma Conta de Finan&#231;as de Dimens&#227;o de tipo pai-filho | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "dimensões [Analysis Services], conta"
  - "dimensões de conta [Analysis Services]"
  - "adicionando inteligência de conta"
  - "inteligência de conta [Analysis Services]"
ms.assetid: 2ba74e81-5b4b-407e-acdf-deb2f6accf0a
caps.latest.revision: 15
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Criar uma Conta de Finan&#231;as de Dimens&#227;o de tipo pai-filho
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], uma dimensão de tipo de conta é aquela cujos atributos representam um plano de contas para uso em relatórios financeiros.  
  
 Uma dimensão de conta permite o gerenciamento seletivo do comportamento de agregação entre contas no decorrer do tempo. Uma dimensão de conta também possibilita o uso de mecanismos padrão para resolver a maioria das questões de agregação não padrão geralmente encontradas em soluções de business intelligence que lidam com dados financeiros. Sem esse tipo de mecanismo padrão, a resolução dessas questões de agregação não padrão requer fórmulas de acúmulo personalizado, membros calculados ou scripts de expressões multidimensionais (MDX).  
  
 Para identificar uma dimensão como dimensão de conta, defina sua propriedade **Type** como **Contas**.  
  
## Estrutura da Dimensão  
 Uma dimensão de conta contém, no mínimo, dois atributos:  
  
-   Um atributo de chave – um atributo que identifica contas individuais na tabela de dimensões para a dimensão de conta.  
  
-   Um atributo de conta – um atributo pai que descreve como as contas são organizadas hierarquicamente na dimensão de conta.  
  
     Para identificar um atributo como atributo de conta, defina sua propriedade **Type** como **Conta** e a propriedade **Usage** como **Pai**.  
  
 Opcionalmente, as dimensões de conta podem conter os seguintes atributos:  
  
-   Um atributo tipo de conta – um atributo que define o tipo de cada conta da dimensão. Os nomes de membros do atributo de tipo de conta são mapeados para os tipos de conta definidos para o banco de dados ou projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e indicam a função de agregação usada pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para essas contas. Também é possível usar operadores unários ou fórmulas de acúmulo personalizado para determinar o comportamento de agregação dos atributos de conta, mas, com os tipos de conta, é possível aplicar facilmente ao plano de contas um comportamento consistente sem precisar fazer alterações no banco de dados relacional subjacente.  
  
     Para identificar um atributo de tipo de conta, defina sua propriedade **Type** como **AccountType**.  
  
-   Um atributo de nome de conta – um atributo usado nos relatórios. Para identificar um atributo de tipo de conta, defina sua propriedade **Type** como **AccountName**.  
  
-   Um atributo de número de conta – um atributo usado nos relatórios. Para identificar um atributo de tipo de conta, defina sua propriedade **Type** como **AccountNumber**.  
  
 Para obter mais informações sobre tipos de atributos, consulte [Configurar tipos de atributo](../../analysis-services/multidimensional-models/configure-attribute-types.md).  
  
## Adicionando inteligência de conta com o Assistente de Business Intelligence  
 Depois de configurar a dimensão de conta e adicioná-la a um cubo, você pode usar o Assistente de Business Intelligence para adicionar à dimensão funcionalidades de inteligência de conta, como identificação e mapeamento de tipos de conta. Para obter mais informações, consulte [Adicionar inteligência de conta a uma dimensão](../../analysis-services/multidimensional-models/add-account-intelligence-to-a-dimension.md).  
  
## Consulte também  
 [Atributos e hierarquias de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Ajuda F1 do Assistente de Business Intelligence](../Topic/Business%20Intelligence%20Wizard%20F1%20Help.md)   
 [Tipos de dimensão](../Topic/Dimension%20Types.md)  
  
  