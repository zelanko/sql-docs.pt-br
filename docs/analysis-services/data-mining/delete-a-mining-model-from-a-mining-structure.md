---
title: Excluir um modelo de mineração de uma estrutura de mineração | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 38d544972849b8de847467f5fa964f34fed3cd57
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="delete-a-mining-model-from-a-mining-structure"></a>Excluir um modelo de mineração de uma estrutura de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Você pode excluir modelos de mineração usando o Designer de Mineração de Dados, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ou instruções DMX.  
  
### <a name="delete-a-mining-model-using-sql-server-data-tools"></a>Exclua um modelo de mineração usando as Ferramentas de Dados do SQL Server  
  
1.  Selecione a guia **Modelos de Mineração** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Clique com o botão direito do mouse no modelo a ser excluído e selecione **Excluir**.  
  
     A caixa de diálogo **Excluir Objetos** é aberta.  
  
3.  Clique em **OK**.  
  
### <a name="delete-a-mining-model-using-sql-server-management-studio"></a>Exclua um modelo de mineração usando o SQL Server Management Studio  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém o modelo.  
  
2.  Expanda **Estruturas de Mineração**e, depois, **Modelos de Mineração**.  
  
3.  Clique com o botão direito do mouse no modelo a ser excluído e selecione **Excluir**.  
  
     A exclusão do modelo não leva à exclusão dos dados de treinamento, mas apenas dos metadados e de quaisquer padrões criados durante o treinamento do modelo.  
  
### <a name="delete-a-mining-model-using-dmx"></a>Excluir um modelo de mineração usando DMX  
  
-   [REMOVER MODELO DE MINERAÇÃO & #40; DMX & #41;](../../dmx/drop-mining-model-dmx.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tutoriais e tarefas do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
