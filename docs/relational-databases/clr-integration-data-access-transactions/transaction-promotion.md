---
title: "Promoção de transação | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- distributed transactions [CLR integration]
- promoting transactions [CLR integration]
- Enlist keyword
- transaction promotion [CLR integration]
ms.assetid: 5bc7e26e-28ad-4198-a40d-8b2c648ba304
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 492191dfa1f3784ccacd8d7f7f12a247f76c9741
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="transaction-promotion"></a>Promoção de transações
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Transação *promoção* descreve uma transação local superficial que pode ser elevada automaticamente a uma transação totalmente distribuída conforme necessário. Quando um procedimento armazenado gerenciado é invocado em uma transação de banco de dados no servidor, o código CLR (Common Language Runtime) é executado no contexto de uma transação local.  Se houver uma conexão com um servidor remoto aberta em uma transação de banco de dados, a conexão com o servidor remoto será inscrita na transação distribuída e a transação local será elevada automaticamente a uma transação distribuída. Assim, a promoção da transação minimiza a sobrecarga das transações distribuídas, adiando a criação de uma transação distribuída até que seja necessário. A promoção da transação será automática, se tiver sido habilitada usando a palavra-chave **Enlist** e não exigir a intervenção do desenvolvedor. O .NET Framework Data Provider para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece suporte para a promoção de transações, tratada pelas classes do .NET Framework **SqlClient** namespace.  
  
## <a name="the-enlist-keyword"></a>A palavra-chave Enlist  
 A propriedade **ConnectionString** de um objeto **SqlConnection** dá suporte à palavra-chave **Enlist** , que indica se **System.Data.SqlClient** detecta contextos transacionais e inscreve automaticamente a conexão em uma transação distribuída. Se essa palavra-chave for definida como true (padrão), a conexão será inscrita automaticamente no contexto da transação atual do thread de abertura. Se essa palavra-chave for definida como false, a conexão SqlClient não irá interagir com uma transação distribuída. Se **Enlist** não estiver especificada na cadeia de conexão, a conexão será inscrita automaticamente em uma transação distribuída, caso uma seja detectada no momento em que a conexão é aberta.  
  
## <a name="distributed-transactions"></a>Transações distribuídas  
 Normalmente, as transações distribuídas consomem recursos do sistema significativos. O Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC) gerencia essas transações e integra todos os gerenciadores de recursos acessados nessas transações. Promoção de transação, por outro lado, é uma forma especial de um **System. Transactions** transação que delega efetivamente o trabalho para um simples [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transação. **System. Transactions**, **SqlClient**, e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] coordenar o trabalho envolvido no tratamento da transação, promovê-lo para uma transação distribuída completa, conforme necessário.  
  
 A vantagem de usar a promoção de transações é que, quando uma conexão é aberta com uma transação **TransactionScope** ativa e não há qualquer outra conexão aberta, a transação é confirmada como uma transação superficial, em vez de incorrer na sobrecarga adicional de uma transação distribuída completa. Para obter mais informações sobre **TransactionScope**, consulte [usando System. Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Integração CLR e transações](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
