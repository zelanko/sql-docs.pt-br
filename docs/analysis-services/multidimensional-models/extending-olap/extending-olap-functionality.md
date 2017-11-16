---
title: Estendendo a funcionalidade OLAP | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 49a17ff3-94e9-4969-84fc-37d49e63933b
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 20749b47397d4cd1826fbdca65be78e7f1905025
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="extending-olap-functionality"></a>Estendendo a funcionalidade OLAP
  Como programador, você pode estender o Analysis Services escrevendo assemblies, extensões personalizadas e procedimentos armazenados que fornecem a funcionalidade que você deseja usar e redefinir em vários aplicativos de banco de dados. Os assemblies são usados para estender as funcionalidade de modelos multidimensional adicionando novos procedimentos e funções à linguagem MDX ou por meio do suplemento de personalização.  
  
 Os procedimentos armazenados podem ser usados para chamar rotinas externas, simplificando o desenvolvimento e a implementação de bancos de dados do Analysis Services ao possibilitar que um código comum seja desenvolvido e armazenado em um único local. Eles podem ser usados para adicionar a seus aplicativos funcionalidades comerciais que não existem como funcionalidade nativa do MDX.  
  
 As personalizações são objetos personalizados que você adiciona a um cubo para fornecer um comportamento que varia de acordo com o usuário. As personalizações não são objetos permanentes no cubo, mas sim objetos que o aplicativo cliente aplica dinamicamente durante a sessão do usuário. Exemplos incluem a alteração da moeda de um valor monetário dependendo da pessoa que está acessando os dados, o fornecimento de KPIs individualizados ou uma lista de sugestões para clientes que compram online regularmente.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Estendendo OLAP por meio de personalizações](../../../analysis-services/multidimensional-models/extending-olap/extending-olap-through-personalizations.md)  
  
 [Extensões de personalização do Analysis Services](../../../analysis-services/multidimensional-models/extending-olap/analysis-services-personalization-extensions.md)  
  
 [Definindo procedimentos armazenados](../../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  

