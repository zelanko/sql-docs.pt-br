---
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
ms.openlocfilehash: 9824e76cebabb6f5f84505292801a0094e359f0f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302437"
---
# <a name="unicode"></a>Unicode
Unicode define codificação para caracteres em muitos idiomas.  
  
 Para obter mais informações sobre a norma Unicode, consulte [o Consórcio Unicode](https://www.unicode.org).  
  
 Unicode define um conjunto de caracteres universal. Uma página de código DO Windows ANSI define um conjunto de caracteres, normalmente contendo caracteres para um idioma. Pode ser mais difícil escrever um aplicativo que é necessário para usar diferentes páginas de código.  
  
 Unicode não requer uma página de código. Cada ponto de código é mapeado para um único caractere em algum idioma.  
  
 Atualmente, a única codificação Unicode que o ODBC suporta é o UCS-2, que usa um inteiro de 16 bits (comprimento fixo) para representar um caractere. O Unicode permite que os aplicativos funcionem em diferentes idiomas.  
  
 O Gerenciador de Driver ODBC 3.5 (ou superior) é habilitado para Unicode. Isso afeta duas áreas principais: chamadas de função e tipos de dados de string. O Driver Manager mapeia argumentos de seqüência de funções e dados de seqüência conforme exigido pelo aplicativo e pelo driver, ambos podem ser habilitados para Unicode ou habilitados para ANSI. Essas duas áreas são discutidas detalhadamente nas seções, [Argumentos de Função Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md) e [Dados Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 O Gerenciador de Driver ODBC 3.5 (ou superior) suporta o uso de um driver Unicode com um aplicativo Unicode e um aplicativo ANSI. Ele também suporta o uso de um driver ANSI com um aplicativo ANSI. O Driver Manager fornece mapeamento Unicode-to-ANSI limitado para um aplicativo Unicode que funciona com um driver ANSI.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Argumentos da função Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Dados Unicode](../../../odbc/reference/develop-app/unicode-data.md)
