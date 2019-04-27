---
title: Trabalhar com o Analysis Services, projetos e bancos de dados em um ambiente de produção | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, projects
ms.assetid: c589097f-ad29-4b97-8c7e-b8a910909c1a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 46f9cc26759470630c51cd50521f7c3705791939
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743708"
---
# <a name="working-with-analysis-services-projects-and-databases-in-a-production-environment"></a>Trabalhando com projetos e bancos de dados do Analysis Services em um ambiente de produção
  Depois de desenvolver e implantar o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a partir do seu projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você precisa decidir como deseja fazer alterações nos objetos do banco de dados implantado. Certas alterações, como aquelas relacionadas a funções de segurança, particionamento e configurações de armazenamento, podem ser feitas com o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Outras alterações podem ser feitas apenas com o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], em modo de projeto ou online (como adicionar atributos ou hierarquias definidas pelo usuário).  
  
 Assim que você alterar o banco de dados implantado do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo online, o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usado na implantação fica desatualizado. Se o desenvolvedor fizer alterações no projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e tentar implantar o projeto modificado, será informado de que ele substituirá todo o banco de dados. Se o desenvolvedor substituir o banco de dados inteiro, será necessário um processamento. Isso se tornará um grande problema se as alterações feitas pelos funcionários de produção diretamente no banco de dados implantado não tiverem sido comunicadas à equipe de desenvolvimento, pois eles não entenderão por que suas alterações não aparecem mais no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Há várias formas de usar as ferramentas do SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para evitar os problemas inerentes a essa situação.  
  
-   Método 1: Sempre que uma alteração for feita para uma versão de produção de um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] do banco de dados, use [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para criar uma nova [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto com base na versão modificada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados. Esse novo projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode ser inserido no sistema de controle do código-fonte como a cópia mestra do projeto. Esse método funcionará, independentemente de a alteração ter sido feita no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo online.  
  
-   Método 2: Só faça alterações para a versão de produção de um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] no modo de projeto. Com esse método, você pode usar as opções disponíveis no Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a fim de preservar as alterações feitas pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], como funções de segurança e configurações de armazenamento. Isso garante que as configurações relacionadas ao design serão mantidas no arquivo do projeto (configurações de armazenamento e funções de segurança podem ser ignoradas) e o servidor online será usado para configurações de armazenamento e funções de segurança.  
  
-   Método 3: Só faça alterações para a versão de produção de um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] no modo online. Como as duas ferramentas funcionam apenas com o mesmo servidor online, não há a possibilidade de se obter uma versão diferente fora de sincronia.  
  
  
