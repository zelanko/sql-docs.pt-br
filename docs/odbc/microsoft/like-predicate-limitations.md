---
title: COMO limitações predicadas | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298956"
---
# <a name="like-predicate-limitations"></a>Limitações do predicado LIKE
Se os dados em uma coluna forem maiores que 255 caracteres, a comparação LIKE será baseada apenas nos primeiros 255 caracteres.  
  
 Um LIKE usado em um procedimento é suportado apenas com padrões constantes. Os drivers de banco de dados da área de trabalho suportam a correspondência de padrões SQL-92 LIKE.  
  
 O uso de uma cláusula de escape em um predicado LIKE não é suportado.  
  
 Uma comparação LIKE não deve ser realizada em uma coluna contendo dados de um tipo de dados numérico ou flutuante. Os resultados podem ser imprevisíveis. Para obter mais informações, consulte o *Guia do Programador do Motor do Banco de Dados microsoft jet*.
