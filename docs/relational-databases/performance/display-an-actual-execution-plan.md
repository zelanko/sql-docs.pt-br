---
title: Exibir um plano de execução real | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- displaying execution plans
- actual execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
caps.latest.revision: 24
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b6ae2e64f8596c9b7210f1c23a2da1f630ed4a5a
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43080528"
---
# <a name="display-an-actual-execution-plan"></a>Exibir um plano de execução real
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este tópico descreve como gerar planos de execução gráfica reais usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Os planos de execução reais são gerados depois que as consultas ou lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] são executados. Por isso, um plano de execução real contém informações de tempo de execução, como avisos de tempo de execução e métricas de uso real do recurso (se houver). O plano de execução gerado exibe o plano de execução de consulta real que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usou para executar as consultas.  
  
 Para usar esse recurso, os usuários devem ter as permissões apropriadas para executar as consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] para as quais um plano de execução gráfica está sendo gerado e eles devem ter a permissão SHOWPLAN para todos os bancos de dados referenciados pela consulta.  
  
### <a name="to-include-an-execution-plan-for-a-query-during-execution"></a>Para incluir um plano de execução para uma consulta durante a execução  
  
1.  Na barra de ferramentas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , clique em **Consulta do Mecanismo de Banco de Dados**. Você também pode abrir uma consulta existente e exibir o plano de execução estimado clicando no botão de barra de ferramentas **Abrir Arquivo** e localizando a consulta existente. 
  
2.  Insira a consulta para a qual você deseja exibir o plano de execução real.  
  
3.  No menu **Consulta** , clique em **Incluir Plano de Execução Real** ou clique no botão de barra de ferramentas **Incluir Plano de Execução Real**  
  
4.  Execute a consulta clicando no botão de barra de ferramentas **Executar** . O plano usado pelo otimizador de consulta é exibido na guia **Plano de Execução** no painel de resultados. Movimente o mouse sobre os operadores lógicos e físicos para exibir a descrição e propriedades dos operadores na dica de tela exibida.  
  
     Você também pode exibir propriedades do operador na janela Propriedades. Se a janela Propriedades não estiver visível, clique com o botão direito do mouse em um operador e selecione **Propriedades**. Selecione um operador cujas propriedades exibir.  
  
5.  Você pode alterar a exibição do plano de execução clicando com o botão direito no plano de execução e selecionando **Ampliar**, **Reduzir**, **Zoom Personalizado**ou **Ajustar Nível de Zoom**. **Ampliar** e **Reduzir** permitem ampliar ou reduzir o plano de execução, enquanto **Zoom Personalizado** permite definir seu próprio zoom, como ampliar em 80 por cento. **Ajustar Nível de Zoom** aumenta o plano de execução para se ajustar ao painel de resultados. Como alternativa, use a tecla CTRL e o botão de rolagem do mouse para ativar o **zoom dinâmico**.  
  
 
 > [!NOTE] 
 > Como alternativa, use [SET STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md) para retornar informações do plano de execução para cada instrução depois de executá-las. Se usada em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], a guia *Resultados* terá um link para abrir o plano de execução em formato gráfico.   
