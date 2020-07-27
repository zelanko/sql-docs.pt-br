---
title: Salvar gráficos de deadlock (SQL Server Profiler) | Microsoft Docs
description: Saiba como salvar um grafo de deadlock usando o SQL Server Profiler. Gráficos de deadlock são salvos como arquivos XML.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- deadlocks [SQL Server], saving deadlock graphs
- graphs [SQL Server]
- saving deadlock graphs
ms.assetid: bf1fc906-abd6-4a89-842e-da0d66b2defe
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 874597d5d62f13556072fb129931fa9e4faf1a85
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458714"
---
# <a name="save-deadlock-graphs-sql-server-profiler"></a>Salvar gráficos de deadlock (SQL Server Profiler)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como salvar um gráfico de deadlock usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Gráficos de deadlock são salvos como arquivos XML.  
  
## <a name="save-deadlock-graph-events-separately"></a>Salvar eventos de gráfico de deadlock separadamente  
  
1. No menu **Arquivo**, selecione **Novo Rastreamento** e conecte-se a uma instância do SQL Server.  
  
     É exibida a caixa de diálogo **Propriedades do Rastreamento** .  
  
    > [!NOTE]  
    >  Se você selecionar **Iniciar rastreamento imediatamente após estabelecer a conexão**, a caixa de diálogo **Propriedades do Rastreamento** não será exibida e, em vez disso, o rastreamento será iniciado. Para desligar essa configuração, no menu **Ferramentas**, selecione **Opções** e desmarque a caixa de seleção **Iniciar rastreamento imediatamente após estabelecer a conexão**.  
  
2. Na caixa de diálogo **Propriedades do Rastreamento** , digite um nome para o rastreamento na caixa **Nome do rastreamento** .  
  
3. Na lista **Usar o modelo**, selecione um modelo de rastreamento no qual esse rastreamento deve ser baseado. Se você não quiser usar um modelo, selecione **Em branco**.  
  
4. Realize um dos seguintes procedimentos:  
  
    -   Selecione a caixa de seleção **Salvar em arquivo** para capturar o rastreamento em um arquivo. Especifique um valor para **Definir tamanho máximo do arquivo**.  
  
         Opcionalmente, marque as caixas de seleção **Habilitar substituição de arquivo** e **Dados de rastreamento de processos do servidor** . 
  
    -   Marque a caixa de seleção **Salvar em tabela** para capturar o rastreamento em uma tabela de banco de dados.  
  
         Opcionalmente, selecione **Definir máximo de linhas** e especifique um valor.  
  
5. Opcionalmente, marque a caixa de seleção **Habilitar horário de parada do rastreamento** e especifique uma data e hora de parada. 
  
6. Selecione a guia **Seleção de Eventos**.  
  
7. Na coluna de dados **Eventos**, expanda a categoria de evento **Bloqueios** e marque a caixa de seleção **Gráfico de deadlock**. Se a categoria de evento **Bloqueios** não estiver disponível, marque a caixa de seleção **Mostrar todos os eventos** para exibi-la.  
  
     A guia **Configurações de Extração de Eventos** é adicionada à caixa de diálogo **Propriedades do Rastreamento**.  
  
8. Na guia **Configurações de Extração de Eventos**, clique em **Salvar eventos Deadlock XML separadamente**.  
  
9. Na caixa de diálogo **Salvar Como**, digite o nome do arquivo no qual armazenar os eventos de gráfico de deadlock.  
  
10. Selecione **Todos os lotes de Deadlock XML em um único arquivo** para salvar todos os eventos gráficos de deadlock em um único arquivo XML. Ou selecione **Cada lote de Deadlock XML em um arquivo distinto** para criar um novo arquivo XML para cada gráfico de deadlock.  
  
 Após salvar o arquivo de deadlock, você pode abri-lo no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, veja [Abrir, exibir e imprimir um arquivo de deadlock &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/open-view-and-print-a-deadlock-file-sql-server-management-studio.md).  
  
## <a name="see-also"></a>Confira também  
 [Analisar deadlocks com o SQL Server Profiler](../../tools/sql-server-profiler/analyze-deadlocks-with-sql-server-profiler.md)  
  
  
