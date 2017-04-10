---
title: "Salvar eventos de perfil de estat&#237;sticas do Plano de Execu&#231;&#227;o XML separadamente (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "eventos de Plano de Execução XML"
  - "salvando eventos de Plano de Execução XML"
  - "eventos [SQL Server], Plano de execução XML"
ms.assetid: df393f13-d538-4d94-8155-9c2fdf5f755d
caps.latest.revision: 20
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 20
---
# Salvar eventos de perfil de estat&#237;sticas do Plano de Execu&#231;&#227;o XML separadamente (SQL Server Profiler)
  Esse tópico descreve como salvar eventos **Showplan XML Statistics Profile** que são capturados nos rastreamentos em arquivos .SQLPlan separados, por meio do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Você pode abrir os arquivos de eventos **Showplan XML Statistics Profile** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o que permite ver o plano de execução gráfico de cada evento.  
  
### Para salvar eventos de estatísticas do Plano de Execução XML separadamente  
  
1.  No menu **Arquivo**, clique em **Novo Rastreamento** e conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     É exibida a caixa de diálogo **Propriedades do Rastreamento**.  
  
    > [!NOTE]  
    >  Se **Iniciar rastreamento imediatamente após estabelecer a conexão** estiver selecionado, a caixa de diálogo **Propriedades do Rastreamento** não será exibida e o rastreamento será iniciado. Para desabilitar essa configuração, no menu **Ferramentas**, clique em **Opções**e desmarque a caixa de seleção **Iniciar rastreamento imediatamente após estabelecer a conexão** .  
  
2.  Na caixa de diálogo **Propriedades do Rastreamento** , digite um nome para o rastreamento na caixa **Nome do rastreamento** .  
  
3.  Na lista **Usar o modelo**, selecione um modelo como base para o rastreamento ou **Em branco**, se não quiser usar um modelo.  
  
4.  Siga um destes procedimentos:  
  
    -   Clique em **Salvar em arquivo** para capturar o rastreamento em um arquivo. Especifique um valor para **Definir tamanho máximo do arquivo**.  
  
         Opcionalmente, selecione **Habilitar substituição de arquivo** e **Dados de rastreamento de processos do servidor**.  
  
    -   Clique em **Salvar em tabela** para capturar o rastreamento em uma tabela de banco de dados.  
  
         Opcionalmente, clique em **Definir máximo de linhas**e especifique um valor.  
  
5.  Opcionalmente, marque a caixa de seleção **Habilitar horário de parada do rastreamento** e especifique uma data e hora de parada.  
  
6.  Clique na guia **Seleção de Eventos**.  
  
7.  Na coluna de dados **Eventos**, expanda a categoria de evento **Desempenho** e marque a caixa de seleção **Showplan XML Statistics Profile**. Se a categoria de evento **Performance** não estiver disponível, marque **Mostrar todos os eventos** para exibi-la.  
  
     A guia **Configurações de Extração de Eventos**é adicionada à caixa de diálogo **Propriedades do Rastreamento**.  
  
8.  No menu **Configurações de Extração de Eventos**, clique em **Salvar eventos de Plano de Execução XML separadamente**.  
  
9. Na caixa de diálogo **alvar como**, digite o nome do arquivo para armazenar os eventos **Showplan XML Statistics Profile**.  
  
10. Clique em **Todos os lotes em um único arquivo** para salvar todos os eventos **Showplan XML Statistics Profile** em um único arquivo XML ou clique em **Cada lote de Plano de Execução XML em um arquivo distinto**para criar um novo arquivo XML para cada evento **Showplan XML Statistics Profile**.  
  
11. Para ver o arquivo do evento **Showplan XML Statistics Profile** no SQL Server Management Studio, no menu **Arquivo**, aponte para **Abrir** e clique em **Arquivo**. Navegue até o diretório em que você salvou o arquivo (ou arquivos) de evento **Showplan XML Statistics Profile** para selecioná-lo e abri-lo. Arquivos de evento **Showplan XML Statistics Profile** têm a extensão .SQLPlan.  
  
## Consulte também  
 [Analisar consultas com resultados do Plano de Execução no SQL Server Profiler](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  