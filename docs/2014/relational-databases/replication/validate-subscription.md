---
title: Validar Assinatura | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.validate.validateandresynch.f1
helpviewer_keywords:
- Validate Subscription dialog box
ms.assetid: 74bdf5e1-b886-4284-b5fb-332bf79ae083
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5f7fae7d5ea40c7914d7f49653e4a8b5530c774f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013088"
---
# <a name="validate-subscription"></a>Validar Assinatura
  Use a caixa de diálogo **Validar Assinatura** para especificar que uma assinatura em uma publicação de mesclagem deve ser validada na próxima execução de assinatura do Merge Agent. Os resultados de validação são exibidos no Replication Monitor. Para obter mais informações, consulte [Validate Data at the Subscriber](validate-data-at-the-subscriber.md).  
  
 Também é possível validar todas as assinaturas para uma publicação de mesclagem clicando com o botão direito do mouse em uma publicação no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e clicando em **Validar Todas as Assinaturas**.  
  
## <a name="options"></a>Opções  
 **Data da última tentativa de validação**  
 A data da última sessão do Merge Agent que incluiu validação de assinatura, independentemente de a validação ter tido êxito.  
  
 **Data da última validação bem-sucedida**  
 A data da última sessão do Merge Agent que incluiu uma validação de assinatura bem-sucedida.  
  
 **Validar esta assinatura**  
 Selecione para validar a assinatura.  
  
 **Opções**  
 Clique para acessar a caixa de diálogo **Opções de Validação de Assinatura** , que permite especificar se deve ser usada a validação de contagem de linhas ou validação de soma de verificação binária.  
  
## <a name="see-also"></a>Consulte também  
 [Validar os dados replicados](validate-replicated-data.md)  
  
  