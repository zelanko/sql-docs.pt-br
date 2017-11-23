---
title: "Exibir ou alterar sinalizadores de modelagem (mineração de dados) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
ms.assetid: d1169735-fb18-417b-b8d6-9a161e444020
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 98ec1ace5b819a123fd4a8949c92caa5e3be4e5f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="view-or-change-modeling-flags-data-mining"></a>Exibir ou alterar sinalizadores de modelagem (mineração de dados)
  Sinalizadores de modelagem são propriedades que você define em uma coluna da estrutura de mineração ou em colunas do modelo de mineração para controlar como o algoritmo processa os dados durante a análise.  
  
 No Designer de Mineração de Dados, é possível exibir e modificar os sinalizadores de modelagem associados a uma estrutura ou a uma coluna de mineração ao exibir as propriedades do modelo ou da estrutura de mineração. Você também pode definir sinalizadores de modelagem usando DMX, AMO ou XMLA.  
  
 Este procedimento descreve como alterar os sinalizadores de modelagem no designer.  
  
### <a name="view-or-change-the-modeling-flag-for-a-structure-column-or-model-column"></a>Exibir ou alterar o sinalizador de modelagem de uma coluna de estrutura ou de modelo  
  
1.  No SQL Server Design Estúdio, abra o Gerenciador de Soluções e clique duas vezes na estrutura de mineração.  
  
2.  Para definir o sinalizador de modelagem NOT NULL, clique na guia **Estrutura de Mineração** . Para definir os sinalizadores REGRESSOR ou MODEL_EXISTENCE_ONLY, clique na guia **Modelo de Mineração** .  
  
3.  Clique com o botão direito do mouse na coluna que você deseja exibir ou alterar e selecione **Propriedades**.  
  
4.  Para adicionar um novo sinalizador de modelagem, clique na caixa de texto próxima de propriedade **ModelingFlags** e marque as caixas de seleção referentes aos sinalizadores de modelagem que você deseja usar.  
  
     Serão exibidos apenas os sinalizadores de modelagem apropriados para o tipo de dados da coluna.  
  
    > [!NOTE]  
    >  Depois de alterar um sinalizador de modelagem, processe novamente o modelo.  
  
### <a name="get-the-modeling-flags-used-in-the-model"></a>Obter os sinalizadores de modelagem usados no modelo  
  
-   No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra uma janela da Consulta DMX e digite uma consulta como o seguinte:  
  
    ```  
    SELECT COLUMN_NAME, CONTENT_TYPE, MODELING_FLAG  
    FROM $system.DMSCHEMA_MINING_COLUMNS  
    WHERE MODEL_NAME = 'Forecasting'  
  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Sinalizadores de modelagem &#40;Mineração de dados&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
  
