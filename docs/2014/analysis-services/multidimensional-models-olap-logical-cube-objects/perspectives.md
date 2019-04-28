---
title: Perspectivas | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2856bca26e8a49ffdb2ed5187479434c7762015b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62702633"
---
# <a name="perspectives"></a>perspectivas
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Uma perspectiva é uma definição que permite os usuários visualizem um cubo de um modo mais simples. Uma perspectiva é um subconjunto dos recursos de um cubo. Uma perspectiva permite que os administradores criem exibições do cubo, ajudando outros usuários a se concentrarem nos dados mais relevantes. Uma perspectiva contém subconjuntos de todos os objetos de um cubo. Uma perspectiva não pode incluir elementos que não estão definidos no cubo pai.  
  
 Um simples objeto <xref:Microsoft.AnalysisServices.Perspective> é composto de: informações básicas, dimensões, grupos de medidas, cálculos, KPIs e ações. As informações básicas incluem o nome e a medida padrão da perspectiva. As dimensões são um subconjunto das dimensões do cubo. Os grupos de medidas são um subconjunto dos grupos de medidas do cubo. Os cálculos são um subconjunto dos cálculos do cubo. Os KPIs são um subconjunto dos KPIs do cubo. As ações são um subconjunto das ações do cubo.  
  
 Um cubo tem que ser atualizado e processado antes que a perspectiva possa ser usada.  
  
 Os cubos podem ser objetos muito complexos para usuários explorarem no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Um único cubo pode representar o conteúdo de um data warehouse completo, com vários grupos de medidas em um cubo representando várias tabelas de fatos e várias dimensões com base em várias tabelas de dimensões. Um cubo assim pode ser muito complexo e poderoso, mas complicado para usuários que precisam apenas interagir com uma pequena parte do cubo para satisfazer seus requisitos de Business Intelligence e geração de relatórios.  
  
 Na [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode usar uma perspectiva para reduzir a complexidade de um cubo no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Uma perspectiva define um subconjunto exibível de um cubo que fornece pontos de vista concentrados, específicos à empresa ou específicos ao aplicativo. A perspectiva controla a visibilidade de objetos contidos por um cubo. Os seguintes objetos podem ser exibidos ou ocultados em uma perspectiva:  
  
-   Dimensões  
  
-   Atributos  
  
-   Hierarquias  
  
-   Grupos de medidas  
  
-   medidas  
  
-   Indicadores chave de desempenho (KPIs)  
  
-   Cálculos (membros calculados, conjuntos nomeados e comandos de script)  
  
-   Ações  
  
 Por exemplo, o **Adventure Works** cubo as [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] exemplo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados contém onze grupos de medidas e vinte dimensões de cubo diferentes, representando vendas, previsão de vendas e dados financeiros. Um aplicativo cliente pode fazer referência diretamente ao cubo completo, mas esse ponto de vista pode ser muito complicado para um usuário, tentando extrair informações básicas de previsão de vendas. Em vez disso, o mesmo usuário pode usar o **metas de vendas** perspectiva para limitar a exibição do **Adventure Works** cubo apenas aos objetos relevantes à previsão de vendas.  
  
 Os objetos em um cubo que não são visíveis ao usuário por meio de uma perspectiva podem ser referenciados diretamente e recuperados, usando instruções XML for Analysis (XMLA), linguagem MDX ou DMX (extensões de mineração de dados). As perspectivas não restringem acesso aos objetos em um cubo e não devem ser usadas desse modo; em vez disso, as perspectivas são usadas para fornecer uma melhor experiência ao usuário ao acessar o cubo.  
  
 Uma perspectiva é uma exibição apenas leitura do cubo; objetos no cubo não podem ser renomeados ou alterados usando uma perspectiva. Do mesmo modo, o comportamento ou recursos de um cubo, como o uso de totais visuais, não podem ser alterados por uma perspectiva.  
  
## <a name="security"></a>Segurança  
 As perspectivas não se destinam a serem usadas como um mecanismo de segurança, mas como uma ferramenta para fornecer uma melhor experiência ao usuário com os aplicativos de business intelligence. Toda a segurança de uma determinada perspectiva é herdada do cubo subjacente. Por exemplo, as perspectivas não podem fornecer acesso a objetos em um cubo ao qual o usuário ainda não tem acesso. A segurança do cubo deve ser resolvida antes que o acesso a objetos no cubo possa ser fornecido por meio de uma perspectiva.  
  
  
