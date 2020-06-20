---
title: Chaves simétricas em bancos de dados do usuário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3333ab5b-2518-4753-a0a8-57df5e5af74f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ca0fb62ccb32ce244e1087281997dcd9929df89c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066608"
---
# <a name="symmetric-keys-on-user-databases"></a>Chaves simétricas em bancos de dados de usuários
  Esta regra verifica se as chaves com um comprimento menor que 128 bytes não usam o algoritmo de criptografia RC2 ou RC4.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Use AES de 128 bits ou maior para criar chaves simétricas para criptografia de dados. Se não houver suporte a AES no seu sistema operacional, use 3DES.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Escolher um algoritmo de criptografia](../security/encryption/choose-an-encryption-algorithm.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor melhores práticas usando o gerenciamento baseado em políticas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
