---
title: "Definir opções de rastreamento globais (SQL Server Profiler) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- global trace options [SQL Server]
ms.assetid: 2854608a-c3c7-4eb8-b567-034bfec4b1a9
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e243eb89d6006d82191e73577ed18dd9a5840bd9
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="set-global-trace-options-sql-server-profiler"></a>Definir opções de rastreamento globais (SQL Server Profiler)
  Este tópico descreve como definir opções que se aplicam a todos os rastreamentos criados com uma instância específica do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-set-global-trace-options"></a>Para definir opções de rastreamento globais  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Na caixa de diálogo **Opções Gerais**, clique em **Escolher Fonte**para modificar as opções de exibição e clique em **OK**.  
  
3.  Opcionalmente, selecione **Iniciar rastreamento imediatamente após estabelecer a conexão**.  
  
4.  Opcionalmente, selecione **Atualizar definição de rastreamento quando a versão do provedor for alterada**. Essa opção é recomendada e encontra-se selecionada por padrão. Quando essa opção está selecionada, a definição do rastreamento é atualizada automaticamente para a versão atual do servidor em que o rastreamento é executado.  
  
5.  Opcionalmente, especifique como o servidor deve gerenciar arquivos de substituição:  
  
    -   Selecione **Carregar todos os arquivos de substituição em sequência, sem perguntar** , para carregar arquivos de substituição automaticamente durante a reprodução.  
  
    -   Selecione **Perguntar antes de carregar arquivos de substituição** para controlar arquivos de substituição durante a repetição.  
  
    -   Selecione **Nunca carregar arquivos de substituição subsequentes** para reproduzir apenas um arquivo por vez.  
  
6.  Opcionalmente, defina as opções de repetição:  
  
    -   **Número padrão de threads de reprodução** controla o número de threads de processador a ser usado durante a reprodução. Um número maior de threads faz com que a repetição se conclua mais rápido, mas degrada o desempenho do servidor durante a repetição. A configuração recomendada é **4**. A tabela a seguir lista as opções disponíveis:  
  
        |Valor|Descrição|  
        |-----------|-----------------|  
        |**2**|Valor mínimo. Usar dois threads na repetição.|  
        |**4**|Valor padrão.|  
        |**255**|Valor máximo. Definir um valor máximo prejudicará o desempenho de outros processos.|  
  
    -   **Intervalo de espera padrão do monitor de integridade (s)** define o período máximo, em segundos, durante o qual um thread de repetição pode bloquear outro processo. A tabela a seguir explica os valores.  
  
        |Valor|Descrição|  
        |-----------|-----------------|  
        |**0**|Valor mínimo. Uma configuração **0** significa que o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] nunca interromperá um processo de bloqueio.|  
        |**3600**|Valor padrão. Permite processos de bloqueio que não excedam **3600** segundos, ou uma hora.|  
        |**86400**|Valor máximo. Permite processos de bloqueio que não excedam **86400** segundos, ou um dia.|  
  
    -   **Intervalo de sondagem padrão do monitor de integridade (s)** define a frequência de sondagem dos threads de reprodução para processos de bloqueio. A tabela a seguir explica os valores.  
  
        |Valor|Descrição|  
        |-----------|-----------------|  
        |**1**|Valor mínimo. Uma configuração **1** significa que o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] sondará processos de bloqueio uma vez a cada segundo.|  
        |**60**|Valor padrão. Sondar processos de bloqueio uma vez por minuto.|  
        |**86400**|Valor máximo. Sondar processos de bloqueio uma vez a cada **86.400** segundos, ou um dia.|  
  
## <a name="see-also"></a>Consulte também  
 [Definir padrões de exibição de rastreamento &#40; SQL Server Profiler &#41;](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

