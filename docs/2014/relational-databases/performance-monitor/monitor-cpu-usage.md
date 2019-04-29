---
title: Monitorar o uso da CPU | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server], CPU usage
- tuning databases [SQL Server], CPU usage
- processors [SQL Server], monitoring usage
- database performance [SQL Server], CPU usage
- monitoring CPU usage [SQL Server]
- server performance [SQL Server], CPU usage
- database monitoring [SQL Server], CPU usage
- monitoring [SQL Server], CPU usage
- processors [SQL Server]
- CPU [SQL Server], monitoring
- monitoring server performance [SQL Server], CPU usage
ms.assetid: 2a02a3b6-07b2-4ad0-8a24-670414d19812
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: e46610823432efde0cc757e3dff317227b7548ac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63032091"
---
# <a name="monitor-cpu-usage"></a>Monitorar o uso da CPU
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Monitore uma instância do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] periodicamente para determinar se as taxas de uso de CPU estão dentro dos intervalos normais. Uma taxa de uso de CPU continuamente alta pode indicar a necessidade de atualizar a CPU ou de adicionar vários processadores. Alternativamente, uma taxa de uso de CPU alta pode indicar um aplicativo mal-ajustado ou malprojetado. Otimizar o aplicativo pode baixar a utilização de CPU.  
  
 Um modo eficiente de determinar o uso de CPU é usar o contador **Processador: %tempo de processador** do Monitor do Sistema. Esse contador monitora o tempo gasto pela CPU para executar um thread que não está ocioso. Um estado consistente de 80 a 90 por cento pode indicar a necessidade de atualizar a CPU ou de adicionar mais processadores. Para sistemas com vários processadores, monitore uma instância separada desse contador para cada processador. Esse valor representa a soma do tempo de processador em um processador específico. Para determinar a média de todos os processadores, use o contador **Sistema: %tempo total de processador** .  
  
 Opcionalmente, você também pode monitorar os seguintes contadores para monitorar o uso de processador:  
  
-   **Processador: % tempo privilegiado**  
  
     Corresponde à porcentagem de tempo que o processador gasta na execução de comandos de kernel do Microsoft Windows, como o processamento de solicitações de E/S do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se esse contador estiver consistentemente alto quando os contadores do **Disco Físico** estiverem altos, considere instalar um subsistema de disco mais rápido ou eficiente.  
  
    > [!NOTE]  
    >  Controladores de disco e drivers diferentes usam tempos diferentes de processamento de kernel. Controladores e drivers eficientes usam menos tempo privilegiado, deixando mais tempo de processamento disponível para aplicativos de usuário, o que aumenta o processamento global.  
  
-   **Processador: % tempo de usuário**  
  
     Corresponde à porcentagem de tempo que o processador gasta na execução de processos de usuário, como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Sistema: Extensão da Fila do Processador**  
  
     Corresponde ao número de threads que esperam por tempo de processador. Um gargalo de processador acontece quando os threads de um processo exigem mais ciclos de processador do que os disponíveis. Se muitos processos tentarem utilizar o tempo de processador, pode ser necessário instalar um processador mais rápido. Caso seja um sistema com vários processadores, você pode adicionar um processador.  
  
 Ao examinar o uso de processador, considere o tipo de trabalho que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] efetua muitos cálculos, como consultas envolvendo agregações ou consultas associadas à memória que não requerem E/S em disco, pode ser usado 100 % do tempo de processador. Se isso influir no desempenho de outros aplicativos, experimente alterar a carga de trabalho. Por exemplo, dedique o computador à execução da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Taxas de uso em torno de 100 %, quando estão sendo processadas muitas solicitações de cliente, podem indicar que os processos estão formando fila para aguardar o tempo de processador e provocando um gargalo. Resolva o problema adicionando processadores mais rápidos.  
  
  
