---
title: "Criação automática de código (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9adbd5e1-f28c-4fb5-afa7-082de2831f3e
caps.latest.revision: 8
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 9eba993695071796b6f9a4dfb4b05a1d1382be5a
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="automatic-code-creation-master-data-services"></a>Criação automática de código (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], os valores numéricos podem ser gerados automaticamente para o atributo de código, ou para qualquer outro atributo numérico. Quando códigos são gerados automaticamente, não está impedido de inserir outros valores para códigos; um valor inicial é definido automaticamente.  
  
## <a name="generating-code-values"></a>Gerando valores de códigos  
 Os administradores podem configurar valores gerados automaticamente para o atributo de código editando as propriedades da entidade associada. Eles podem especificar um valor inicial e cada valor subsequente é acrescido de um.  
  
 Quando você digita valores de códigos no MDS, em uma das ferramentas ou usando o processo de preparo, poderá deixar o valor de código em branco e um valor de código será gerado automaticamente. Ou você pode especificar um valor de código de sua escolha.  
  
## <a name="generating-other-attribute-values"></a>Gerando outros valores de atributo  
 Os administradores podem gerar valores automaticamente para atributos que não sejam código, criando regras de negócio. Eles podem especificar um valor inicial e especificar o número de acréscimo em cada valor subsequente.  
  
 Quando você insere valores de atributo no MDS, em uma das ferramentas ou usando o processo de preparo, o valor de atributo pode ficar em branco. Quando forem aplicadas regras de negócio, os valores serão incrementados com base no valor existente mais alto. Por exemplo, se sua regra for "Atributo padrão para um valor gerado que inicia em 1 e é incrementado de 4" e o valor atual mais alto para o atributo for 700, o valor do próximo membro adicionado será 704.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Gerar automaticamente valores para o atributo de código.|[Gerar automaticamente valores de atributo de código &#40;Master Data Services&#41;](../master-data-services/automatically-generate-code-attribute-values-master-data-services.md)|  
|Gerar automaticamente valores para outros atributos.|[Gerar automaticamente valores de atributo diferentes de código &#40;Master Data Services&#41;](../master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Visão geral do Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
-   [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
-   [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  
