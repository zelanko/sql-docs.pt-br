---
title: "Verificar o subsistema de entrada e saída de disco quanto a problemas de repetição de leitura | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: cedf4097-5b73-4964-9935-74a101847019
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 48624f64233a37be0f1d1c2dc5ad0be6b323cfe6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="check-disk-input-output-subsystem-for-read-retry-problems"></a>Verificar o subsistema de entrada e saída de disco para problemas de repetição de leitura
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Esta regra verifica o log de eventos quanto à mensagem de erro 825 do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta mensagem indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde ler os dados do disco na primeira tentativa. Esta mensagem indica um problema grave com o subsistema de E/S do disco. Atualmente, esta mensagem não indica um problema no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Entretanto, o problema com o disco poderia causar perda de dados ou danos no banco de dados se não for resolvido.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 As ações a seguir podem ajudar a identificar e resolver o problema subjacente no hardware:  
  
-   Revise o log de erros e o texto variável nesta mensagem para encontrar pistas que expliquem o problema.  
  
-   Verifique o sistema de disco. O problema pode estar relacionado aos discos, aos controladores de disco, aos cartões de matriz ou aos drivers de disco.  
  
-   Contate o fabricante do disco para obter os mais recentes utilitários para verificar o status do sistema do disco.  
  
-   Contate o fabricante do disco para obter as mais recentes atualizações de driver.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [MSSQLSERVER_825](http://msdn.microsoft.com/library/f69f8214-5af1-4769-878b-117ad6eaff52)  
  
 [Fundamentos de E/S do SQL Server, Capítulo 2](http://go.microsoft.com/fwlink/?linkid=69370)  
  
  
