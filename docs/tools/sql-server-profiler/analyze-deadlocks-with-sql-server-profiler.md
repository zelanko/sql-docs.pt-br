---
title: Analisar Deadlocks com o SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- process nodes [SQL Server Profiler]
- Profiler [SQL Server Profiler], deadlocks
- deadlocks [SQL Server], identifying cause
- resource nodes [SQL Server Profiler]
- graphs [SQL Server Profiler]
- SQL Server Profiler, deadlocks
- events [SQL Server], deadlocks
- edges [SQL Server Profiler]
ms.assetid: 72d6718f-501b-4ea6-b344-c0e653f19561
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 918856e619fbb44ef5b5bc382e5d95efc99aba0e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47833484"
---
# <a name="analyze-deadlocks-with-sql-server-profiler"></a>Analisar deadlocks com o SQL Server Profiler
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para identificar a causa de um deadlock. Um deadlock ocorre quando há uma dependência cíclica entre dois ou mais threads, ou processos, do mesmo conjunto de recursos dentro do SQL Server. Usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], é possível criar um rastreamento que registra, reproduz e exibe eventos de deadlock para análise.  
  
 Para rastrear eventos de deadlock, adicione a classe de evento **Deadlock graph** a um rastreamento. Esta classe de evento popula a coluna de dados **TextData** no rastreamento com dados XML sobre o processo e objetos que estão envolvidos no deadlock. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] pode extrair o documento XML para um arquivo XML de deadlock (.xdl) que pode ser exibido posteriormente no SQL Server Management Studio. Você pode configurar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para extrair eventos **Deadlock graph** para um único arquivo contendo todos os eventos **Deadlock graph** ou para arquivos separados. Essa extração pode ser feita de qualquer uma destas formas:  
  
-   No momento da configuração do rastreamento, usando a guia **Configurações de Extração de Eventos** . Observe que essa guia não será exibida a menos que você selecione o evento **Deadlock graph** na guia **Seleção de Eventos** .  
  
-   Usando a opção **Extrair Eventos do SQL Server** no menu **Arquivo** .  
  
-   Eventos individuais também podem ser extraídos e salvos clicando com o botão direito do mouse em um evento específico e escolhendo **Extrair Dados de Evento**.  
  
## <a name="deadlock-graphs"></a>Gráficos de deadlock  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usam um gráfico de espera de deadlock para descrever um deadlock. O gráfico de espera de deadlock contém nós de processo, nós de recurso e bordas representando as relações entre os processos e os recursos. Os componentes dos gráficos de espera estão definidos na tabela a seguir:  
  
 Nó de processo  
 Um thread que executa uma tarefa; por exemplo, INSERT, UPDATE ou DELETE.  
  
 Nó de recurso  
 Um objeto de banco de dados; por exemplo, uma tabela, índice ou linha.  
  
 Borda  
 Uma relação entre um processo e um recurso. Uma borda **request** ocorre quando um processo aguarda um recurso. Uma borda **owner** ocorre quando um recurso aguarda um processo. O modo de bloqueio encontra-se na descrição da borda. Por exemplo, **Modo: X**.  
  
## <a name="deadlock-process-node"></a>Nó de processo de deadlock  
 Em um gráfico de espera, o nó de processo contém informações sobre o processo. A tabela a seguir explica os componentes de um processo.  
  
|Componente|Definição|  
|---------------|----------------|  
|ID de processo do servidor|Identificador de processo de servidor (SPID), um identificador atribuído pelo servidor ao processo proprietário do bloqueio.|  
|ID de lote do servidor|Identificador de lote de servidor (SBID).|  
|ID do contexto de execução|Identificador do contexto de execução (ECID). A ID do contexto de execução de determinado thread associado a uma SPID específica.<br /><br /> ECID = {0,1,2,3, *...n*}, em que 0 sempre representa o thread principal ou pai e {1,2,3, *...n*} representa os subthreads.|  
|Prioridade do deadlock|Prioridade do deadlock para o processo. Para obter mais informações sobre os valores possíveis, veja [SET DEADLOCK_PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/set-deadlock-priority-transact-sql.md).|  
|Log Usado|Quantidade de espaço de log usada pelo processo.|  
|ID do Proprietário|ID de transação para os processos que estão usando transações e, atualmente, aguardam em um bloqueio.|  
|Descritor da transação|Ponteiro para o descritor de transação que descreve o estado da transação.|  
|Buffer de entrada|Buffer de entrada do processo atual; define o tipo de evento e a instrução que são executados. Os valores possíveis incluem:<br /><br /> **Idioma**<br /><br /> **RPC**<br /><br /> **Nenhuma**|  
|de|Tipo de instrução. Os valores possíveis são:<br /><br /> **NOP**<br /><br /> **SELECT**<br /><br /> **UPDATE**<br /><br /> **INSERT**<br /><br /> **DELETE**<br /><br /> **Unknown (desconhecido)**|  
  
## <a name="deadlock-resource-node"></a>Nó de recurso de deadlock  
 Em um deadlock, dois processos esperam por um recurso ocupado pelo outro processo. Em um gráfico de deadlock, os recursos são exibidos como nós de recurso.  
  
  
