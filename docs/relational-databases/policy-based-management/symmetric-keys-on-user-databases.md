---
title: "Chaves sim&#233;tricas em bancos de dados de usu&#225;rios | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Práticas recomendadas [Mecanismo de Banco de Dados]"
ms.assetid: 3333ab5b-2518-4753-a0a8-57df5e5af74f
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Chaves sim&#233;tricas em bancos de dados de usu&#225;rios
  Esta regra verifica se as chaves com um comprimento menor que 128 bytes não usam o algoritmo de criptografia RC2 ou RC4.  
  
## Práticas Recomendadas  
 Use AES de 128 bits ou maior para criar chaves simétricas para criptografia de dados. Se não houver suporte a AES no seu sistema operacional, use 3DES.  
  
## Para obter mais informações  
 [Escolher um algoritmo de criptografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
## Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  