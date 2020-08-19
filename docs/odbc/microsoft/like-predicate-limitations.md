---
description: Limitações do predicado LIKE
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
ms.openlocfilehash: 63410b78b6d0b7ab59dd74b9f69fe57fe498c6ea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483519"
---
# <a name="like-predicate-limitations"></a>Limitações do predicado LIKE
Se os dados em uma coluna forem maiores que 255 caracteres, a comparação LIKE será baseada apenas nos primeiros 255 caracteres.  
  
 Um LIKE usado em um procedimento só tem suporte com padrões constantes. Os drivers do banco de dados de desktop dão suporte ao SQL-92 como correspondência de padrões.  
  
 Não há suporte para o uso de uma cláusula escape em um predicado LIKE.  
  
 Uma comparação LIKE não deve ser executada em uma coluna que contém dados de um tipo de dados numérico ou flutuante. Os resultados podem ser imprevisíveis. Para obter mais informações, consulte o *Guia do programador do Microsoft Jet mecanismo de banco de dados*.
