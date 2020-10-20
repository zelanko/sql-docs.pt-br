---
description: Gerenciador de dependências de entidade
title: Gerenciador de dependências de entidade
ms.custom: ''
ms.date: 04/06/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
keywords:
- master data services
ms.assetid: 9d922118-1412-4a9d-9c02-70d6c48d6c0d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e0b20fde852e02662780f75bd14e4b9023e01d80
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192397"
---
# <a name="entity-dependencies-explorer"></a>Gerenciador de dependências de entidade

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  
[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 2016 adiciona uma nova página de gerenciador, Dependências da Entidade, que fornece uma maneira alternativa para visualizar relações entre membros de entidade em um modelo, conforme especificado por seus valores DBA (atributo baseado em domínio), mas sem a necessidade de definir uma Hierarquia Derivada primeiro.   
  
Ele ajuda a responder a pergunta "que está consumindo minha entidade e como?". A exibição é semelhante à página do gerenciador Hierarquia Derivada, mas é mais inclusiva. Ela mostra todas as relações de DBA, não apenas aquelas definidas como parte de uma hierarquia específica. Uma definição de hierarquia não é necessária porque a estrutura hierárquica exibida é simplesmente inferida de DBAs existentes.  
  
No menu de página do Gerenciador, o item de menu Dependências da Entidade lista todas as entidades no modelo que são dependentes pelo menos de uma entidade (ou seja, pelo menos uma entidade tem um DBA que faz referência à entidade listada). O número de dependências (diretas e indiretas) é exibido próximo ao nome da entidade e a lista é classificada por esse número com as entidades mais intensamente referenciadas na parte superior. A captura de tela abaixo, obtida do modelo do cliente dos [dados de exemplo](./sql-server-samples-model-deployment-packages-mds.md), mostra que a entidade BigArea é referenciada (direta ou indiretamente) por 7 entidades:  
  
![MDS_EntityDependencies_Menu.jpg](../master-data-services/media/mds-entitydependencies-menu-jpg.jpg)  
    
Clicar neste item de menu abre a nova página do gerenciador de Dependências da Entidade para a entidade BigArea, que mostra como os membros da entidade são consumidos. Ele mostra uma exibição hierárquica com membros BigArea na parte superior da árvore, com os membros de suas 7 entidades de consumo aninhadas abaixo:  
  
![MDS_EntityDependencies_Tree.jpg](../master-data-services/media/mds-entitydependencies-tree-jpg.jpg)  
    
Uma entidade pode ser diretamente consumida por mais de uma entidade. No exemplo acima, as entidades SubRegion e RegionClimate consomem (têm referências de DBA também) a entidade da Região. Os membros de cada entidade de consumo são agrupados em um nó pai que tem o nome de entidade:   
  
![MDS_EntityDependencies_Entity_Node.jpg](../master-data-services/media/mds-entitydependencies-entity-node-jpg.jpg)  
  
Esses nós de árvore de contêiner têm um ícone de grade à esquerda do nome da entidade e o texto é colorido por profundidade do nível de hierarquia. O exemplo acima mostra que a sub-região "CDSR {Canadá}" tem uma referência de DBA para a região "CDR {Canadá}", que faz referência a área "CDA {Canadá}", que referencia a BigArea "NAm {N. America}".  
  
A exibição é totalmente editável, assim como na página Gerenciador de Hierarquias. Relações pai-filho podem ser modificadas na árvore por membros filho de recortar e colar ou arrastar-soltar, de um pai para outro. Outros valores de atributo de membro podem ser modificados no painel de detalhes à direita da árvore.   
  
  
  
