---
title: Valores HOST_NAME | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newsubwizard.hostnamevalue.f1
ms.assetid: 21548f08-2910-4a55-baac-b911ba9afaf1
caps.latest.revision: "20"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c14e995d8e5f27ec5df6bda0d605c5f6a662386a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="hostname-values"></a>Valores HOST_NAME
  Asp ublicações de mesclagem com filtros com parâmetros usam a função SUSER_SNAME() e/ou a função HOST_NAME() para filtrar dados. A função é especificada no Assistente para Nova Publicação ou na caixa de diálogo **Propriedades de Publicação** .  
  
 Por padrão, a função HOST_NAME() retorna o nome do computador que conecta ao Publicador. É comum substituir esse valor, ao usar filtros com parâmetros, fornecendo um valor nessa página do assistente. Uma função HOST_NAME() retorna o valor que você especifica em lugar do nome do computador. Para mais informações, consulte a seção “Substituindo o valor do HOST_NAME()” de [Filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
> [!NOTE]  
>  Se substituir HOST_NAME(), todas as chamadas para a função HOST_NAME() retornarão o valor que você especificou. Assegure-se de que outros aplicativos não estão dependendo de que HOST_NAME() retorne o nome do computador.  
  
## <a name="options"></a>Opções  
 **Propriedades da assinatura**  
 Insira um valor para cada Assinante na coluna **Valor de HOST_NAME** ou aceite o padrão, que é o nome do computador do Assinante.  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Exibir e modificar propriedades de assinatura push](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [HOST_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md)   
 [Assinar Publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
