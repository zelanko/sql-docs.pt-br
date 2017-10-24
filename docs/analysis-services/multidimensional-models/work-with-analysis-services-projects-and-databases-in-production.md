---
title: "Trabalhar com projetos e bancos de dados de produção do Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services, projects
ms.assetid: c589097f-ad29-4b97-8c7e-b8a910909c1a
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 027e9cfb4f69cbdb89d776b80916afa8ac89eb69
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="work-with-analysis-services-projects-and-databases-in-production"></a>Trabalhar com projetos e bancos de dados de produção do Analysis Services
  Depois de desenvolver e implantar o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a partir do seu projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você precisa decidir como deseja fazer alterações nos objetos do banco de dados implantado. Certas alterações, como aquelas relacionadas a funções de segurança, particionamento e configurações de armazenamento, podem ser feitas com o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Outras alterações podem ser feitas apenas com o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], em modo de projeto ou online (como adicionar atributos ou hierarquias definidas pelo usuário).  
  
 Assim que você alterar o banco de dados implantado do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo online, o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usado na implantação fica desatualizado. Se o desenvolvedor fizer alterações no projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e tentar implantar o projeto modificado, será informado de que ele substituirá todo o banco de dados. Se o desenvolvedor substituir o banco de dados inteiro, será necessário um processamento. Isso se tornará um grande problema se as alterações feitas pelos funcionários de produção diretamente no banco de dados implantado não tiverem sido comunicadas à equipe de desenvolvimento, pois eles não entenderão por que suas alterações não aparecem mais no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Há várias formas de usar as ferramentas do SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para evitar os problemas inerentes a essa situação.  
  
-   Método 1: sempre que for feita uma alteração em uma versão de produção de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , use o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para criar um novo projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] com base na versão modificada do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Esse novo projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode ser inserido no sistema de controle do código-fonte como a cópia mestra do projeto. Esse método funcionará, independentemente de a alteração ter sido feita no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo online.  
  
-   Método 2: fazer alterações na versão de produção de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] somente usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo de projeto. Com esse método, você pode usar as opções disponíveis no Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a fim de preservar as alterações feitas pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], como funções de segurança e configurações de armazenamento. Isso garante que as configurações relacionadas ao design serão mantidas no arquivo do projeto (configurações de armazenamento e funções de segurança podem ser ignoradas) e o servidor online será usado para configurações de armazenamento e funções de segurança.  
  
-   Método 3: fazer alterações na versão de produção de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] somente usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] no modo online. Como as duas ferramentas funcionam apenas com o mesmo servidor online, não há a possibilidade de se obter uma versão diferente fora de sincronia.  
  
  

