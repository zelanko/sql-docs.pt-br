---
description: Unicode
title: Unicode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC]
- Unicode [ODBC], about Unicode
ms.assetid: 113e1c9a-8333-4805-86f2-e4b57ab816a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a09a2647175d2b19aa44f1458d0ae8c4ef4565c7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424428"
---
# <a name="unicode"></a>Unicode
O Unicode define a codificação para caracteres em muitas linguagens.  
  
 Para obter mais informações sobre o padrão Unicode, consulte [o consórcio Unicode](https://www.unicode.org).  
  
 O Unicode define um conjunto de caracteres universais. Uma página de código ANSI do Windows define um conjunto de caracteres, normalmente contendo caracteres para um idioma. Pode ser mais difícil escrever um aplicativo necessário para usar páginas de código diferentes.  
  
 O Unicode não requer uma página de código. Cada ponto de código é mapeado para um único caractere em algum idioma.  
  
 Atualmente, a única codificação Unicode com a qual o ODBC dá suporte é o UCS-2, que usa um inteiro de 16 bits (comprimento fixo) para representar um caractere. O Unicode permite que os aplicativos funcionem em diferentes idiomas.  
  
 O Gerenciador de driver ODBC 3,5 (ou superior) está habilitado para Unicode. Isso afeta duas áreas principais: chamadas de função e tipos de dados de cadeia de caracteres. O Gerenciador de driver mapeia os argumentos da cadeia de caracteres da função e os dados de cadeia de caracteres conforme exigido pelo aplicativo e Driver, ambos podem ser habilitados para Unicode ou habilitados para ANSI. Essas duas áreas são discutidas em detalhes nas seções, [argumentos de função Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md) e [dados Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 O Gerenciador de driver ODBC 3,5 (ou superior) dá suporte ao uso de um driver Unicode com um aplicativo Unicode e um aplicativo ANSI. Ele também dá suporte ao uso de um driver ANSI com um aplicativo ANSI. O Gerenciador de driver fornece mapeamento limitado de Unicode para ANSI para um aplicativo Unicode que funcione com um driver ANSI.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Argumentos da função Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Dados Unicode](../../../odbc/reference/develop-app/unicode-data.md)
