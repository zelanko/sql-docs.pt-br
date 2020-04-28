---
title: COMO limitações de predicado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d596d688956d7bdbf3d9125184d81c16249781c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298956"
---
# <a name="like-predicate-limitations"></a>Limitações do predicado LIKE
Se os dados em uma coluna forem maiores que 255 caracteres, a comparação LIKE será baseada apenas nos primeiros 255 caracteres.  
  
 Um LIKE usado em um procedimento só tem suporte com padrões constantes. Os drivers do banco de dados de desktop dão suporte ao SQL-92 como correspondência de padrões.  
  
 Não há suporte para o uso de uma cláusula escape em um predicado LIKE.  
  
 Uma comparação LIKE não deve ser executada em uma coluna que contém dados de um tipo de dados numérico ou flutuante. Os resultados podem ser imprevisíveis. Para obter mais informações, consulte o *Guia do programador do Microsoft Jet mecanismo de banco de dados*.
