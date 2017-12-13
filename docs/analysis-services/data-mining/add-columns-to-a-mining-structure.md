---
title: "Adicionar colunas a uma estrutura de mineração | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], columns
- columns [data mining], mining structure columns
- adding columns
ms.assetid: 3f879344-9f66-4178-851a-e8c5ccccf4cb
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 095d9ad73f983f38c1d702c18f7391be045e63e9
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="add-columns-to-a-mining-structure"></a>Adicionar colunas a uma estrutura de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Use o Designer de mineração de dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] adicionar colunas a uma estrutura de mineração depois que você definiu no Assistente de mineração de dados. É possível adicionar qualquer coluna existente na exibição de fonte de dados que foi usada para definir a estrutura de mineração.  
  
> [!NOTE]  
>  Você pode adicionar várias cópias de colunas em uma estrutura de mineração, porém deve evitar o uso de mais de uma instância da coluna dentro do mesmo modelo, a fim de impedir correlações falsas entre a coluna de origem e a coluna derivada.  
  
### <a name="to-add-a-column-to-a-mining-structure"></a>Para adicionar uma coluna a uma estrutura de mineração  
  
1.  Selecione a guia **Estrutura de Mineração** no Designer de Mineração de Dados.  
  
2.  Clique com o botão direito do mouse na estrutura de mineração e selecione **Adicionar uma Coluna**.  
  
     A caixa de diálogo **Selecionar uma Coluna** é exibida.  
  
3.  Em **Tabela de Origem**, selecione a tabela na exibição de fonte de dados em que reside a coluna.  
  
4.  Em **Coluna de origem**, selecione a coluna que você quer adicionar à estrutura de mineração.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Se você adicionar uma coluna existente, uma cópia será incluída na estrutura, e o nome anexado com um "1". Você pode alterar o nome da coluna copiada para algo mais descritivo digitando um novo nome na propriedade **Nome** da coluna da estrutura de mineração.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções da estrutura de mineração](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
