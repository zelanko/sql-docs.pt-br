---
title: Documentar e gerar scripts de um banco de dados do Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2fa4d5df2af04402ae8dc40c81ec75a72f7d8671
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208909"
---
# <a name="document-and-script-an-analysis-services-database"></a>Documentar e gerar scripts de um banco de dados do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Após a implantação de um banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gerar os metadados do banco de dados ou de um objeto contido no banco de dados, como um script XMLA. Você pode extrair esse script em uma nova janela do **Editor de Consultas XMLA** , em um arquivo ou na Área de Transferência. Para obter mais informações sobre o XMLA, consulte [Linguagem de script do Analysis Services &#40;ASSL para XMLA&#41;](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla).  
  
 O script XMLA gerado usa os elementos da Linguagem de Script do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (ASSL) para definir os objetos contidos pelo script. Se você gerou um script CREATE, o script XMLA resultante conterá um comando XMLA **Create** e elementos ASSL que poderão ser usados para criar toda a estrutura de banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma instância. Se você gerou um script ALTER, o script XMLA resultante conterá um comando XMLA **Alter** e elementos ASSL que poderão ser usados para restaurar a estrutura de um banco de dados existente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ao estado do banco de dados no momento em que o script foi criado.  
  
 Você pode usar o script XMLA gerado a partir de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de muitas maneiras, incluindo:  
  
-   Para manter um script de backup que possibilita a recriação de todos os objetos e permissões do banco de dados.  
  
-   Para criar ou atualizar o código de desenvolvimento do banco de dados.  
  
-   Para criar um ambiente de teste ou desenvolvimento a partir de um esquema existente.  
  
## <a name="see-also"></a>Consulte também  
 [Modificar ou excluir um banco de dados do Analysis Services](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)   
 [Elemento Alter &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)   
 [Elemento Create &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)  
  
  
