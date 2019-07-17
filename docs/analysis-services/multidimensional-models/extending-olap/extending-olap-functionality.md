---
title: Estendendo a funcionalidade OLAP | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 06b73c0b9f8b4c2d93bb81762ebec442f94e7198
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68177795"
---
# <a name="extending-olap-functionality"></a>Estendendo a funcionalidade OLAP
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Como programador, você pode estender o Analysis Services escrevendo assemblies, extensões personalizadas e procedimentos armazenados que fornecem a funcionalidade que você deseja usar e redefinir em vários aplicativos de banco de dados. Os assemblies são usados para estender as funcionalidade de modelos multidimensional adicionando novos procedimentos e funções à linguagem MDX ou por meio do suplemento de personalização.  
  
 Os procedimentos armazenados podem ser usados para chamar rotinas externas, simplificando o desenvolvimento e a implementação de bancos de dados do Analysis Services ao possibilitar que um código comum seja desenvolvido e armazenado em um único local. Eles podem ser usados para adicionar a seus aplicativos funcionalidades comerciais que não existem como funcionalidade nativa do MDX.  
  
 As personalizações são objetos personalizados que você adiciona a um cubo para fornecer um comportamento que varia de acordo com o usuário. As personalizações não são objetos permanentes no cubo, mas sim objetos que o aplicativo cliente aplica dinamicamente durante a sessão do usuário. Exemplos incluem a alteração da moeda de um valor monetário dependendo da pessoa que está acessando os dados, o fornecimento de KPIs individualizados ou uma lista de sugestões para clientes que compram online regularmente.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Estendendo o OLAP por meio de personalizações](../../../analysis-services/multidimensional-models/extending-olap/extending-olap-through-personalizations.md)  
  
 [Extensões de personalização do Analysis Services](../../../analysis-services/multidimensional-models/extending-olap/analysis-services-personalization-extensions.md)  
  
 [Definindo procedimentos armazenados](../../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
