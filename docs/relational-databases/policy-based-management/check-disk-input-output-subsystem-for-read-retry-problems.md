---
title: "Verificar o subsistema de entrada e saída de disco quanto a problemas de repetição de leitura | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: cedf4097-5b73-4964-9935-74a101847019
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c40f4c7e64d8ee022618c2d5d6bc962b1a94b398
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="check-disk-input-output-subsystem-for-read-retry-problems"></a>Verificar o subsistema de entrada e saída de disco para problemas de repetição de leitura
  Esta regra verifica o log de eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a mensagem de erro 825. Esta mensagem indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde ler os dados do disco na primeira tentativa. Esta mensagem indica um problema grave com o subsistema de E/S do disco. Atualmente, esta mensagem não indica um problema no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Entretanto, o problema com o disco poderia causar perda de dados ou danos no banco de dados se não for resolvido.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 As ações a seguir podem ajudar a identificar e resolver o problema subjacente no hardware:  
  
-   Revise o log de erros e o texto variável nesta mensagem para encontrar pistas que expliquem o problema.  
  
-   Verifique o sistema de disco. O problema pode estar relacionado aos discos, aos controladores de disco, aos cartões de matriz ou aos drivers de disco.  
  
-   Contate o fabricante do disco para obter os mais recentes utilitários para verificar o status do sistema do disco.  
  
-   Contate o fabricante do disco para obter as mais recentes atualizações de driver.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [MSSQLSERVER_825](http://msdn.microsoft.com/library/f69f8214-5af1-4769-878b-117ad6eaff52)  
  
 [Fundamentos de E/S do SQL Server, Capítulo 2](http://go.microsoft.com/fwlink/?linkid=69370)  
  
  
