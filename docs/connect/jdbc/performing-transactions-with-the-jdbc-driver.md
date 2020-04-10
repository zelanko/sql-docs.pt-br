---
title: Como executar transações com o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: afbb776f-05dc-4e79-bb25-2c340483e401
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aa86cde4d8c7d0aa91b5864f5beb3317b91bf0ee
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923745"
---
# <a name="performing-transactions-with-the-jdbc-driver"></a>Executando transações com o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O processamento de transações é um requisito obrigatório de todos os aplicativos que desejam garantir consistência de seus dados persistentes. Com o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], o processamento de transações pode ser realizado localmente ou ser distribuído. Transações são módulos de execução atômicos, consistentes, isolados e duráveis (ACID).  
  
 Os tópicos nesta seção descrevem como o driver JDBC oferece suporte a transações inclusive níveis de isolamento, pontos de salvamento de transação e retenção do conjunto de resultados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[Noções básicas sobre transações](../../connect/jdbc/understanding-transactions.md)|Fornece uma visão geral de como são usadas transações com o driver JDBC.|  
|[Noções básicas sobre transações XA](../../connect/jdbc/understanding-xa-transactions.md)|Fornece uma visão geral de como são usadas transações XA com o driver JDBC.|  
|[Noções básicas sobre níveis de isolamento](../../connect/jdbc/understanding-isolation-levels.md)|Descreve os vários níveis de isolamento que têm suporte pelo driver JDBC.|  
|[Como usar pontos de salvamento](../../connect/jdbc/using-savepoints.md)|Descreve como usar o driver JDBC com pontos de salvamento de transação.|  
|[Como usar a suspensão](../../connect/jdbc/using-holdability.md)|Descreve como usar o driver JDBC com colocação em espera do conjunto de resultados.|  
  
## <a name="see-also"></a>Confira também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
