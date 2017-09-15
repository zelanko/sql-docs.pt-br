---
title: "Compatibilidade de Driver do banco de dados de área de trabalho | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], Unicode
- Unicode [ODBC], desktop database drivers
- ODBC desktop database drivers [ODBC], Unicode
- backward compatibility [ODBC], Unicode
- desktop database drivers [ODBC], Unicode
- Jet-based ODBC drivers [ODBC], Unicode
ms.assetid: dd695638-1a0b-4e27-8a6a-9510ebb5a5ee
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 34b9221b117819988e44196cee0f04578e85d436
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="desktop-database-driver-compatibility"></a>Compatibilidade de Driver do banco de dados de área de trabalho
Unicode é um método de codificação de caracteres de software trata todos os caracteres como tendo uma largura fixa de dois bytes. Esse método é usado como uma alternativa para codificação de caracteres ANSI do Windows, que, pois ela representa caracteres em um byte, é limitada a 256 caracteres. Como Unicode pode representar mais de 65.000 caracteres, ele acomoda muitos idiomas cujos caracteres não são representados em codificação de ANSI.  
  
 O Gerenciador de Driver ODBC 3.5 (ou posterior) está habilitado para Unicode. Isso afeta duas áreas principais: chamadas de função e tipos de dados de cadeia de caracteres. Os argumentos de cadeia de caracteres de função do Gerenciador de Driver mapas e dados de cadeia de caracteres, conforme exigido pelo aplicativo e do driver, ambos podem ser habilitado para Unicode ou ANSI habilitado.  
  
 O Gerenciador de Driver ODBC 3.5 (ou posterior) oferece suporte ao uso de um driver de Unicode com um aplicativo Unicode e um aplicativo de ANSI. Ele também suporta o uso de um driver de ANSI em um aplicativo de ANSI. O Gerenciador de Driver fornece mapeamento de Unicode para ANSI limitado para um aplicativo Unicode trabalhando com um driver de ANSI. Isso permite o acesso aos bancos de dados Jet 3.5 e suporte de todos os tipos de arquivo ISAM existentes.  
  
 Quando um aplicativo ANSI usa o Driver de banco de dados ODBC Desktop 4.0 e acessa o Microsoft Access 4.0 ou posterior, o driver expõe o tipo de dados como SQL_CHAR, SQL_VARCHAR ou SQL_LONGVARCHAR, embora o Jet 4.0 suporta a versão ampla. Não dão suporte a versões mais antigas do Jet SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR. Essa restrição também se aplica em casos em que os formatos antigos são usados com o mecanismo de banco de dados do Jet 4.0.  
  
 Para obter mais informações sobre problemas de Unicode com ODBC, consulte [Unicode](../../odbc/reference/develop-app/unicode.md) em considerações de programação.
