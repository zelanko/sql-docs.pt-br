---
title: Salvar gráficos de deadlock (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- deadlocks [SQL Server], saving deadlock graphs
- graphs [SQL Server]
- saving deadlock graphs
ms.assetid: bf1fc906-abd6-4a89-842e-da0d66b2defe
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 352bbfd96fcf3d70d6bce07ce520c4ee1333c51d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37268822"
---
# <a name="save-deadlock-graphs-sql-server-profiler"></a>Salvar gráficos de deadlock (SQL Server Profiler)
  Este tópico descreve como salvar um gráfico de deadlock usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Gráficos de deadlock são salvos como arquivos XML.  
  
### <a name="to-save-deadlock-graph-events-separately"></a>Para salvar eventos de gráfico de deadlock separadamente  
  
1.  No menu **Arquivo** , clique em **Novo Rastreamento**e conecte a uma instância do SQL Server.  
  
     A caixa de diálogo **Propriedades do Rastreamento**é exibida.  
  
    > [!NOTE]  
    >  Se a opção **Iniciar rastreamento imediatamente após estabelecer a conexão** estiver marcada, a caixa de diálogo **Propriedades do Rastreamento**não será exibida e o rastreamento será iniciado. Para desabilitar essa configuração, no menu **Ferramentas**, clique em **Opções**e desmarque a caixa de seleção **Iniciar rastreamento imediatamente após estabelecer a conexão** .  
  
2.  Na caixa de diálogo Propriedades do Rastreamento, digite um nome para o rastreamento na caixa**Nome do rastreamento** .  
  
3.  Na lista **Usar o modelo** , selecione um modelo como base para o rastreamento ou **Em branco** , se não quiser usar um modelo.  
  
4.  Siga um destes procedimentos:  
  
    -   Marque a caixa de seleção**Salvar em arquivo** para capturar o rastreamento em um arquivo. Especifique um valor para **Definir tamanho máximo do arquivo**.  
  
         Opcionalmente, selecione **Habilitar substituição de arquivo** e **Dados de rastreamento de processos do servidor**.  
  
    -   Marque a caixa de seleção **Salvar em tabela** para capturar o rastreamento em uma tabela de banco de dados.  
  
         Opcionalmente, clique em **Definir máximo de linhas**e especifique um valor.  
  
5.  Opcionalmente, marque a caixa de seleção **Habilitar horário de parada do rastreamento** e especifique uma data e hora de parada.  
  
6.  Clique na guia **Seleção de Eventos**.  
  
7.  Na coluna de dados **Eventos**, expanda a categoria de evento **Locks**e marque a caixa de seleção **Gráfico de deadlock**. Se a categoria de evento Locks não estiver disponível, marque **Mostrar todos os eventos** para exibi-la.  
  
     A caixa de diálogo **Configurações de Extração de Eventos**é adicionada à caixa de diálogo **Propriedades do Rastreamento**.  
  
8.  Na guia **Configurações de Extração de Eventos**, clique em **Salvar eventos deadlock XML separadamente**.  
  
9. Na caixa de diálogo **Salvar Como** , digite um nome para o arquivo no qual armazenar os eventos de gráfico de deadlock.  
  
10. Clique em **Todos os lotes de deadlock XML em um único arquivo** para salvar todos os eventos de gráfico de deadlock em um mesmo arquivo XML, ou clique em **Cada lote de deadlock XML em um arquivo distinto**, para criar um novo arquivo XML para cada gráfico de deadlock.  
  
 Após salvar o arquivo de deadlock, você pode abri-lo no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, veja [Abrir, exibir e imprimir um arquivo de deadlock &#40;SQL Server Management Studio&#41;](open-view-and-print-a-deadlock-file-sql-server-management-studio.md).  
  
## <a name="see-also"></a>Consulte também  
 [Analisar deadlocks com o SQL Server Profiler](../../tools/sql-server-profiler/analyze-deadlocks-with-sql-server-profiler.md)  
  
  
