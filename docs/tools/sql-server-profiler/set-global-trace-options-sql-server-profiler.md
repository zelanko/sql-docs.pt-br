---
title: Definir opções de rastreamento globais
titleSuffix: SQL Server Profiler
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 2854608a-c3c7-4eb8-b567-034bfec4b1a9
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: c66bb6a8a2f894cb80fd17c9fce24a0d98d027f2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75307948"
---
# <a name="set-global-trace-options-sql-server-profiler"></a>Definir opções de rastreamento globais (SQL Server Profiler)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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
  
        |Valor|DESCRIÇÃO|  
        |-----------|-----------------|  
        |**2**|Valor mínimo. Usar dois threads na repetição.|  
        |**4**|Valor padrão.|  
        |**255**|Valor máximo. Definir um valor máximo prejudicará o desempenho de outros processos.|  
  
    -   **Intervalo de espera padrão do monitor de integridade (s)** define o período máximo, em segundos, durante o qual um thread de repetição pode bloquear outro processo. A tabela a seguir explica os valores.  
  
        |Valor|DESCRIÇÃO|  
        |-----------|-----------------|  
        |**0**|Valor mínimo. Uma configuração **0** significa que o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] nunca interromperá um processo de bloqueio.|  
        |**3600**|Valor padrão. Permite processos de bloqueio que não excedam **3600** segundos, ou uma hora.|  
        |**86400**|Valor máximo. Permite processos de bloqueio que não excedam **86400** segundos, ou um dia.|  
  
    -   **Intervalo de sondagem padrão do monitor de integridade (s)** define a frequência de sondagem dos threads de reprodução para processos de bloqueio. A tabela a seguir explica os valores.  
  
        |Valor|DESCRIÇÃO|  
        |-----------|-----------------|  
        |**1**|Valor mínimo. Uma configuração **1** significa que o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] sondará processos de bloqueio uma vez a cada segundo.|  
        |**60**|Valor padrão. Sondar processos de bloqueio uma vez por minuto.|  
        |**86400**|Valor máximo. Sondar processos de bloqueio uma vez a cada **86.400** segundos, ou um dia.|  
  
## <a name="see-also"></a>Consulte Também  
 [Definir padrões de exibição de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
