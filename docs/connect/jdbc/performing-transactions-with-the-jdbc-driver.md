---
title: "Executando transações com o Driver JDBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: afbb776f-05dc-4e79-bb25-2c340483e401
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ba17135613396e2552119aa058dfba0a73a07f3e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="performing-transactions-with-the-jdbc-driver"></a>Executando transações com o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O processamento de transações é um requisito obrigatório de todos os aplicativos que desejam garantir consistência de seus dados persistentes. Com o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], processamento de transações pode ser realizado localmente ou distribuído. Transações são módulos de execução atômicos, consistentes, isolados e duráveis (ACID).  
  
 Os tópicos nesta seção descrevem como o driver JDBC oferece suporte a transações inclusive níveis de isolamento, pontos de salvamento de transação e retenção do conjunto de resultados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Noções básicas sobre transações](../../connect/jdbc/understanding-transactions.md)|Fornece uma visão geral de como são usadas transações com o driver JDBC.|  
|[Noções básicas sobre transações XA](../../connect/jdbc/understanding-xa-transactions.md)|Fornece uma visão geral de como são usadas transações XA com o driver JDBC.|  
|[Noções básicas sobre os níveis de isolamento](../../connect/jdbc/understanding-isolation-levels.md)|Descreve os vários níveis de isolamento que têm suporte pelo driver JDBC.|  
|[Usando pontos de salvamento](../../connect/jdbc/using-savepoints.md)|Descreve como usar o driver JDBC com pontos de salvamento de transação.|  
|[Usando colocação em espera](../../connect/jdbc/using-holdability.md)|Descreve como usar o driver JDBC com colocação em espera do conjunto de resultados.|  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

