---
title: Correlacionar um rastreamento com os dados de log de desempenho do Windows | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- correlating trace with log data
- logs [SQL Server], traces
- Profiler [SQL Server Profiler], correlating trace with log data
- traces [SQL Server], logs
- SQL Server Profiler, correlating trace with log data
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bdbd634a74c5e7cd48232a28ab4c7709e8febfad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63033754"
---
# <a name="correlate-a-trace-with-windows-performance-log-data"></a>Correlacionar um rastreamento com os dados de log de desempenho do Windows
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], você pode abrir um log de desempenho do Microsoft Windows, escolher os contadores que deseja correlacionar com um rastreamento e exibir os contadores de desempenho selecionados junto com o rastreamento na interface gráfica do usuário do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] . Quando você seleciona um evento na janela de rastreamento, uma barra vermelha vertical no painel da janela de dados do Monitor do Sistema do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] indica os dados do log de desempenho que se correlacionam com o evento de rastreamento selecionado.  
  
 Para correlacionar um rastreamento com contadores de desempenho, abra um arquivo ou tabela de rastreamento que contenha as colunas de dados **StartTime** e **EndTime** data columns, e then click **Importar Dados de Desempenho** no menu [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **File** menu. Em seguida, você pode abrir um log de desempenho e selecionar os objetos e contadores do Monitor do Sistema que deseja correlacionar com o rastreamento.  
  
### <a name="to-correlate-a-trace-with-performance-log-data"></a>Para correlacionar um rastreamento com dados do log de desempenho  
  
1.  No [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], abra uma tabela ou arquivo de rastreamento salvo. Não é possível correlacionar um rastreamento em execução que ainda está coletando dados de evento. Para correlação precisa com os dados do Monitor do Sistema, o rastreamento deve conter as colunas de dados **StartTime** e **EndTime** .  
  
2.  No menu [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **File** menu, click **Import Performance Data**.  
  
3.  Na caixa de diálogo **Abrir** , selecione um arquivo que contenha um log de desempenho. Os dados do log de desempenho devem ter sido capturados durante o mesmo período de tempo que os dados do rastreamento.  
  
4.  Na caixa de diálogo **Limite de Contadores de Desempenho** , marque as caixas de seleção que correspondem aos objetos e contadores do Monitor do Sistema que você deseja exibir junto com o rastreamento. Clique em **OK.**  
  
5.  Na janela de eventos de rastreamento, selecione um evento ou navegue pelas linhas adjacentes usando as teclas de direção. A barra vertical vermelha na janela **Dados do Monitor do Sistema** indica os dados do log de desempenho correlacionados com o evento de rastreamento selecionado.  
  
6.  Clique em um ponto de interesse no gráfico do Monitor do Sistema. É selecionada a linha de rastreamento correspondente ao horário mais próximo. Para aumentar o zoom sobre um intervalo de tempo, pressione e arraste o ponteiro do mouse no gráfico do Monitor do Sistema.  
  
### <a name="to-create-performance-logs-that-can-be-shared-among-different-versions-of-windows"></a>Para criar logs de desempenho que possam ser compartilhados entre versões diferentes do Windows  
  
1.  No Painel de Controle, abra **Ferramentas Administrativas**e clique duas vezes em **Desempenho**.  
  
2.  Na caixa de diálogo **Desempenho** , expanda **Logs e Alertas de Desempenho**, clique com o botão direito do mouse em **Logs do Contador**e clique em **Novas Configurações de Log**.  
  
3.  Digite um nome para o log do contador e clique em **OK**.  
  
4.  Na guia **Geral** , clique em **Adicionar Contadores**.  
  
5.  Na lista **Objeto de Desempenho** , selecione o objeto de desempenho a monitorar. Os nomes dos objetos de desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instâncias padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] começam com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as instâncias nomeadas começam com MSSQL$*instanceName*.  
  
6.  Adicione quantos contadores forem necessários para a sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e outros valores importantes, como tempo de processador e tempo de disco.  
  
7.  Quando terminar de adicionar contadores, clique em **Fechar**.  
  
8.  Defina valores para o intervalo **Amostrar dados a cada** . Comece com um intervalo de amostragem modesto, como 5 minutos e depois ajuste o intervalo, se necessário.  
  
9. Na guia **Arquivos de Log** , escolha **Arquivo de Texto (delimitado por vírgula)** na lista **Tipo de arquivo de log** . Os arquivos de log de texto delimitados por vírgula podem ser compartilhados entre versões diferentes do Windows, bem como ser visualizados mais tarde, em ferramentas de relatório como o Microsoft Excel.  
  
10. Na guia **Agenda** , especifique uma agenda de monitoramento.  
  
11. Clique em **OK** para criar o log de desempenho.  
