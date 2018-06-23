---
title: Trabalhar com o Analysis Services projetos e bancos de dados durante a fase de desenvolvimento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Analysis Services, projects
ms.assetid: 39cf9166-fa92-40fe-9962-210a52461257
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2f6aa0b033d0f30f2c4db017583d0f785e13215d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121374"
---
# <a name="working-with-analysis-services-projects-and-databases-during-the-development-phase"></a>Trabalhando com projetos e bancos de dados do Analysis Services durante a fase de desenvolvimento
  Você pode desenvolver um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo de projeto ou online.  
  
## <a name="single-developer"></a>Único desenvolvedor  
 Quando apenas um desenvolvedor estiver desenvolvendo o banco de dados inteiro do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e todos os seus objetos constituintes, o desenvolvedor pode usar o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo de projeto ou online a qualquer momento durante o ciclo de vida da solução de business intelligence. No caso de um único desenvolvedor, a escolha dos modos não é imprescindível. A manutenção de um arquivo de projeto offline integrado ao sistema de controle de código-fonte apresenta muitas vantagens, como arquivamento e reversão. No entanto, havendo um único desenvolvedor, não haverá problema de comunicar alterações a outro desenvolvedor.  
  
## <a name="multiple-developers"></a>Vários desenvolvedores  
 Se houver vários desenvolvedores trabalhando em uma solução de business intelligence, surgirão problemas se eles não utilizarem o modo de projeto com o controle de código-fonte na maior parte do tempo, senão integralmente. O controle de código-fonte evita que dois desenvolvedores alterem ao mesmo tempo o mesmo objeto.  
  
 Por exemplo, suponhamos que um desenvolvedor esteja trabalhando em modo de projeto e alterando os objetos selecionados. Enquanto ele faz essas alterações, outro desenvolvedor altera o banco de dados implantado em modo online. Um problema surgirá quando o primeiro desenvolvedor tentar implantar seu projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] modificado. Ou seja, o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] detectará que os objetos mudaram no banco de dados implantado e pedirá que o desenvolvedor substitua todo o banco de dados, o que eliminará as alterações feitas pelo segundo desenvolvedor. Como o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] não tem como resolver as alterações entre a instância do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e os objetos do projeto que estão prestes a serem substituídos, a única opção real do primeiro desenvolvedor será descartar suas alterações e iniciar um novo projeto com base na versão atual do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
  