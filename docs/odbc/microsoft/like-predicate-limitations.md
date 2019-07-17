---
title: Limitações do predicado LIKE | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8cd3cebfcf20df2f8a3a786ea66fd28dd76307c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119705"
---
# <a name="like-predicate-limitations"></a>Limitações do predicado LIKE
Se os dados em uma coluna forem maiores que 255 caracteres, a comparação LIKE se baseará apenas os primeiros 255 caracteres.  
  
 Um tipo usado em um procedimento é compatível apenas com padrões constantes. Os Drivers de banco de dados de área de trabalho dão suporte a SQL-92, como correspondência de padrões.  
  
 Não há suporte para o uso de uma cláusula de escape em um predicado LIKE.  
  
 Uma comparação LIKE não podem ser realizada em uma coluna que contém dados de um tipo de dados numéricos ou de float. Os resultados podem ser imprevisíveis. Para obter mais informações, consulte o *guia do programador do Microsoft Jet banco de dados Engine*.
