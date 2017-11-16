---
title: "Chaves simétricas em bancos de dados do usuário | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 3333ab5b-2518-4753-a0a8-57df5e5af74f
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e5ce3ca1c947a5393337ce75c4030182971c355d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="symmetric-keys-on-user-databases"></a>Chaves simétricas em bancos de dados de usuários
  Esta regra verifica se as chaves com um comprimento menor que 128 bytes não usam o algoritmo de criptografia RC2 ou RC4.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Use AES de 128 bits ou maior para criar chaves simétricas para criptografia de dados. Se não houver suporte a AES no seu sistema operacional, use 3DES.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Escolher um algoritmo de criptografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
