---
title: Exibir o plano de execução estimado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- zoom [SQL Server]
- estimated execution plan [SQL Server]
- displaying execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
- customizing execution plan display [SQL Server]
- modifying execution plan display
- custom zoom [SQL Server]
ms.assetid: e94aa576-4c0c-4c54-ad05-6c3432cc615b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 555ded0e34c0dc13ce794cc6f3119af7b2688910
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150879"
---
# <a name="display-the-estimated-execution-plan"></a>Exibir o plano de execução estimado
  Este tópico descreve como gerar planos de execução gráfica estimados usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Quando são gerados planos de execução estimados, as consultas ou lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] não são executadas. Ao invés disso, o plano de execução gerado exibe o plano de execução de consulta que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] teria maior probabilidade de usar se fossem executadas consultas.  
  
 Para usar esse recurso, os usuários devem ter as permissões apropriadas para executar a consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] para as quais está sendo gerado um plano de execução gráfica e devem ter permissão SHOWPLAN para todos os bancos de dados incluídos na consulta.  
  
### <a name="to-display-the-estimated-execution-plan-for-a-query"></a>Para exibir o plano de execução estimado para uma consulta  
  
1.  Na barra de ferramentas, clique em **Consulta do Mecanismo de Banco de Dados**. Você também pode abrir uma consulta existente e exibir o plano de execução estimado clicando no botão de barra de ferramentas **Abrir Arquivo** e localizando a consulta existente.  
  
2.  Insira a consulta para a qual você deseja exibir o plano de execução estimado.  
  
3.  No menu **Consulta** , clique em **Exibir Plano de Execução Estimado** ou clique no botão de barra de ferramentas **Exibir Plano de Execução Estimado** . O plano de execução estimado é exibido na guia **Plano de execução** no painel de resultados. Para exibir mais informações, mantenha o mouse sobre os ícones dos operadores lógicos e físicos e exiba a dica de tela com a descrição e as propriedades do operador. Você também pode exibir propriedades do operador na janela Propriedades. Se a janela Propriedades não estiver visível, clique com o botão direito do mouse em um operador e clique em **Propriedades**. Selecione um operador cujas propriedades exibir.  
  
4.  Para alterar a exibição do plano de execução, clique com o botão direito do mouse no plano de execução e selecione **Ampliar**, **Reduzir**, **Zoom Personalizado**ou **Ajustar Nível de Zoom**. **Ampliar** e **Reduzir** permitem ampliar ou reduzir o plano de execução com valores fixos. **Zoom personalizado** permite que você defina sua própria ampliação da exibição, como ampliar em 80 por cento. **Ajustar Nível de Zoom** aumenta o plano de execução para se ajustar ao painel de resultados.  
  
  
