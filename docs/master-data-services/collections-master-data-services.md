---
title: "Cole&#231;&#245;es (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "coleções [Master Data Services]"
  - "coleções [Master Data Services], sobre coleções"
ms.assetid: 5aa1d1e0-b4e5-4897-8e74-01dcf418df73
caps.latest.revision: 14
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 14
---
# Cole&#231;&#245;es (Master Data Services)
  Uma coleção é um grupo de membros folha e consolidados de uma única entidade. Use coleções quando não precisar de uma hierarquia completa e desejar exibir agrupamentos diferentes de membros para relatório ou análise, ou quando precisar criar uma taxonomia.  
  
> [!NOTE]  
>  A coleção é preterida.  
  
## O que as coleções contêm  
 Coleções não limitam o número ou o tipo de membros que podem ser incluídos, desde que os membros estejam dentro da mesma entidade. Uma coleção pode conter membros folha e consolidados de várias hierarquias explícitas obrigatórias e não obrigatórias.  
  
 Quando você cria uma coleção, não está criando uma estrutura hierárquica; você está criando uma lista simples de membros. Quando você seleciona um nó de uma hierarquia e adiciona-o à coleção, o membro consolidado selecionado é o único membro acrescentado à coleção.  
  
 Uma coleção também pode conter outras coleções. É possível usar coleções de coleções para criar taxonomias.  
  
 Quando cria uma coleção, você é listado automaticamente como o proprietário. Se você for um administrador, poderá criar outros atributos para a coleção conforme necessário.  
  
## Exibições de assinatura para coleções  
 Há dois tipos de exibições de assinatura que mostram coleções. O formato **Atributos da coleção** mostra uma lista de coleções e todos os atributos relacionados às coleções (como descrição ou proprietário). O formato **Coleções** mostra todos os membros em todas as coleções, bem como cada peso de membros e a ordem de classificação. Para obter mais informações, consulte [Visão geral: Exportando dados &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md).  
  
 Se você definir valores de peso para membros específicos em uma coleção, estes valores estarão disponíveis em exibições de assinatura relacionadas.  
  
## Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar uma nova coleção.|[Criar uma coleção &#40;Master Data Services&#41;](../master-data-services/create-a-collection-master-data-services.md)|  
|Adicionar membros a uma coleção existente.|[Adicionar membros a uma coleção &#40;Master Data Services&#41;](../master-data-services/add-members-to-a-collection-master-data-services.md)|  
  
## Conteúdo relacionado  
  
-   [Hierarquias explícitas &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [Visão geral: Exportando dados &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)  
  
  