---
title: "Propriedades da publicação, geral | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newpubwizard.pubproperties.general.f1
ms.assetid: 7912362f-c4d6-4f60-bd39-dee1f656ed18
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8bbcc75b2e04f5bfa9e96fa0f0b39099eaa9872a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="publication-properties-general"></a>Propriedades de Publicação, Geral
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] A página **Geral** da caixa de diálogo **Propriedades de Publicação** contém informações básicas sobre a publicação, incluindo nome, descrição e a política de validade da assinatura.  
  
## <a name="options"></a>Opções  
 **Nome**  
 O nome da publicação (somente leitura).  
  
 **Banco de dados**  
 O nome do banco de dados de publicação (somente leitura).  
  
 **Descrição**  
 A descrição da publicação.  
  
 **Tipo**  
 O tipo da publicação (somente leitura).  
  
 **Validade da assinatura**  
 Selecione uma das opções para validade da assinatura: **As assinaturas nunca expiram** ou **As assinaturas expiram**, com um período de tempo explícito (**Intervalo**).  
  
 Para publicações de instantâneo e transacionais, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você aceite o padrão de **As assinaturas nunca expiram**.  
  
 Para replicação de mesclagem, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você aceite o padrão de **As assinaturas nunca expiram** e defina um valor o mais baixo possível para o **Intervalo**. Como o período de validade da assinatura aumenta, o mesmo ocorre com os metadados armazenados, que podem afetar desempenho. Equilibre a necessidade de desconectar os Assinantes ou simplesmente não sincronize por um período estendido em questões de desempenho potencial de armazenamento e processamento de grande quantidade de metadados.  
  
 Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 **Nível de compatibilidade**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] and later versions only; merge publications only. Selecione versão mínima requerida do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Assinantes que sincronizam com essa publicação. Há várias regras associadas com a determinação do nível de compatibilidade.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
