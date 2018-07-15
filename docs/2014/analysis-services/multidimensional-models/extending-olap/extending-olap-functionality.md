---
title: Estendendo a funcionalidade OLAP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 49a17ff3-94e9-4969-84fc-37d49e63933b
caps.latest.revision: 4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d55ef159195d42935db271c3b3a51860fd698ec9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220256"
---
# <a name="extending-olap-functionality"></a>Estendendo a funcionalidade OLAP
  Como programador, você pode estender o Analysis Services escrevendo assemblies, extensões personalizadas e procedimentos armazenados que fornecem a funcionalidade que você deseja usar e redefinir em vários aplicativos de banco de dados. Os assemblies são usados para estender as funcionalidade de modelos multidimensional adicionando novos procedimentos e funções à linguagem MDX ou por meio do suplemento de personalização.  
  
 Os procedimentos armazenados podem ser usados para chamar rotinas externas, simplificando o desenvolvimento e a implementação de bancos de dados do Analysis Services ao possibilitar que um código comum seja desenvolvido e armazenado em um único local. Eles podem ser usados para adicionar a seus aplicativos funcionalidades comerciais que não existem como funcionalidade nativa do MDX.  
  
 As personalizações são objetos personalizados que você adiciona a um cubo para fornecer um comportamento que varia de acordo com o usuário. As personalizações não são objetos permanentes no cubo, mas sim objetos que o aplicativo cliente aplica dinamicamente durante a sessão do usuário. Exemplos incluem a alteração da moeda de um valor monetário dependendo da pessoa que está acessando os dados, o fornecimento de KPIs individualizados ou uma lista de sugestões para clientes que compram online regularmente.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Estendendo o OLAP por meio de personalizações](extending-olap-through-personalizations.md)  
  
 [Extensões de personalização do Analysis Services](analysis-services-personalization-extensions.md)  
  
 [Definindo procedimentos armazenados](../../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
