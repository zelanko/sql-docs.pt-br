---
title: Correlacionar um rastreamento com os dados de log de desempenho do Windows (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], logs
ms.assetid: e1b3072c-8daf-49a7-9895-c8cccd2adb95
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2d1b66cbbed716a4ce7b2d5cf9611e161141f162
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934573"
---
# <a name="correlate-a-trace-with-windows-performance-log-data-sql-server-profiler"></a>Correlacionar um rastreamento com dados do log de desempenho do Windows (SQL Server Profiler)
  [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]pode correlacionar contadores do monitor do sistema do Microsoft Windows a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] eventos ou. O Monitor do Sistema do Windows registra a atividade do sistema em logs de desempenho para os contadores especificados.  
  
> [!NOTE]  
>  Para obter informações sobre como compartilhar logs entre versões diferentes do Windows, consulte o procedimento ao final desse tópico.  
  
### <a name="to-correlate-a-trace-with-performance-log-data"></a>Para correlacionar um rastreamento com dados do log de desempenho  
  
1.  No [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], abra uma tabela ou arquivo de rastreamento salvo. Não é possível correlacionar um rastreamento em execução que ainda está coletando dados de evento. Para correlação precisa com os dados do Monitor do Sistema, o rastreamento deve conter as colunas de dados **StartTime** e **EndTime** .  
  
2.  No menu  **Arquivo** do [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], clique em **Importar Dados de Desempenho**.  
  
3.  Na caixa de diálogo **Abrir** , selecione um arquivo que contenha um log de desempenho. Os dados do log de desempenho devem ter sido capturados durante o mesmo período de tempo que os dados do rastreamento.  
  
4.  Na caixa de diálogo **Limite de Contadores de Desempenho** , marque as caixas de seleção que correspondem aos objetos e contadores do Monitor do Sistema que você deseja exibir junto com o rastreamento. Clique em **OK**  
  
5.  Na janela de eventos de rastreamento, selecione um evento ou navegue pelas linhas adjacentes usando as teclas de direção. A barra vertical vermelha na janela **Dados do Monitor do Sistema** indica os dados do log de desempenho correlacionados com o evento de rastreamento selecionado.  
  
6.  Clique em um ponto de interesse no gráfico do Monitor do Sistema. É selecionada a linha de rastreamento correspondente ao horário mais próximo. Para aumentar o zoom sobre um intervalo de tempo, pressione e arraste o ponteiro do mouse no gráfico do Monitor do Sistema.  
  
### <a name="to-create-performance-logs-that-can-be-shared-among-different-versions-of-windows"></a>Para criar logs de desempenho que possam ser compartilhados entre versões diferentes do Windows  
  
1.  No Painel de Controle, abra **Ferramentas Administrativas**e clique duas vezes em **Desempenho**.  
  
2.  Na caixa de diálogo **Desempenho** , expanda **Logs e Alertas de Desempenho**, clique com o botão direito do mouse em **Logs do Contador**e clique em **Novas Configurações de Log**.  
  
3.  Digite um nome para o log do contador e clique em **OK**.  
  
4.  Na guia **Geral** , clique em **Adicionar Contadores**.  
  
5.  Na lista **Objeto de Desempenho** , selecione o objeto de desempenho a monitorar. Os nomes dos objetos de desempenho do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para instâncias padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] começam com [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e as instâncias nomeadas começam com MSSQL$*instanceName*.  
  
6.  Adicione quantos contadores forem necessários para a sua instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e outros valores importantes, como tempo de processador e tempo de disco.  
  
7.  Quando terminar de adicionar contadores, clique em **Fechar**.  
  
8.  Defina valores para o intervalo **Amostrar dados a cada** . Comece com um intervalo de amostragem modesto, como 5 minutos e depois ajuste o intervalo, se necessário.  
  
9. Na guia **Arquivos de Log** , escolha **Arquivo de Texto (delimitado por vírgula)** na lista **Tipo de arquivo de log** . Os arquivos de log de texto delimitados por vírgula podem ser compartilhados entre versões diferentes do Windows, bem como ser visualizados mais tarde, em ferramentas de relatório como o Microsoft Excel.  
  
10. Na guia **Agenda** , especifique uma agenda de monitoramento.  
  
11. Clique em **OK** para criar o log de desempenho.  
  
## <a name="see-also"></a>Consulte Também  
 [Modelos e permissões do SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [Iniciar o SQL Server Profiler](../tools/sql-server-profiler/start-sql-server-profiler.md)  
  
  
