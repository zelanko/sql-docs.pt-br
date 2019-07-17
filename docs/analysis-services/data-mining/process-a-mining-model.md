---
title: Processar um modelo de mineração | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2bfc8d22ff87f467fa89d178d46b422918aa4dd6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209735"
---
# <a name="process-a-mining-model"></a>Processar um modelo de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Na guia Modelos de Mineração do Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você pode processar um modelo de mineração específico que está associado a uma estrutura de mineração ou processar todos os modelos que estão associados com a estrutura.  
  
 É possível processar um modelo de mineração usando as seguintes ferramentas:  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
 Você também pode usar um comando do processo XMLA. Para obter mais informações, consulte [Ferramentas e abordagens para processamento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md).  
  
### <a name="process-a-single-mining-model-using-sql-server-data-tools"></a>Processar um único modelo de mineração usando as Ferramentas de Dados do SQL Server  
  
1.  Na guia **Modelos de Mineração** do Designer de Mineração de Dados, selecione um modelo de mineração de uma ou mais colunas de modelos na grade.  
  
2.  No menu **Modelo de Mineração** , selecione **Processar Modelo**.  
  
     Caso faça uma alteração na estrutura de mineração, você receberá uma solicitação para implantar a estrutura novamente antes de processar o modelo. Clique em **Sim**.  
  
3.  No **processando modelo de mineração - \<modelo >** caixa de diálogo, clique em **executar**.  
  
     A caixa de diálogo **Andamento do Processo** é aberta e exibe os detalhes sobre o processamento do modelo.  
  
4.  Clique em **Fechar** na caixa de diálogo **Andamento do Processo** , após o modelo completar seu processamento.  
  
5.  Clique em **feche** na **processando modelo de mineração - \<modelo >** caixa de diálogo.  
  
 Só foram processados a estrutura de mineração e o modelo de mineração selecionado.  
  
### <a name="process-all-mining-models-that-are-associated-with-a-mining-structure"></a>Processar todos os modelos de mineração que estão associados com uma estrutura de mineração  
  
1.  Na guia **Modelos de Mineração** do Designer de Mineração de Dados, selecione **Processar Estrutura de Mineração e Todos os Modelos** a partir do menu **Modelo de Mineração** .  
  
2.  Caso faça alterações na estrutura de mineração, você receberá uma solicitação para implantar a estrutura novamente antes de processar os modelos. Clique em **Sim**.  
  
3.  No **processando estrutura de mineração - \<estrutura >** caixa de diálogo, clique em **executar**.  
  
4.  A caixa de diálogo **Andamento do Processo** é aberta e exibe os detalhes sobre o processamento do modelo.  
  
5.  Clique em **Fechar** na caixa de diálogo **Andamento do Processo** , após os modelos completarem seu processamento.  
  
6.  Clique em **feche** na **processamento \<modelo >** caixa de diálogo.  
  
 A estrutura de mineração e todos os modelos de mineração associados foram processados.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
