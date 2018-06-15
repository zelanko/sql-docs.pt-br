---
title: Validar Todas as Assinaturas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.allsubscriptions.f1
helpviewer_keywords:
- Validate All Subscriptions dialog box
ms.assetid: 32e31469-36e4-42d9-a57a-12388bfd229d
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1ce404929248e867df2d2c127521ec30fe29050e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32960551"
---
# <a name="validate-all-subscriptions"></a>Validar Todas as Assinaturas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use a caixa de diálogo **Validar Todas as Assinaturas** para especificar que todas as assinaturas em uma publicação de mesclagem devem ser validadas na próxima execução do Merge Agent. Os resultados de validação são exibidos no Replication Monitor. Para obter mais informações, consulte [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
 Também é possível validar uma única assinatura clicando com o botão direito em uma assinatura no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e clicando em **Validar Assinatura**.  
  
## <a name="options"></a>Opções  
 **Verificar as contagens de linhas somente**  
 Selecione para validar se a tabela no Assinante tem o mesmo número de linhas que a tabela no Publicador. Esse método não valida que o conteúdo de correspondências de linhas. A validação de número de linhas fornece uma abordagem superficial à validação que pode alertá-lo sobre problemas com seus dados.  
  
 **Verificar as contagens de linhas e comparar as somas de verificação para verificar os dados da linha**  
 Além de contar o número de linhas no Publicador e no Assinante, uma soma de verificação de todos os dados é calculada usando o algoritmo de soma de verificação binária. Se a contagem de linhas falhar, a soma de verificação não será executada. Essa opção não é válida para [!INCLUDE[ssEW](../../includes/ssew-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Validar os dados replicados](../../relational-databases/replication/validate-replicated-data.md)  
  
  
