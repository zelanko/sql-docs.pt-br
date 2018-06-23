---
title: Promoção de transação | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- distributed transactions [CLR integration]
- promoting transactions [CLR integration]
- Enlist keyword
- transaction promotion [CLR integration]
ms.assetid: 5bc7e26e-28ad-4198-a40d-8b2c648ba304
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 74beef45bcf29f78b800100e2c3c8ec14c301435
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020717"
---
# <a name="transaction-promotion"></a>Promoção de transações
  A *promoção* de transações descreve uma transação local superficial que pode ser elevada automaticamente a uma transação totalmente distribuída, conforme necessário. Quando um procedimento armazenado gerenciado é invocado em uma transação de banco de dados no servidor, o código CLR (Common Language Runtime) é executado no contexto de uma transação local.  Se houver uma conexão com um servidor remoto aberta em uma transação de banco de dados, a conexão com o servidor remoto será inscrita na transação distribuída e a transação local será elevada automaticamente a uma transação distribuída. Assim, a promoção da transação minimiza a sobrecarga das transações distribuídas, adiando a criação de uma transação distribuída até que seja necessário. A promoção da transação será automática, se tiver sido habilitada usando a palavra-chave `Enlist` e não exigir a intervenção do desenvolvedor. O Provedor de Dados .NET Framework para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à promoção de transações, tratada pelas classes no namespace `System.Data.SqlClient` do .NET Framework.  
  
## <a name="the-enlist-keyword"></a>A palavra-chave Enlist  
 A propriedade `ConnectionString` de um objeto `SqlConnection` dá suporte à palavra-chave `Enlist`, que indica se `System.Data.SqlClient` detecta contextos transacionais e inscreve automaticamente a conexão em uma transação distribuída. Se essa palavra-chave for definida como true (padrão), a conexão será inscrita automaticamente no contexto da transação atual do thread de abertura. Se essa palavra-chave for definida como false, a conexão SqlClient não irá interagir com uma transação distribuída. Se `Enlist` não estiver especificada na cadeia de conexão, a conexão será inscrita automaticamente em uma transação distribuída, caso uma seja detectada no momento em que a conexão é aberta.  
  
## <a name="distributed-transactions"></a>Transações distribuídas  
 Normalmente, as transações distribuídas consomem recursos do sistema significativos. O Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC) gerencia essas transações e integra todos os gerenciadores de recursos acessados nessas transações. Por outro lado, a promoção de transações é uma forma especial de uma transação `System.Transactions` que delega efetivamente o trabalho para uma simples transação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. `System.Transactions`, `System.Data.SqlClient` e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] coordenam o trabalho envolvido no tratamento da transação, elevando-a a uma transação distribuída completa, conforme necessário.  
  
 A vantagem de usar a promoção de transações é que, quando uma conexão é aberta com uma transação `TransactionScope` ativa e não há qualquer outra conexão aberta, a transação é confirmada como uma transação superficial, em vez de incorrer na sobrecarga adicional de uma transação distribuída completa. Para obter mais informações sobre `TransactionScope`, consulte [usando System. Transactions](../native-client-ole-db-transactions/transactions.md).  
  
## <a name="see-also"></a>Consulte também  
 [Integração CLR e transações](clr-integration-and-transactions.md)  
  
  