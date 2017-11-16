---
title: "Salvar eventos do plano de execução XML separadamente (SQL Server Profiler) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Showplan XML events
- saving Showplan XML events
- events [SQL Server], Showplan XML
ms.assetid: 33320a7a-36e8-401c-876d-5b82c49abd85
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6dc6f5b52c0634e4ec2163a7069e0fbcbe13f314
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="save-showplan-xml-events-separately-sql-server-profiler"></a>Salvar eventos de Plano de Execução XML separadamente (SQL Server Profiler)
  Esse tópico descreve como salvar eventos **Showplan XML** capturados nos rastreamentos em arquivos .SQLPlan separados, por meio do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Você pode abrir os arquivos de eventos **Showplan XML** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o que permite visualizar o plano de execução gráfico de cada evento.  
  
### <a name="to-save-showplan-xml-events-separately"></a>Para salvar eventos de Plano de Execução XML separadamente  
  
1.  No menu **Arquivo** , clique em **Novo Rastreamento**e conecte a uma instância do SQL Server.  
  
     A caixa de diálogo **Propriedades do Rastreamento**é exibida.  
  
    > [!NOTE]  
    >  Se **Iniciar rastreamento imediatamente após estabelecer a conexão**estiver selecionado, a caixa de diálogo **Propriedades do Rastreamento**não será exibida e o rastreamento será iniciado. Para desabilitar essa configuração, no menu **Ferramentas**, clique em **Opções**e desmarque a caixa de seleção **Iniciar rastreamento imediatamente após estabelecer a conexão** .  
  
2.  Na caixa de diálogo **Propriedades do Rastreamento** , digite um nome para o rastreamento na caixa **Nome do rastreamento** .  
  
3.  Na lista **Usar o modelo** , selecione um modelo como base para o rastreamento ou **Em branco** , se não quiser usar um modelo.  
  
4.  Siga um destes procedimentos:  
  
    -   Marque a caixa de seleção**Salvar em arquivo** para capturar o rastreamento em um arquivo. Especifique um valor para **Definir tamanho máximo do arquivo**. Opcionalmente, marque as caixas de seleção **Habilitar substituição de arquivo** e **Dados de rastreamento de processos do servidor** .  
  
    -   Marque a caixa de seleção**Salvar em tabela** para capturar o rastreamento em uma tabela de banco de dados. Opcionalmente, clique em **Definir máximo de linhas**e especifique um valor.  
  
5.  Opcionalmente, marque a caixa de seleção **Habilitar horário de parada do rastreamento** e especifique uma data e hora de parada.  
  
6.  Clique na guia **Seleção de Eventos**.  
  
7.  Na caixa de diálogo **Eventos**, expanda a categoria de evento **Performance**e marque a caixa de seleção **Showplan XML**. Se a categoria de evento **Performance** não estiver disponível, marque **Mostrar todos os eventos** para exibi-la.  
  
     A caixa de diálogo **Configurações de Extração de Eventos**é adicionada à caixa de diálogo **Propriedades do Rastreamento**.  
  
8.  No menu **Configurações de Extração de Eventos**, clique em **Salvar eventos de Plano de Execução XML separadamente**.  
  
9. Na caixa de diálogo **Salvar como** , digite um nome para o arquivo no qual armazenar os eventos **Showplan XML** .  
  
10. Clique em **Todos os lotes de Plano de Execução XML em um único arquivo** para salvar todos os eventos **Showplan XML** em um único arquivo XML ou clique em **Cada lote de Plano de Execução XML em um arquivo distinto**para criar um novo arquivo XML para cada evento **Showplan XML** .  
  
11. Para visualizar o arquivo do evento **Showplan XML** no SQL Server Management Studio, no menu **Arquivo** , aponte para **Abrir**e clique em **Arquivo**. Navegue até o diretório em que você salvou o arquivo (ou arquivos) de evento **Showplan XML** para selecioná-lo e abri-lo. Os arquivos de evento**Showplan XML** têm a extensão .SQLPlan.  
  
## <a name="see-also"></a>Consulte também  
 [Analisar consultas com resultados do Plano de Execução no SQL Server Profiler](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  
