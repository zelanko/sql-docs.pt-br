---
title: "Executar lógica de negócios durante sincronizações de mesclagem | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- custom error resolution [SQL Server replication]
- custom change handling [SQL Server replication]
- errors [SQL Server replication], business logic handlers
- merge replication business logic handlers [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
- business logic handlers [SQL Server replication]
ms.assetid: 9d4da2ef-c17f-4a31-a1f6-5c3b7ca85f71
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0a165253bc79d9fe6c958a9d0e8ec83e73cf58c7
ms.lasthandoff: 04/11/2017

---
# <a name="execute-business-logic-during-merge-synchronization"></a>Executar lógica de negócios durante sincronizações de mesclagem
  A estrutura do manipulador de lógica comercial permite que você grave um assembly de código gerenciado que é chamado durante o processo de sincronização de mesclagem. O assembly inclui lógica comercial que pode responder a uma série de condições durante a sincronização: alterações de dados, conflitos e erros. A estrutura do manipulador de lógica comercial oferece um modelo de programação simples e os dados que o processo de mesclagem oferece ao seu assembly estão na forma de um conjunto de dados ADO.NET, portanto você pode aproveitar do conhecimento de ADO.NET ao invés de aprender uma interface proprietária. Para obter mais informações sobre como programar manipuladores de lógica comercial, consulte:  
  
-   A referência de API (interface de programação de aplicativo): <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>  
  
-   Instruções sobre como implementar um manipulador de lógica de negócios: [Implementar um manipulador de lógica de negócios para um artigo de mesclagem](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
## <a name="uses-for-business-logic-handlers"></a>Usos para manipuladores de lógica comercial  
 O processo de sincronização de mesclagem pode chamar manipuladores de lógica comercial para executar:  
  
-   Manipulação de alteração personalizada  
  
-   Resolução de conflito personalizada  
  
-   Resolução de erro personalizada  
  
> [!NOTE]  
>  O manipulador de lógica de negócios que você especificar será executado para cada linha que for sincronizada. A lógica complexa e as chamadas para outros aplicativos ou serviços de rede podem comprometer o desempenho.  
  
### <a name="custom-change-handling"></a>Manipulação de alteração personalizada  
 O manipulador de lógica comercial pode ser invocado durante o processamento de alterações de dados não conflitantes e pode executar uma destas três ações:  
  
-   Rejeite os dados  
  
     Isso é útil para aplicativos que não querem alterações propagadas para ou de um determinado Assinante. Por exemplo, um administrador poderá retirar inserções que não pertencem à partição do Assinante ou possivelmente rejeitar exclusões executadas em um Assinante. Como outro exemplo, um aplicativo poderá rejeitar uma ordem inserida em um Assinante porque o inventário não está mais disponível.  
  
-   Aceite os dados  
  
     Isto é útil para aplicativos nos quais é necessário rever alterações de dados feitas no Publicador ou Assinante antes de permitir a sua propagação. Por exemplo, um aplicativo da camada intermediária poderá examinar novas ordens provenientes do campo e integrá-las com um processo de fluxo de trabalho de aquisição na camada intermediária.  
  
-   Aplique dados personalizados  
  
     Isto é útil para aplicativos que precisam substituir valores de dados ou operações específicos. Por exemplo, uma aplicativo poderá transformar a exclusão de uma linha em uma atualização especial que define uma coluna de **status** na linha a um valor de "excluído" e então rastreia a identidade do cliente executando a exclusão. Isto poderá ser útil para fins de auditoria ou de fluxo de trabalho.  
  
### <a name="custom-conflict-resolution"></a>Resolução de conflito personalizada  
 A replicação de mesclagem fornece detecção e solução de conflitos, permitindo que você aceite uma estratégia de resolução padrão ou escolha uma resolução personalizada para conflitos. Para obter mais informações, consulte [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md). O manipulador de lógica comercial pode ser chamado durante o processamento de alterações de dados conflitantes e pode executar uma destas duas ações:  
  
-   Aceite resolução padrão  
  
     Isso é útil para aplicativos que podem precisar analisar o conflito, executar ações adicionais e possivelmente registrar uma mensagem de log de conflito personalizada.  
  
-   Execute resolução personalizada  
  
     Isso é útil para aplicativos que podem precisar selecionar valores de dados que são específicos à sua lógica comercial e fornecer o processo de sincronização com este conjunto de dados personalizados. Por exemplo, um aplicativo poderá fornecer uma nova versão da linha vencedora combinando valores dos conjuntos de dados do Publicador e Assinante.  
  
### <a name="custom-error-resolution"></a>Resolução de erro personalizada  
 A lógica personalizada pode ser chamada durante a propagação de alterações que resultam em erros. A lógica pode executar uma dessas duas ações:  
  
-   Aceite resolução de erro padrão  
  
     Isso é útil para aplicativos precisam analisar o erro e executar outras ações e, possivelmente, registrar uma mensagem de log de erros personalizada.  
  
-   Aceite resolução de erro personalizada  
  
     Isso é útil para aplicativos que podem precisar selecionar valores de dados que são específicos à sua lógica comercial e fornecer o processo de sincronização com este conjunto de dados personalizados. Por exemplo, se o processo de replicação encontrar uma violação de chave duplicada, o manipulador de lógica comercial poderá fornecer uma nova versão da alteração de dados em que a chave não será mais conflitante. As alterações feitas no Publicador e Assinante poderão então persistir no banco de dados e o processo de replicação não terá que compensar pela inserção falha com uma exclusão.  
  
## <a name="deployment-scenarios-for-business-logic-handlers"></a>Cenários de Implantação para manipuladores de lógica comercial  
 Manipuladores de lógica comercial podem ser implantados no:  
  
-   O Distribuidor. Use uma assinatura push de forma que a lógica comercial seja executada no Distribuidor.  
  
-   Assinante. Use uma assinatura pull de forma que a lógica comercial seja executada no Assinante.  
  
-   Um servidor IIS (Serviços de Informações da Internet) se a sincronização da Web for usada. Use uma assinatura pull sincronizada com a sincronização da Web e o manipulador de lógica comercial executará no Servidor IIS.  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de mesclagem](../../../relational-databases/replication/merge/merge-replication.md)   
 [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md)   
 [Sincronizar dados](../../../relational-databases/replication/synchronize-data.md)   
 [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
