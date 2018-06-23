---
title: Exibir um plano de execução real | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- displaying execution plans
- actual execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 71c3239d474b6252ff36bc10fe33eb20024091b5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012034"
---
# <a name="display-an-actual-execution-plan"></a>Exibir um plano de execução real
  Este tópico descreve como gerar planos de execução gráfica reais usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Quando planos de execução reais são gerados, as consultas ou lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] são executados. O plano de execução gerado exibe o plano de execução de consulta real que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usa para executar as consultas.  
  
 Para usar esse recurso, os usuários devem ter as permissões apropriadas para executar as consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] para as quais um plano de execução gráfica está sendo gerado e eles devem ter a permissão SHOWPLAN para todos os bancos de dados referenciados pela consulta.  
  
### <a name="to-include-an-execution-plan-for-a-query-during-execution"></a>Para incluir um plano de execução para uma consulta durante a execução  
  
1.  Na barra de ferramentas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , clique em **Consulta do Mecanismo de Banco de Dados**. Você também pode abrir uma consulta existente e exibir o plano de execução estimado clicando no botão de barra de ferramentas **Abrir Arquivo** e localizando a consulta existente.  
  
2.  Insira a consulta para a qual você deseja exibir o plano de execução real.  
  
3.  No menu **Consulta** , clique em **Incluir Plano de Execução Real** ou clique no botão de barra de ferramentas **Incluir Plano de Execução Real**  
  
4.  Execute a consulta clicando no botão de barra de ferramentas **Executar** . O plano usado pelo otimizador de consulta é exibido na guia **Plano de Execução** no painel de resultados. Movimente o mouse sobre os operadores lógicos e físicos para exibir a descrição e propriedades dos operadores na dica de tela exibida.  
  
     Você também pode exibir propriedades do operador na janela Propriedades. Se a janela Propriedades não estiver visível, clique com o botão direito do mouse em um operador e selecione **Propriedades**. Selecione um operador cujas propriedades exibir.  
  
5.  Você pode alterar a exibição do plano de execução clicando com o botão direito no plano de execução e selecionando **Ampliar**, **Reduzir**, **Zoom Personalizado**ou **Ajustar Nível de Zoom**. **Ampliar** e **Reduzir** permitem ampliar ou reduzir o plano de execução, enquanto **Zoom Personalizado** permite definir seu próprio zoom, como ampliar em 80 por cento. **Ajustar Nível de Zoom** aumenta o plano de execução para se ajustar ao painel de resultados.  
  
  