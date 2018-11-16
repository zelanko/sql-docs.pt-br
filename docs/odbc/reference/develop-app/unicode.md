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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e6201b83b909573476b043cdb1a10543f894def
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51661805"
---
# <a name="unicode"></a>Unicode
O Unicode define a codificação de caracteres em várias linguagens.  
  
 Para obter mais informações sobre o padrão Unicode, consulte [The Unicode Consortium](https://www.unicode.org).  
  
 O Unicode define um conjunto de caracteres universais. Uma página de código ANSI do Windows define um conjunto de caracteres, geralmente contendo caracteres para um idioma. Pode ser mais difícil de escrever um aplicativo que é necessário para usar diferentes páginas de código.  
  
 Não requer uma página de código Unicode. Todos os pontos de código é mapeado para um único caractere em alguns idiomas.  
  
 Atualmente, o Unicode somente codificação que dá suporte a ODBC é UCS-2, que usa um inteiro de 16 bits (comprimento fixo) para representar um caractere. Unicode permite que os aplicativos trabalham em diferentes idiomas.  
  
 O Gerenciador de Driver ODBC 3.5 (ou superior) é habilitado para Unicode. Isso afeta duas áreas principais: chamadas de função e tipos de dados de cadeia de caracteres. Os argumentos de cadeia de caracteres de função do Gerenciador de Driver mapas e dados de cadeia de caracteres, conforme exigido pelo aplicativo e do driver, ambos os quais podem ser habilitado para Unicode ou ANSI habilitados. Essas duas áreas são discutidas em detalhes nas seções, [argumentos da função Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md) e [dados Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 O Gerenciador de Driver ODBC 3.5 (ou superior) oferece suporte ao uso de um driver de Unicode com um aplicativo Unicode e um aplicativo ANSI. Ele também suporta o uso de um driver de ANSI com um aplicativo ANSI. O Gerenciador de Driver fornece o mapeamento de Unicode para ANSI limitado para um aplicativo Unicode trabalhando com um driver de ANSI.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Argumentos da função Unicode](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Dados Unicode](../../../odbc/reference/develop-app/unicode-data.md)
