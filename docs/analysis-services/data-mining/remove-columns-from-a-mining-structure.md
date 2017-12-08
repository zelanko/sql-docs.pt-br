---
title: "Remover colunas de uma estrutura de mineração | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], columns
- removing columns
- deleting columns
- columns [data mining], mining structure columns
ms.assetid: 41073ffe-9351-416b-9f0c-62634bc213f9
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d7dc82033994b08f45283bf03bcae11d441c1b60
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="remove-columns-from-a-mining-structure"></a>Remover colunas de uma estrutura de mineração
  Você pode usar o Designer de Mineração de Dados para remover colunas de uma estrutura de mineração após a criação da estrutura. Alguns motivos para remover uma coluna da estrutura de mineração:  
  
-   A estrutura de mineração contém várias cópias de uma coluna e você deseja evitar o uso de dados duplicados em um modelo.  
  
-   Os dados devem ser protegidos, mas o detalhamento foi habilitado.  
  
-   Os dados não são usados na modelagem e não devem ser processados.  
  
 A exclusão de uma coluna da estrutura de mineração não altera a coluna na exibição da fonte de dados nem nos dados externos; apenas os metadados são excluídos. Entretanto, quando você altera as colunas usadas em uma estrutura de mineração, precisa reprocessar a estrutura e quaisquer modelos com base nela.  
  
### <a name="to-remove-a-column-from-the-mining-structure"></a>Para remover colunas de uma estrutura de mineração  
  
1.  Selecione a guia **Estrutura de Mineração** no Designer de Mineração de Dados.  
  
2.  Expanda a árvore da estrutura de mineração para que mostre todas as colunas.  
  
3.  Clique com o botão direito do mouse na coluna que você quer excluir e selecione **Excluir**.  
  
4.  Na caixa de diálogo **Excluir Objetos** , clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções da estrutura de mineração](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
