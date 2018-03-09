---
title: Unicode | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC]
- Unicode [ODBC], about Unicode
ms.assetid: 113e1c9a-8333-4805-86f2-e4b57ab816a5
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b66efb11afce77a878451b767c1a6db000185f41
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="unicode"></a>Unicode
O Unicode define a codificação de caracteres em vários idiomas.  
  
 Para obter mais informações sobre o padrão Unicode, consulte [Unicode Consortium](http://www.unicode.org).  
  
 Unicode define um conjunto de caracteres universais. Uma página de código ANSI do Windows define um conjunto de caracteres, normalmente com caracteres de um idioma. Pode ser mais difícil de escrever um aplicativo que é necessário para usar páginas de código diferentes.  
  
 Unicode não requer uma página de código. Cada ponto de código é mapeado para um único caractere em alguns idiomas.  
  
 Atualmente, o Unicode somente codificação que dá suporte a ODBC é UCS-2, que usa um inteiro de 16 bits (comprimento fixo) para representar um caractere. Unicode permite que os aplicativos funcionam em idiomas diferentes.  
  
 O Gerenciador de Driver ODBC 3.5 (ou superior) está habilitado para Unicode. Isso afeta duas áreas principais: chamadas de função e tipos de dados de cadeia de caracteres. Os argumentos de cadeia de caracteres de função do Gerenciador de Driver mapas e dados de cadeia de caracteres, conforme exigido pelo aplicativo e do driver, ambos podem ser habilitado para Unicode ou ANSI habilitado. Nessas duas áreas são discutidas em detalhes nas seções, [argumentos da função Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md) e [dados Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 O Gerenciador de Driver ODBC 3.5 (ou superior) oferece suporte ao uso de um driver de Unicode com um aplicativo Unicode e um aplicativo de ANSI. Ele também suporta o uso de um driver de ANSI em um aplicativo de ANSI. O Gerenciador de Driver fornece mapeamento de Unicode para ANSI limitado para um aplicativo Unicode trabalhando com um driver de ANSI.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Argumentos da função Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Dados Unicode](../../../odbc/reference/develop-app/unicode-data.md)
