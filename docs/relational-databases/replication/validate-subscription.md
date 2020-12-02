---
description: Validar Assinatura
title: Validar Assinatura | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.validateandresynch.f1
helpviewer_keywords:
- Validate Subscription dialog box
ms.assetid: 74bdf5e1-b886-4284-b5fb-332bf79ae083
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 2e80697f75a6234b913e0784b0110873b3c848ac
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88470120"
---
# <a name="validate-subscription"></a>Validar Assinatura
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  Use a caixa de diálogo **Validar Assinatura** para especificar que uma assinatura em uma publicação de mesclagem deve ser validada na próxima execução de assinatura do Merge Agent. Os resultados de validação são exibidos no Replication Monitor. Para obter mais informações, consulte [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
 Também é possível validar todas as assinaturas para uma publicação de mesclagem clicando com o botão direito do mouse em uma publicação no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e clicando em **Validar Todas as Assinaturas**.  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>Opções  
 **Data da última tentativa de validação**  
 A data da última sessão do Merge Agent que incluiu validação de assinatura, independentemente de a validação ter tido êxito.  
  
 **Data da última validação bem-sucedida**  
 A data da última sessão do Merge Agent que incluiu uma validação de assinatura bem-sucedida.  
  
 **Validar esta assinatura**  
 Selecione para validar a assinatura.  
  
 **Opções**  
 Clique para acessar a caixa de diálogo **Opções de Validação de Assinatura** , que permite especificar se deve ser usada a validação de contagem de linhas ou validação de soma de verificação binária.  
  
## <a name="see-also"></a>Consulte Também  
 [Validar os dados replicados](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
