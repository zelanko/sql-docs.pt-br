---
title: Transações herdadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], inherited
- child packages
- inherited transactions [Integration Services]
ms.assetid: 90db5564-d41e-4cfe-8c9e-4e68d41eff1c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d8e22375e660e6bcd55c8075edaaba067160279d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058061"
---
# <a name="inherited-transactions"></a>Transações herdadas
  Um pacote pode executar outro pacote usando a tarefa Executar Pacote. O pacote filho, que é o pacote executado pela tarefa Executar Pacote, pode criar sua própria transação de pacote ou pode herdar a transação do pacote pai.  
  
 Um pacote filho herda a transação do pacote pai se ambos os itens a seguir forem verdadeiros:  
  
-   O pacote é invocado por uma tarefa Executar Pacote.  
  
-   A tarefa Executar Pacote que invoca o pacote também tenha unido a transação de pacote pai.  
  
 Os contêineres e tarefas no pacote filho não podem unir-se à transação de pacote pai, a menos que o próprio pacote filho seja unido na transação.  
  
## <a name="illustration-of-package-transactions"></a>Ilustração de transações de pacotes  
 No diagrama a seguir, há três pacotes que usam transações. Cada pacote contém múltiplas tarefas. Para enfatizar o comportamento das transações, só serão mostradas as tarefas Executar Pacote. O pacote A executa os pacotes B e C. Por sua vez, o pacote B executa os pacotes D e E, e o pacote C executa o pacote F.  
  
 Os pacotes e tarefas têm os seguintes atributos de transação:  
  
-   **TransactionOption** é definida como **Required** nos pacotes A e C  
  
-   **TransactionOption** é definida como **Com Suporte** nos pacotes B e D, e nas tarefas Executar Pacote B, Executar Pacote C e Executar Pacote F.  
  
-   **TransactionOption** é definida como **NotSupported** no pacote E e nas tarefas Executar Pacote C e Executar Pacote E.  
  
 ![Fluxo de transações herdadas](media/mw-dts-executepack.gif "Fluxo de transações herdadas")  
  
 Só pacotes B, D e F podem herdar transações de seus pacotes pai.  
  
 Pacotes B e D herdam a transação que foi iniciada pelo pacote A.  
  
 Pacote F herda a transação que foi iniciada pelo pacote C.  
  
 Pacotes A e C controlam suas próprias transações.  
  
 Pacote E não usa transações.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Configurar um pacote para usar transações](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
