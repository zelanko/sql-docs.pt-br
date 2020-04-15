---
title: Compatibilidade do driver do banco de dados do desktop | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], Unicode
- Unicode [ODBC], desktop database drivers
- ODBC desktop database drivers [ODBC], Unicode
- backward compatibility [ODBC], Unicode
- desktop database drivers [ODBC], Unicode
- Jet-based ODBC drivers [ODBC], Unicode
ms.assetid: dd695638-1a0b-4e27-8a6a-9510ebb5a5ee
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89eea7ab112eaefdc73c7cbc72ee3555797c7efd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303516"
---
# <a name="desktop-database-driver-compatibility"></a>Compatibilidade de driver de banco de dados de área de trabalho
Unicode é um método de codificação de caracteres de software que trata todos os caracteres como tendo uma largura fixa de dois bytes. Este método é usado como uma alternativa à codificação de caracteres Windows ANSI, que, por representar caracteres em um byte, é limitada a 256 caracteres. Como o Unicode pode representar mais de 65.000 caracteres, ele acomoda muitas linguagens cujos caracteres não estão representados na codificação ANSI.  
  
 O Gerenciador de Driver ODBC 3.5 (ou posterior) é habilitado para Unicode. Isso afeta duas áreas principais: chamadas de função e tipos de dados de string. O Driver Manager mapeia argumentos de seqüência de funções e dados de seqüência conforme exigido pelo aplicativo e pelo driver, ambos podem ser habilitados para Unicode ou habilitados para ANSI.  
  
 O Gerenciador de Driver ODBC 3.5 (ou posterior) suporta o uso de um driver Unicode com um aplicativo Unicode e um aplicativo ANSI. Ele também suporta o uso de um driver ANSI com um aplicativo ANSI. O Driver Manager fornece mapeamento Unicode-to-ANSI limitado para um aplicativo Unicode que funciona com um driver ANSI. Isso permite o acesso aos bancos de dados jet 3.5 e suporte de todos os tipos de arquivos ISAM existentes.  
  
 Quando um aplicativo ANSI usa o ODBC Desktop Database Driver 4.0 e acessa o Microsoft Access 4.0 ou posterior, o driver expõe o tipo de dados como SQL_CHAR, SQL_VARCHAR ou SQL_LONGVARCHAR mesmo que o Jet 4.0 suporte a versão ampla. As versões mais antigas do Jet não suportam SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR. Essa restrição também se aplica nos casos em que os formatos antigos são usados com o Jet 4.0 Database Engine.  
  
 Para obter mais informações sobre os problemas do Unicode com o ODBC, consulte [Unicode](../../odbc/reference/develop-app/unicode.md) em Considerações de Programação.
