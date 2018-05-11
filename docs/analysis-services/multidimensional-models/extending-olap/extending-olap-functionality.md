---
title: Estendendo a funcionalidade OLAP | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 804a41edd5667163de9a6b4de1cf0a9fbea71022
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="extending-olap-functionality"></a>Estendendo a funcionalidade OLAP
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Como programador, você pode estender o Analysis Services escrevendo assemblies, extensões personalizadas e procedimentos armazenados que fornecem a funcionalidade que você deseja usar e redefinir em vários aplicativos de banco de dados. Os assemblies são usados para estender as funcionalidade de modelos multidimensional adicionando novos procedimentos e funções à linguagem MDX ou por meio do suplemento de personalização.  
  
 Os procedimentos armazenados podem ser usados para chamar rotinas externas, simplificando o desenvolvimento e a implementação de bancos de dados do Analysis Services ao possibilitar que um código comum seja desenvolvido e armazenado em um único local. Eles podem ser usados para adicionar a seus aplicativos funcionalidades comerciais que não existem como funcionalidade nativa do MDX.  
  
 As personalizações são objetos personalizados que você adiciona a um cubo para fornecer um comportamento que varia de acordo com o usuário. As personalizações não são objetos permanentes no cubo, mas sim objetos que o aplicativo cliente aplica dinamicamente durante a sessão do usuário. Exemplos incluem a alteração da moeda de um valor monetário dependendo da pessoa que está acessando os dados, o fornecimento de KPIs individualizados ou uma lista de sugestões para clientes que compram online regularmente.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Estendendo OLAP por meio de personalizações](../../../analysis-services/multidimensional-models/extending-olap/extending-olap-through-personalizations.md)  
  
 [Extensões de personalização do Analysis Services](../../../analysis-services/multidimensional-models/extending-olap/analysis-services-personalization-extensions.md)  
  
 [Definindo procedimentos armazenados](../../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
