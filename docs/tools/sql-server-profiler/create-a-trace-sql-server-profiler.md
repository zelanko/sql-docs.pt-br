---
title: Criar um rastreamento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], creating
ms.assetid: 0302fa6d-d2b5-43fe-ad70-7a337575b112
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9b40c4ab9616ec4d7a1271c5e3b5c1a0a36be2e7
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="create-a-trace-sql-server-profiler"></a>Criar um rastreamento (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Este tópico descreve como usar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para criar um rastreamento.  
  
### <a name="to-create-a-trace"></a>Para criar um rastreamento  
  
1.  No menu **Arquivo**, clique em **Novo Rastreamento** e conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     É exibida a caixa de diálogo **Propriedades do Rastreamento** .  
  
    > **OBSERVAÇÃO:** a caixa de diálogo **Propriedades do Rastreamento** não será exibida, e o rastreamento será iniciado, se a opção **Iniciar rastreamento imediatamente após estabelecer a conexão** for selecionada. Para desabilitar essa configuração, no **ferramentas* * menu, clique em **opções**e desmarque o iniciar rastreamento imediatamente após estabelecer a caixa de seleção da conexão.  
  
2.  Na caixa **Nome do rastreamento** , digite um nome para o rastreamento.  
  
3.  Na lista **Usar o modelo** , selecione um modelo como base para o rastreamento ou **Em branco** , se não quiser usar um modelo.  
  
4.  Para salvar os resultados do rastreamento, siga um destes procedimentos:  
  
    -   Clique em **Salvar em arquivo** para capturar o rastreamento em um arquivo. Especifique um valor para **Definir tamanho máximo do arquivo**. O valor padrão é 5 megabytes (MB).  
  
         Opcionalmente, selecione **Habilitar substituição de arquivo** para criar um novo arquivo automaticamente toda vez que o tamanho máximo for atingido. Opcionalmente, você também pode selecionar **Dados de rastreamento de processos do servidor**, o que faz com que o serviço que estiver executando o rastreamento processe os dados do rastreamento, em vez do aplicativo cliente. Quando o servidor processa dados de rastreamento, nenhum evento é ignorado, nem mesmo sob condições de estresse, mas o desempenho do servidor pode ser afetado.  
  
    -   Clique em **Salvar em tabela** para capturar o rastreamento em uma tabela de banco de dados.  
  
         Opcionalmente, clique em **Definir máximo de linhas**e especifique um valor.  
  
    > **CUIDADO!** Quando você não salva os resultados do rastreamento em um arquivo ou tabela, pode exibir o rastreamento enquanto o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] estiver aberto. No entanto, os resultados serão perdidos depois que o rastreamento for interrompido e o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] for fechado. Para evitar perder os resultados do rastreamento dessa forma, clique em **Salvar** no menu **Arquivo** para salvar os resultados antes de fechar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
5.  Opcionalmente, marque a caixa de seleção **Habilitar horário de parada do rastreamento** e especifique uma data e hora de parada.  
  
6.  Para adicionar ou remover eventos, colunas de dados ou filtros, clique na guia **Seleção de Eventos**  . Para obter mais informações, consulte: [Especificar eventos e colunas de dados para um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
7.  Clique em **Executar** para iniciar o rastreamento.  
  
## <a name="see-also"></a>Consulte também  
 [Permissões necessárias para executar o SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)   
 [Modelos e permissões do SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [Correlacionar um rastreamento com dados do log de desempenho do Windows &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  
