---
title: Propriedades da publicação, geral | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.general.f1
ms.assetid: 7912362f-c4d6-4f60-bd39-dee1f656ed18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6bbcd23aa185e9d311fbc8b81d9ab167717997b2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718754"
---
# <a name="publication-properties-general"></a>Propriedades de Publicação, Geral
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A página **Geral** da caixa de diálogo **Propriedades de Publicação** contém informações básicas sobre a publicação, incluindo nome, descrição e a política de validade da assinatura.  
  
## <a name="options"></a>Opções  
 **Nome**  
 O nome da publicação (somente leitura).  
  
 **Backup de banco de dados**  
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
  
## <a name="see-also"></a>Consulte Também  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
