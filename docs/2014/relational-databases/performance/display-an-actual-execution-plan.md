---
title: Exibir um plano de execução real | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- displaying execution plans
- actual execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9403e6e2cf1c341780a06bbdff1c5f38685dd34a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63150976"
---
# <a name="display-an-actual-execution-plan"></a>Exibir um plano de execução real
  Este tópico descreve como gerar planos de execução gráfica reais usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Quando planos de execução reais são gerados, as consultas ou lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] são executados. O plano de execução gerado exibe o plano de execução de consulta real que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usa para executar as consultas.  
  
 Para usar esse recurso, os usuários devem ter as permissões apropriadas para executar as consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] para as quais um plano de execução gráfica está sendo gerado e eles devem ter a permissão SHOWPLAN para todos os bancos de dados referenciados pela consulta.  
  
### <a name="to-include-an-execution-plan-for-a-query-during-execution"></a>Para incluir um plano de execução para uma consulta durante a execução  
  
1.  Na barra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] de ferramentas, clique em **mecanismo de banco de dados consulta**. Você também pode abrir uma consulta existente e exibir o plano de execução estimado clicando no botão de barra de ferramentas **Abrir Arquivo** e localizando a consulta existente.  
  
2.  Insira a consulta para a qual você deseja exibir o plano de execução real.  
  
3.  No menu **consulta** , clique em **incluir plano de execução real** ou clique no botão de barra de ferramentas **incluir plano de execução real**  
  
4.  Execute a consulta clicando no botão de barra de ferramentas **Executar** . O plano usado pelo otimizador de consulta é exibido na guia **Plano de Execução** no painel de resultados. Movimente o mouse sobre os operadores lógicos e físicos para exibir a descrição e propriedades dos operadores na dica de tela exibida.  
  
     Você também pode exibir propriedades do operador na janela Propriedades. Se a janela Propriedades não estiver visível, clique com o botão direito do mouse em um operador e selecione **Propriedades**. Selecione um operador cujas propriedades exibir.  
  
5.  Você pode alterar a exibição do plano de execução clicando com o botão direito no plano de execução e selecionando **Ampliar**, **Reduzir**, **Zoom Personalizado**ou **Ajustar Nível de Zoom**. **Ampliar** e **reduzir** permite que você Amplie ou reduza o plano de execução, enquanto o **zoom personalizado** permite que você defina seu próprio zoom, como o zoom em 80%. **Zoom para ajustar** amplia o plano de execução para se ajustar ao painel de resultados.  
  
  
