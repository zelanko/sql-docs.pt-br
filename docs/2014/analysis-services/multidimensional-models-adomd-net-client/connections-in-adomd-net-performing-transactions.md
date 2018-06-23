---
title: Executando transações no ADOMD.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- transactions [ADOMD.NET]
- ADOMD.NET, transactions
- AdomdTransaction object
ms.assetid: 7978c28b-c255-43c0-ad05-f38604d4d8fe
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2b37257b647dc9c1675e36c0f0b6a9b06bbf08d8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121175"
---
# <a name="performing-transactions-in-adomdnet"></a>Executando transações no ADOMD.NET
  No ADOMD.NET, você usa o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> para gerenciar contexto de transação para um determinado objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>. Essa funcionalidade permite que você execute vários comandos dentro do mesmo contexto. Cada comando lerá os mesmos dados sem que os dados lidos sejam alterados entre cada execução de comando.  
  
> [!NOTE]  
>  A classe <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> é a implementação da interface `System.Data.IDbTransaction`, parte da Biblioteca de Classes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework e implementada por todos os provedores de dados .NET Framework que dão suporte a transações.  
  
 O objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> só dá suporte a transações confirmadas por leitura em que bloqueios compartilhados são mantidos enquanto os dados são lidos para impedir leituras sujas.  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> é usado para iniciar a transação. Para usá-la, os comandos serão executados na conexão que a iniciou. Quando concluir a transação, você poderá revertê-la ou confirmá-la.  
  
## <a name="starting-a-transaction"></a>Iniciando uma transação  
 Você cria uma instância de um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> chamando o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.BeginTransaction%2A> do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>. O exemplo a seguir mostra como criar uma instância do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>:  
  
```  
Dim objTransaction As AdomdTransaction = objConnection.BeginTransaction()  
AdomdTransaction objTransaction = objConnection.BeginTransaction();  
```  
  
## <a name="rolling-back-a-transaction"></a>Revertendo uma transação  
 Para reverter transação existente e incompleta, chame o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction.Rollback%2A> do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>. Se você chamar esse método em uma transação existente e completa, será lançada uma exceção.  
  
## <a name="committing-a-transaction"></a>Confirmando uma transação  
 Depois de chamar o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.BeginTransaction%2A> para iniciar uma transação, você poderá concluir a transação chamando o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction.Commit%2A> do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>. Se esse método for chamado em uma transação existente e completa, será lançada uma exceção.  
  
## <a name="see-also"></a>Consulte também  
 [Estabelecendo conexões no ADOMD.NET](connections-in-adomd-net.md)   
 [Programação do cliente no ADOMD.NET](adomd-net-client-programming.md)  
  
  