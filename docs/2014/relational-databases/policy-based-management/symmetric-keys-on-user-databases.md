---
title: Chaves simétricas em bancos de dados do usuário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3333ab5b-2518-4753-a0a8-57df5e5af74f
caps.latest.revision: 5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8f8a87976d4db4e00207822bbd171e2fb0844dcb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37284942"
---
# <a name="symmetric-keys-on-user-databases"></a>Chaves simétricas em bancos de dados de usuários
  Esta regra verifica se as chaves com um comprimento menor que 128 bytes não usam o algoritmo de criptografia RC2 ou RC4.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Use AES de 128 bits ou maior para criar chaves simétricas para criptografia de dados. Se não houver suporte a AES no seu sistema operacional, use 3DES.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Escolher um algoritmo de criptografia](../security/encryption/choose-an-encryption-algorithm.md)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
