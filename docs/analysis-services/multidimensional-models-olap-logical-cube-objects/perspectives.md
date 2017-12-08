---
title: Perspectivas | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- ready-only cube view
- OLAP objects [Analysis Services], perspectives
- storing data [Analysis Services], perspectives
- perspectives [Analysis Services]
- cubes [Analysis Services], perspectives
- visibility [Analysis Services]
- storage [Analysis Services], perspectives
ms.assetid: b064171e-b1b4-4f32-95e5-59e1b831c4c9
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2a892a571a70b3f5bff5fb16496c2fee5d18f151
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="perspectives"></a>Perspectivas
  Uma perspectiva é uma definição que permite os usuários visualizem um cubo de um modo mais simples. Uma perspectiva é um subconjunto dos recursos de um cubo. Uma perspectiva permite que os administradores criem exibições do cubo, ajudando outros usuários a se concentrarem nos dados mais relevantes. Uma perspectiva contém subconjuntos de todos os objetos de um cubo. Uma perspectiva não pode incluir elementos que não estão definidos no cubo pai.  
  
 Um simples objeto <xref:Microsoft.AnalysisServices.Perspective> está composto de: informações básicas, dimensões, grupos de medidas, cálculos, KPIs e ações. As informações básicas incluem o nome e a medida padrão da perspectiva. As dimensões são um subconjunto das dimensões do cubo. Os grupos de medidas são um subconjunto dos grupos de medidas do cubo. Os cálculos são um subconjunto dos cálculos do cubo. Os KPIs são um subconjunto dos KPIs do cubo. As ações são um subconjunto das ações do cubo.  
  
 Um cubo tem que ser atualizado e processado antes que a perspectiva possa ser usada.  
  
 Os cubos podem ser objetos muito complexos para usuários explorarem no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Um único cubo pode representar o conteúdo de um data warehouse completo, com vários grupos de medidas em um cubo representando várias tabelas de fatos e várias dimensões com base em várias tabelas de dimensões. Um cubo assim pode ser muito complexo e poderoso, mas complicado para usuários que precisam apenas interagir com uma pequena parte do cubo para satisfazer seus requisitos de Business Intelligence e geração de relatórios.  
  
 Em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode usar uma perspectiva para reduzir a complexidade de um cubo no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Uma perspectiva define um subconjunto exibível de um cubo que fornece pontos de vista concentrados, específicos à empresa ou específicos ao aplicativo. A perspectiva controla a visibilidade de objetos contidos por um cubo. Os seguintes objetos podem ser exibidos ou ocultados em uma perspectiva:  
  
-   Dimensões  
  
-   Atributos  
  
-   Hierarquias  
  
-   Grupos de medidas  
  
-   Medidas  
  
-   Indicadores chave de desempenho (KPIs)  
  
-   Cálculos (membros calculados, conjuntos nomeados e comandos de script)  
  
-   Ações  
  
 Por exemplo, o **Adventure Works** cubo o [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] exemplo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados contém onze grupos de medidas e vinte dimensões de cubo diferentes, representando vendas, previsão de vendas e dados financeiros. Um aplicativo cliente pode fazer referência diretamente ao cubo completo, mas esse ponto de vista pode ser muito complicado para um usuário, tentando extrair informações básicas de previsão de vendas. Em vez disso, o mesmo usuário pode usar o **metas de venda** perspectiva para limitar a exibição do **Adventure Works** cubo apenas aos objetos relevantes à previsão de vendas.  
  
 Os objetos em um cubo que não são visíveis ao usuário por meio de uma perspectiva podem ser referenciados diretamente e recuperados, usando instruções XML for Analysis (XMLA), linguagem MDX ou DMX (extensões de mineração de dados). As perspectivas não restringem acesso aos objetos em um cubo e não devem ser usadas desse modo; em vez disso, as perspectivas são usadas para fornecer uma melhor experiência ao usuário ao acessar o cubo.  
  
 Uma perspectiva é uma exibição apenas leitura do cubo; objetos no cubo não podem ser renomeados ou alterados usando uma perspectiva. Do mesmo modo, o comportamento ou recursos de um cubo, como o uso de totais visuais, não podem ser alterados por uma perspectiva.  
  
## <a name="security"></a>Segurança  
 As perspectivas não se destinam a serem usadas como um mecanismo de segurança, mas como uma ferramenta para fornecer uma melhor experiência ao usuário com os aplicativos de business intelligence. Toda a segurança de uma determinada perspectiva é herdada do cubo subjacente. Por exemplo, as perspectivas não podem fornecer acesso a objetos em um cubo ao qual o usuário ainda não tem acesso. A segurança do cubo deve ser resolvida antes que o acesso a objetos no cubo possa ser fornecido por meio de uma perspectiva.  
  
  
