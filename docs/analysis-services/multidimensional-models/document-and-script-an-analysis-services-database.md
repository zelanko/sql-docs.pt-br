---
title: Documentar e gerar scripts de um banco de dados do Analysis Services | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML for Analysis, scripts
- XMLA, scripts
- scripts [Analysis Services], databases
- documenting databases
- databases [Analysis Services], documenting
- databases [Analysis Services], scripts
ms.assetid: 125044e2-8d36-4733-8743-8bb68ff9aa4e
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ba1f7a1a969b055261f5b32955b18ad83941e3c9
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="document-and-script-an-analysis-services-database"></a>Documentar e gerar scripts de um banco de dados do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Após a implantação de um banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gerar os metadados do banco de dados ou de um objeto contido no banco de dados, como um script XMLA. Você pode extrair esse script em uma nova janela do **Editor de Consultas XMLA** , em um arquivo ou na Área de Transferência. Para obter mais informações sobre o XMLA, consulte [Linguagem de script do Analysis Services &#40;ASSL para XMLA&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).  
  
 O script XMLA gerado usa os elementos da Linguagem de Script do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (ASSL) para definir os objetos contidos pelo script. Se você gerou um script CREATE, o script XMLA resultante conterá um comando XMLA **Create** e elementos ASSL que poderão ser usados para criar toda a estrutura de banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma instância. Se você gerou um script ALTER, o script XMLA resultante conterá um comando XMLA **Alter** e elementos ASSL que poderão ser usados para restaurar a estrutura de um banco de dados existente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ao estado do banco de dados no momento em que o script foi criado.  
  
 Você pode usar o script XMLA gerado a partir de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de muitas maneiras, incluindo:  
  
-   Para manter um script de backup que possibilita a recriação de todos os objetos e permissões do banco de dados.  
  
-   Para criar ou atualizar o código de desenvolvimento do banco de dados.  
  
-   Para criar um ambiente de teste ou desenvolvimento a partir de um esquema existente.  
  
## <a name="see-also"></a>Consulte também  
 [Modificar ou excluir um banco de dados do Analysis Services](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)   
 [Alterar o elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)   
 [Criar elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)  
  
  
