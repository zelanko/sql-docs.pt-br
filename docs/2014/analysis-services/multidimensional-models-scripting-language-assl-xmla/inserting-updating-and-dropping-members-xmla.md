---
title: Inserindo, atualizando e descartando Membros (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- inserting dimension members
- XML for Analysis, members
- removing dimension members
- dropping dimension members
- write-enabled dimensions [Analysis Services]
- XMLA, members
- deleting dimension members
- dimensions [Analysis Services], XML for Analysis
ms.assetid: bba922b5-8b88-4051-9506-ff055248182a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 98da3e0f7a9b61b178372d9b24b8b595ab6b6626
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62727160"
---
# <a name="inserting-updating-and-dropping-members-xmla"></a>Inserindo, atualizando e descartando membros (XMLA)
  Você pode usar os comandos [Insert](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla), [Update](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)e [drop](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla) em XML for Analysis (XMLA) para inserir, atualizar ou excluir, respectivamente, membros de uma dimensão habilitada para gravação. Para obter mais informações sobre dimensões habilitadas para gravação, consulte [dimensões habilitadas para gravação](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
## <a name="inserting-new-members"></a>Inserindo membros novos  
 O comando `Insert` insere novos membros em atributos especificados de uma dimensão habilitada para gravação.  
  
 Antes de criar o comando `Insert`, você deve ter as seguintes informações disponíveis para os membros novos a serem inseridos:  
  
-   A dimensão na qual os membros novos serão inseridos.  
  
-   O atributo da dimensão no qual os membros novos serão inseridos.  
  
-   Os nomes dos membros novos, incluindo qualquer tradução aplicável para o nome.  
  
-   As chaves dos membros novos. Se um atributo usar uma chave composta, ela poderá exigir diversos valores.  
  
-   Os valores para qualquer propriedade de atributo aplicável que não são implementados como outros atributos dentro da dimensão. Tais propriedades de atributo incluem operações unárias, traduções, rollups personalizados, propriedades de rollup personalizadas e níveis ignorados.  
  
 O comando `Insert` só contém duas propriedades:  
  
-   A propriedade [Object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) , que contém uma referência de objeto para a dimensão na qual os membros devem ser inseridos. A referência de objeto contém o identificador de banco de dados, o identificador de cubo e o identificador de dimensão para a dimensão.  
  
-   A propriedade [Attributes](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attributes-element-xmla) , que contém um ou mais elementos [Attribute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attribute-element-xmla) para identificar os atributos nos quais os membros devem ser inseridos. Cada elemento `Attribute` identifica um atributo e fornece o nome, valor, traduções, operador unário, rollup personalizado, propriedades de rollup personalizadas e níveis ignorados para um único membro a ser adicionado ao atributo identificado.  
  
    > [!NOTE]  
    >  Todas as propriedades do elemento `Attribute` devem ser incluídas. Caso contrário, poderá ocorrer um erro.  
  
## <a name="updating-existing-members"></a>Atualizando membros existentes  
 O comando `Update` atualiza os membros existentes em atributos especificados, com base em relacionamentos com outros membros em outros atributos, em uma dimensão habilitada para gravação. O comando `Update` pode mover membros para outros níveis em hierarquias contidas pela dimensão e pode ser usado para reestruturar hierarquias pai-filho definidas por atributos pai.  
  
 Antes de criar o comando `Update`, você deve ter as seguintes informações disponíveis para os membros a serem atualizados:  
  
-   A dimensão na qual os membros existentes serão atualizados.  
  
-   Os atributos de dimensão nos quais os membros existentes serão atualizados.  
  
-   As chaves dos membros existentes. Se um atributo usar uma chave composta, ela poderá exigir diversos valores.  
  
-   Os valores para qualquer propriedade de atributo aplicável que não são implementados como outros atributos dentro da dimensão. Tais propriedades de atributo incluem operações unárias, traduções, rollups personalizados, propriedades de rollup personalizadas e níveis ignorados.  
  
 O comando `Update` só contém três propriedades obrigatórias:  
  
-   A propriedade `Object`, que contém uma referência de objeto para a dimensão na qual os membros serão atualizados. A referência de objeto contém o identificador de banco de dados, o identificador de cubo e o identificador de dimensão para a dimensão.  
  
-   A propriedade `Attributes`, que contém um ou mais elementos `Attribute` para identificar os atributos nos quais os membros serão atualizados. O elemento `Attribute` identifica um atributo e fornece o nome, valor, traduções, operador unário, rollup personalizado, propriedades de rollup personalizadas e níveis ignorados para um único membro a ser atualizado para o atributo identificado.  
  
    > [!NOTE]  
    >  Todas as propriedades do elemento `Attribute` devem ser incluídas. Caso contrário, poderá ocorrer um erro.  
  
-   A propriedade [Where](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/where-element-xmla) , que contém um ou mais `Attribute` elementos que restringem os atributos nos quais os membros devem ser atualizados. A `Where` propriedade é crucial para limitar um `Update` comando a instâncias específicas de um membro. Se a `Where` propriedade não for especificada, todas as instâncias de um determinado membro serão atualizadas. Por exemplo, existem três clientes para quem você deseja alterar o nome da cidade de Redmond para Bellevue. Para alterar o nome da cidade, forneça uma propriedade `Where` que identifique os três membros no atributo Customer para o qual os membros do atributo City devem ser alterados. Se você não fornecer essa propriedade `Where`, todos os clientes cujo nome da cidade é Redmond receberiam o nome da cidade Bellevue após a execução do comando `Update`.  
  
    > [!NOTE]  
    >  Com exceção dos membros novos, o comando `Update` só pode atualizar valores chaves de atributo para atributos não incluídos na cláusula `Where`. Por exemplo, o nome da cidade não pode ser atualizado quando um cliente é atualizado; caso contrário, o nome da cidade seria alterado para todos os clientes.  
  
### <a name="updating-members-in-parent-attributes"></a>Atualizando membros em atributos pai  
 Para dar suporte a atributos pai `Update` , o comando as propriedades [MoveWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/movewithdescendants-element-xmla)MovewithDescedants opcionais. A configuração da propriedade `MoveWithDescendants` como verdadeira indica que os descendentes do membro pai também devem ser movidos com o membro pai quando o seu identificador for alterado. Se esse valor for definido como falso, mover um membro pai fará com que os descendentes imediatos desse membro pai sejam promovidos ao nível no qual o membro pai residia anteriormente.  
  
 Ao atualizar os membros em um atributo pai, o comando `Update` não poderá atualizar os membros em outros atributos.  
  
## <a name="dropping-existing-members"></a>Descartando membros existentes  
 Antes de criar o comando `Drop`, você deve ter as seguintes informações disponíveis para os membros a serem descartados:  
  
-   A dimensão na qual os membros existentes serão descartados.  
  
-   Os atributos de dimensão nos quais os membros existentes serão descartados.  
  
-   As chaves dos membros existentes serem descartados. Se um atributo usar uma chave composta, ela poderá exigir diversos valores.  
  
 O comando `Drop` só contém duas propriedades obrigatórias:  
  
-   A propriedade `Object` que contém uma referência de objeto para a dimensão na qual os membros devem ser descartados. A referência de objeto contém o identificador de banco de dados, o identificador de cubo e o identificador de dimensão para a dimensão.  
  
-   A propriedade `Where`, que contém um ou mais elementos `Attribute` para restringir os atributos nos quais os membros serão excluídos. A propriedade `Where` é fundamental para limitar um comando `Drop` a instâncias específicas de um membro. Se o comando `Where` não for especificado, serão descartadas todas as instâncias de um determinado membro. Por exemplo, existem três clientes que você deseja descartar de Redmond. Para descartar esses clientes, forneça uma propriedade `Where` que identifique os três membros de um atributo Customer a ser removido e o membro Redmond do atributo City a partir do qual os três clientes serão removidos. Se a propriedade `Where` só especificar o membro Redmond do atributo City, todos os clientes associados a Redmond serão descartados pelo comando `Drop`. Se a propriedade `Where` só especificar os três membros do atributo Customer, os três clientes serão totalmente excluídos pelo comando `Drop`.  
  
    > [!NOTE]  
    >  Os elementos `Attribute` incluídos em um comando `Drop` só devem conter as propriedades `AttributeName` e `Keys`. Caso contrário, poderá ocorrer um erro.  
  
### <a name="dropping-members-in-parent-attributes"></a>Descartando membros em atributos pai  
 A definição da propriedade [DeleteWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/deletewithdescendants-element-xmla) indica que os descendentes de um membro pai também devem ser excluídos com o membro pai. Se esse valor for definido como falso, os descendentes imediatos do membro pai serão promovidos ao nível no qual o membro pai residia anteriormente.  
  
> [!IMPORTANT]  
>  Um usuário só precisa ter permissões de exclusão para o membro pai para poder excluir o membro pai e seus descendentes. Um usuário não precisa excluir permissões nos descendentes.  
  
## <a name="see-also"></a>Consulte Também  
 [Descartar elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)   
 [Inserir elemento &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)   
 [Atualizar o elemento &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Definindo e identificando objetos &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)   
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
