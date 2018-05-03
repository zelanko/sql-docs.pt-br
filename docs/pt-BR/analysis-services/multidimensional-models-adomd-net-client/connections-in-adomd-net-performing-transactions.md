---
title: Executando transações no ADOMD.NET | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 872d7aca21569018180e537c635032a9d036e3dd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="connections-in-adomdnet---performing-transactions"></a>Conexões no ADOMD.NET - executando transações
  No ADOMD.NET, você usa o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> para gerenciar contexto de transação para um determinado objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>. Essa funcionalidade permite que você execute vários comandos dentro do mesmo contexto. Cada comando lerá os mesmos dados sem que os dados lidos sejam alterados entre cada execução de comando.  
  
> [!NOTE]  
>  O <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> classe é a implementação do **System.Data.IDbTransaction** interface, a parte do [!INCLUDE[msCoName](../../includes/msconame-md.md)] biblioteca de classes do .NET Framework e implementada por todos os provedores de dados .NET Framework que dão suporte a transações.  
  
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
 [Estabelecendo conexões no ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)   
 [Programação do cliente no ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
