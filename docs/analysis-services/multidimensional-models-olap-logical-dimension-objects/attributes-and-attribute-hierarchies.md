---
title: Atributos e hierarquias de atributo | Microsoft Docs
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
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- regular attributes [Analysis Services]
- parent attributes [Analysis Services]
- hierarchies [Analysis Services], attribute
- attributes [Analysis Services], about attributes
- account attributes [Analysis Services]
- dimensions [Analysis Services], attributes
- key attributes [Analysis Services]
- OLAP objects [Analysis Services], attributes
- attributes [Analysis Services], relationships
- attributes [Analysis Services]
- relationships [Analysis Services], attributes
ms.assetid: 59de1ea2-e7a9-4a53-9ee0-14be52e95643
caps.latest.revision: "49"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 18621eba78a2e4c95de6373485044b5f88e1f744
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="attributes-and-attribute-hierarchies"></a>Atributos e hierarquias de atributos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]As dimensões são coleções de atributos que estão associados a uma ou mais colunas em uma tabela ou exibição na exibição da fonte de dados.  
  
## <a name="key-attribute"></a>Atributo de chave  
 Cada dimensão contém um atributo de chave. Cada atributo está associado a uma ou mais colunas em uma tabela de dimensões. O atributo de chave é o atributo em uma dimensão que identifica as colunas na tabela de dimensões principal usada em relações de chave estrangeira com a tabela de fatos. Normalmente, o atributo de chave representa a coluna ou colunas de chave primária na tabela de dimensões. Você pode definir uma chave primária lógica em uma tabela na exibição de fonte de dados, que não tenha a chave primária física na fonte de dados subjacente. **Para obter mais informações**, consulte [definir chaves primárias lógicas em uma exibição da fonte de dados & #40; Analysis Services & #41; ](../../analysis-services/multidimensional-models/define-logical-primary-keys-in-a-data-source-view-analysis-services.md). Ao definir os atributos de chave, o Assistente para Cubos e o Assistente para Dimensões tentam usar as colunas de chave primária da tabela de dimensões na exibição da fonte de dados. Se a tabela de dimensões não tem uma chave lógica primária ou uma chave física primária definida, os assistentes não definirão corretamente os atributos da chave da dimensão.  
  
## <a name="binding-an-attribute-to-columns-in-data-source-view-tables-or-views"></a>Associando um atributo a colunas nas tabelas de exibição da fonte de dados ou exibições  
 Um atributo é associado às colunas em uma ou mais tabelas de exibição da fonte de dados ou exibições. Um atributo está sempre associado a uma ou mais colunas de chave, o que determina os membros contidos pelo atributo. Por padrão, essa é a única coluna à qual um atributo é associado. Um atributo também pode ser associado a uma ou mais colunas adicionais para fins específicos. Por exemplo, um atributo **NameColumn** propriedade determina o nome que aparece para o usuário para cada membro de atributo - essa propriedade do atributo pode ser associada a uma coluna de dimensão específica por meio de uma exibição da fonte de dados ou pode ser associado a uma coluna calculada na exibição da fonte de dados. Para obter mais informações, consulte [referência de propriedades de atributo de dimensão](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md).  
  
## <a name="attribute-hierarchies"></a>Hierarquias de atributo  
 Por padrão, os membros de atributo são organizados em dois níveis hierárquicos, consistindo de um nível de folha e um nível ALL. O nível ALL contém o valor de agregação dos membros do atributo nas medidas em cada grupo de medidas, no qual a dimensão de cada atributo está relacionada a um membro. No entanto, se o **IsAggregatable** está definida como False, o nível All não será criado. Para obter mais informações, consulte [referência de propriedades de atributo de dimensão](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md).  
  
 Os atributos podem ser, e geralmente são, organizados em hierarquias definidas pelo usuário que fornecem os caminhos de busca detalhada pelos quais os usuários podem pesquisar os dados no grupo de medidas ao qual o atributo está relacionado. Em aplicativos cliente, podem ser usados atributos para fornecer informações de agrupamento e restrição. Quando atributos são organizados em hierarquias definidas pelo usuário, você definir relações entre níveis hierárquicos quando os níveis estão relacionados em um muitos-para-um ou para a relação (chamado um *natural* relação). Por exemplo, em uma hierarquia de Tempo de Calendário, um nível Dia deve estar relacionado ao nível Mês, o nível Mês relacionado ao nível Trimestre e assim por diante. A definição de relações entre os níveis em uma hierarquia definida pelo usuário permite que o Analysis Services defina agregações mais úteis para aumentar o desempenho da consulta e também economizar memória durante o processamento, o que pode ser importante em cubos grandes ou complexos. Para obter mais informações, consulte [hierarquias de usuário](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md), [Create User-Defined hierarquias](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md), e [definir relações de atributo](../../analysis-services/multidimensional-models/attribute-relationships-define.md).  
  
## <a name="attribute-relationships-star-schemas-and-snowflake-schemas"></a>Relações de atributo, esquemas em estrela e esquemas floco de neve  
 Por padrão, em um esquema em estrela, todos os atributos estão diretamente relacionados ao atributo de chave, o que permite que os usuários pesquisem os fatos no cubo com base em qualquer hierarquia de atributos na dimensão. Em um esquema floco de neve, um atributo estará diretamente vinculado ao atributo de chave se a tabela subjacente estiver diretamente vinculada à tabela de fatos, ou vinculado indiretamente pelos atributos associados à chave na tabela subjacente, que vincula a tabela floco de neve à tabela vinculada diretamente.  
  
## <a name="see-also"></a>Consulte também  
 [Criar hierarquias definidas pelo usuário](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)   
 [Definir relações de atributo](../../analysis-services/multidimensional-models/attribute-relationships-define.md)   
 [Referência de propriedades de atributo de dimensão](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
