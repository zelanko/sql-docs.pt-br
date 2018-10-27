---
title: Documentar e gerar scripts de um banco de dados do Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- XML for Analysis, scripts
- XMLA, scripts
- scripts [Analysis Services], databases
- documenting databases
- databases [Analysis Services], documenting
- databases [Analysis Services], scripts
ms.assetid: 125044e2-8d36-4733-8743-8bb68ff9aa4e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a1a10d27612d127bcc9fcc5ca60f97575f6fc1fe
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50144683"
---
# <a name="document-and-script-an-analysis-services-database"></a>Documentar e gerar scripts de um banco de dados do Analysis Services
  Após a implantação de um banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gerar os metadados do banco de dados ou de um objeto contido no banco de dados, como um script XMLA. Você pode extrair esse script em uma nova janela do **Editor de Consultas XMLA** , em um arquivo ou na Área de Transferência. Para obter mais informações sobre o XMLA, consulte [Analysis Services Scripting Language &#40;ASSL&#41; referência](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla).  
  
 O script XMLA gerado usa os elementos da Linguagem de Script do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (ASSL) para definir os objetos contidos pelo script. Se você gerou um script CREATE, o script XMLA resultante conterá um comando XMLA **Create** e elementos ASSL que poderão ser usados para criar toda a estrutura de banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma instância. Se você gerou um script ALTER, o script XMLA resultante conterá um comando XMLA **Alter** e elementos ASSL que poderão ser usados para restaurar a estrutura de um banco de dados existente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ao estado do banco de dados no momento em que o script foi criado.  
  
 Você pode usar o script XMLA gerado a partir de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de muitas maneiras, incluindo:  
  
-   Para manter um script de backup que possibilita a recriação de todos os objetos e permissões do banco de dados.  
  
-   Para criar ou atualizar o código de desenvolvimento do banco de dados.  
  
-   Para criar um ambiente de teste ou desenvolvimento a partir de um esquema existente.  
  
## <a name="see-also"></a>Consulte também  
 [Modificar ou excluir um banco de dados do Analysis Services](modify-or-delete-an-analysis-services-database.md)   
 [Elemento Alter &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)   
 [Elemento Create &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)  
  
  
