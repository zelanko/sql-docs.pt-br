---
title: Implantar o PowerPivot e Power View - Farm multicamadas do SharePoint 2016 | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e36a632-0750-4247-92b6-1fe38c7a4ce2
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: da59f6eddb113c8af70e3ddcf3bcb3f35d6a6123
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="deploy-powerpivot-and-power-view---multi-tier-sharepoint-2016-farm"></a>Implantar o PowerPivot e Power View - Farm multicamadas do SharePoint 2016
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  **Resumo:** este white paper fornece aos administradores e arquitetos do SharePoint instruções passo a passo detalhadas para implantar e configurar um ambiente de demonstração de BI da Microsoft em um farm do SharePoint com vários servidores, com base em versões de Preview do SharePoint Server 2016, Servidor do Office Online e a pilha de BI do SQL Server 2016 para SharePoint 2016. A seguir uma breve introdução às importantes alterações de arquitetura e dependências correspondentes do sistema, descreve os requisitos de configuração e de software e um caminho de implantação recomendada para habilitar e verificar os recursos de BI em três etapas principais. Este white paper também aborda problemas conhecidos que existem nas versões SharePoint Server 2016 Beta 2, visualização do servidor online do Office e SQL Server 2016 CTP 3.1 e sugere soluções alternativas apropriadas. Essas soluções alternativas não serão mais necessárias as nas versões finais dos produtos. Procure uma versão atualizada deste white paper ao implantar versões de RTM.  
  
 **Autor:**Kay Unkroth, Jason Haak  
  
 **Revisores técnicos:** Adam Saxton, Anne Zorner, Craig Guyer, Frank Weigel, Gregory Appel, Heidi Steen, Kasper de Jonge, Kirk Stark, Klaus Sobel, Mike Plumley, Mike Taghizadeh, Patrick Wheeler, Riccardo Muti e Steve Hord  
  
 **Publicado:**janeiro de 2016  
  
 **Aplica-se a:** SQL Server 2016 CTP3.1, visualização do SharePoint 2016 e do Servidor do Office Online  
  
 Para examinar o documento, baixe o documento do Word [Implantando o SQL Server 2016 PowerPivot e Power View em um farm multicamadas do SharePoint 2016](http://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/Deploying%20SQL%20Server%202016%20PowerPivot%20and%20Power%20View%20in%20a%20Multi-Tier%20SharePoint%202016%20Farm.docx) .  
  
  
