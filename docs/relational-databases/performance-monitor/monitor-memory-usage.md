---
title: Monitorar o uso de memória | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance-monitor
ms.topic: conceptual
helpviewer_keywords:
- tuning databases [SQL Server], memory
- monitoring server performance [SQL Server], memory usage
- isolating memory [SQL Server]
- paging rate [SQL Server]
- memory [SQL Server], monitoring usage
- monitoring [SQL Server], memory usage
- low-memory conditions
- database monitoring [SQL Server], memory usage
- available memory [SQL Server]
- page faults [SQL Server]
- monitoring performance [SQL Server], memory usage
- server performance [SQL Server], memory
ms.assetid: 1aee3933-a11c-4b87-91b7-32f5ea38c87f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e51393cea321fe597047b671e604318664aec473
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51030396"
---
# <a name="monitor-memory-usage"></a>Monitorar o uso da memória
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Monitore uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] periodicamente para confirmar que o uso de memória está dentro de intervalos normais.  
  
 Para monitorar uma condição da memória baixa, use os seguintes contadores de objetos:  
  
-   **Memória: Bytes disponíveis**  
  
-   **Memória: Páginas/segundo**  
  
 O contador **Bytes disponíveis** indica quantos bytes de memória estão atualmente disponíveis para uso dos processos. O contador **Páginas/s** indica o número de páginas que foram recuperadas do disco devido a falhas de página física ou gravadas no disco para liberar espaço no conjunto de trabalho devido a falhas de página.  
  
 Baixos valores no contador **Bytes disponíveis** podem indicar a existência de uma escassez global de memória no computador ou que um aplicativo não está liberando a memória. Uma taxa alta no contador **Páginas/s** pode indicar paginação excessiva. Monitore o contador **Memory: Page Faults/sec (Memória: Falhas de Páginas/s)** para ter certeza de que a atividade no disco não é provocada por paginação.  
  
 Uma taxa baixa de paginação (e, logo, de falhas de página) é normal, mesmo que o computador tenha muita memória disponível. O Gerenciador de Memória Virtual (VMM) do Microsoft Windows conta as páginas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e de outros processos, organizando os tamanhos de conjunto de trabalho desses processos. Essa atividade do VMM tende a causar falhas de página. Para determinar se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou outro processo é a causa da paginação excessiva, monitore o contador **Process: Page Faults/sec (Processo: Falhas de Página/s)** da instância do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obter mais informações sobre como solucionar a paginação excessiva, consulte a documentação do sistema operacional Windows.  
  
## <a name="isolating-memory-used-by-sql-server"></a>Isolando a memória usada pelo SQL Server  
 Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] altera seus requisitos de memória dinamicamente, com base nos recursos de sistema disponíveis. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisar de mais memória, ele consultará o sistema operacional para determinar se há memória física livre disponível e a usará. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não precisar da memória alocada para ele atualmente, ele a liberará para o sistema operacional. Porém, é possível substituir a opção de usar a memória dinamicamente, por meio das opções de configuração de servidor **minservermemory**e **maxservermemory** . Para obter mais informações, consulte [Opções de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).  
  
 Para monitorar a quantidade de memória utilizada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , examine os seguintes contadores de desempenho:  
  
-   **Processo: Conjunto de trabalho**  
  
-   **SQL Server: Gerenciador de Buffer: Taxa de acertos do cache do buffer**  
  
-   **SQL Server: Gerenciador de Buffer: Páginas de Banco de Dados**  
  
-   **SQL Server: Gerenciador de Memória: Memória total do servidor (KB)**  
  
 O contador **WorkingSet** mostra a quantidade de memória utilizada por um processo. Se esse número estiver consistentemente abaixo da quantidade de memória definida pelas opções de servidor **min server memory** e **max server memory** , o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para usar memória demais.  
  
 O contador **Taxa de acertos do cache do buffer** é específico ao aplicativo. Porém, uma taxa de 90 por cento ou mais é desejável. Adicione memória até que o valor seja consistentemente maior que 90%. Um valor maior que 90% indica que mais de 90% de todas as solicitações de dados foram satisfeitas pelo cache de dados.  
  
 Se o contador **TotalServerMemory (KB)** estiver consistentemente alto, em comparação com a quantidade de memória física disponível no computador, isso pode indicar a necessidade de mais memória.  
  
## <a name="determining-current-memory-allocation"></a>Determinando a alocação de memória atual  
 A instrução a seguir retorna informações sobre a memória alocada atualmente.  
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
  
