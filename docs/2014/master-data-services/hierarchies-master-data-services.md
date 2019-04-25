---
title: Hierarquias (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Master Data Services]
- hierarchies [Master Data Services], about hierarchies
ms.assetid: 70dbb1fc-ead7-45be-9552-a45e3ccd8d21
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: af91e39bd3c338670906bb5dc50987bc0c413746
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62765131"
---
# <a name="hierarchies-master-data-services"></a>Hierarquias (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], uma hierarquia é uma estrutura de árvore que você pode usar para:  
  
-   Agrupar membros semelhantes para fins organizacionais.  
  
-   Consolidar e resumir membros para relatório e análise.  
  
## <a name="what-hierarchies-contain"></a>O que as hierarquias contêm  
 Cada hierarquia contém os membros de uma ou mais entidades. Quando um membro é adicionado, alterado ou excluído, todas as hierarquias são atualizadas. Isso assegura que os dados sejam precisos em todas as hierarquias. As hierarquias também ajudam a garantir que cada membro é contado apenas uma vez.  
  
 Se você quiser criar um agrupamento de um subconjunto de membros, use uma coleção. Para obter mais informações, consulte [Collections &#40;Master Data Services&#41;](collections-master-data-services.md).  
  
## <a name="kinds-of-hierarchies"></a>Tipos de hierarquia  
 Você pode criar várias hierarquias para exibir e organizar seus membros de formas diferentes. Você pode criar:  
  
-   Hierarquias desbalanceadas de uma única entidade, que são chamadas de hierarquias explícitas. Para obter mais informações, consulte [Explicit Hierarchies &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md).  
  
-   Hierarquias baseadas em nível de várias entidades, com base nas relações existentes entre as entidades e seus atributos, que são chamadas de hierarquias derivadas. Para obter mais informações, consulte [Derived Hierarchies &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md).  
  
> [!NOTE]  
>  Todos os membros em uma hierarquia devem estar dentro do mesmo modelo.  
  
## <a name="hierarchies-are-not-taxonomies"></a>Hierarquias não são taxonomias  
 Uma hierarquia é diferente de uma taxonomia. Uma taxonomia organiza os membros por vários atributos ao mesmo tempo, enquanto uma hierarquia organiza os membros por um atributo de cada vez. Uma taxonomia pode incluir o mesmo membro várias vezes, enquanto uma hierarquia inclui um membro somente uma vez.  
  
 Por exemplo, a mesma bicicleta pode ser incluída duas vezes em uma taxonomia: uma vez porque é vermelha e uma vez porque é tamanho 38. Em uma hierarquia, a bicicleta é incluída apenas uma vez, de modo que você deve decidir se deseja mostrá-la em relação à cor ou ao tamanho.  
  
## <a name="hierarchy-example"></a>Exemplo de hierarquia  
 No exemplo a seguir, os membros de produto são agrupados por membros de subcategoria.  
  
 ![Exemplo de hierarquia agrupada por subcategoria](../../2014/master-data-services/media/mds-conc-hierarchy.gif "Exemplo de hierarquia agrupada por subcategoria")  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Habilitar uma entidade para hierarquias explícitas e coleções.|[Habilitar uma entidade para hierarquias explícitas e coleções &#40;Master Data Services&#41;](../../2014/master-data-services/enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md)|  
|Criar uma hierarquia explícita.|[Criar uma hierarquia explícita &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|Criar uma hierarquia derivada.|[Criar uma hierarquia derivada &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|Ocultar ou excluir níveis em uma hierarquia derivada existente.|[Ocultar ou excluir níveis em uma hierarquia derivada &#40;Master Data Services&#41;](../../2014/master-data-services/hide-or-delete-levels-in-a-derived-hierarchy-master-data-services.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Hierarquias explícitas &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [Hierarquias derivadas &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)  
  
-   [Hierarquias recursivas &#40;Master Data Services&#41;](../../2014/master-data-services/recursive-hierarchies-master-data-services.md)  
  
-   [Hierarquias derivadas com limites explícitos &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)  
  
-   [Coleções &#40;Master Data Services&#41;](collections-master-data-services.md)  
  
  
