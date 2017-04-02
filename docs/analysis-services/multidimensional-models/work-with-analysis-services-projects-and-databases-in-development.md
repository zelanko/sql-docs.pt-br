---
title: "Trabalhando com projetos e bancos de dados do Analysis Services durante a fase de desenvolvimento | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Analysis Services, projetos"
ms.assetid: 39cf9166-fa92-40fe-9962-210a52461257
caps.latest.revision: 16
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 16
---
# Trabalhando com projetos e bancos de dados do Analysis Services durante a fase de desenvolvimento
  Você pode desenvolver um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo de projeto ou online.  
  
## Único desenvolvedor  
 Quando apenas um desenvolvedor estiver desenvolvendo o banco de dados inteiro do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e todos os seus objetos constituintes, o desenvolvedor pode usar o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo de projeto ou online a qualquer momento durante o ciclo de vida da solução de business intelligence. No caso de um único desenvolvedor, a escolha dos modos não é imprescindível. A manutenção de um arquivo de projeto offline integrado ao sistema de controle de código-fonte apresenta muitas vantagens, como arquivamento e reversão. No entanto, havendo um único desenvolvedor, não haverá problema de comunicar alterações a outro desenvolvedor.  
  
## Vários desenvolvedores  
 Se houver vários desenvolvedores trabalhando em uma solução de business intelligence, surgirão problemas se eles não utilizarem o modo de projeto com o controle de código-fonte na maior parte do tempo, senão integralmente. O controle de código-fonte evita que dois desenvolvedores alterem ao mesmo tempo o mesmo objeto.  
  
 Por exemplo, suponhamos que um desenvolvedor esteja trabalhando em modo de projeto e alterando os objetos selecionados. Enquanto ele faz essas alterações, outro desenvolvedor altera o banco de dados implantado em modo online. Um problema surgirá quando o primeiro desenvolvedor tentar implantar seu projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] modificado. Ou seja, o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] detectará que os objetos mudaram no banco de dados implantado e pedirá que o desenvolvedor substitua todo o banco de dados, o que eliminará as alterações feitas pelo segundo desenvolvedor. Como o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] não tem como resolver as alterações entre a instância do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e os objetos do projeto que estão prestes a serem substituídos, a única opção real do primeiro desenvolvedor será descartar suas alterações e iniciar um novo projeto com base na versão atual do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
  