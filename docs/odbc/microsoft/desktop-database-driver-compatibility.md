---
description: Compatibilidade de driver de banco de dados de área de trabalho
title: Compatibilidade de driver de banco de dados desktop | Microsoft Docs
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
ms.openlocfilehash: 6b15ec35a01b61eef401f217733917a80bbe32b4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340772"
---
# <a name="desktop-database-driver-compatibility"></a>Compatibilidade de driver de banco de dados de área de trabalho
Unicode é um método de codificação de caracteres de software que trata todos os caracteres como tendo uma largura fixa de dois bytes. Esse método é usado como uma alternativa à codificação de caracteres ANSI do Windows, que, por representar caracteres em um byte, é limitado a 256 caracteres. Como o Unicode pode representar mais de 65.000 caracteres, ele acomoda muitas linguagens cujos caracteres não são representados na codificação ANSI.  
  
 O Gerenciador de driver do ODBC 3,5 (ou posterior) está habilitado para Unicode. Isso afeta duas áreas principais: chamadas de função e tipos de dados de cadeia de caracteres. O Gerenciador de driver mapeia os argumentos da cadeia de caracteres da função e os dados de cadeia de caracteres conforme exigido pelo aplicativo e Driver, ambos podem ser habilitados para Unicode ou habilitados para ANSI.  
  
 O Gerenciador de driver do ODBC 3,5 (ou posterior) dá suporte ao uso de um driver Unicode com um aplicativo Unicode e um aplicativo ANSI. Ele também dá suporte ao uso de um driver ANSI com um aplicativo ANSI. O Gerenciador de driver fornece mapeamento limitado de Unicode para ANSI para um aplicativo Unicode que funcione com um driver ANSI. Isso permite o acesso aos bancos de dados Jet 3,5 e ao suporte de todos os tipos de arquivo ISAM existentes.  
  
 Quando um aplicativo ANSI usa o driver de banco de dados da área de trabalho do ODBC 4,0 e acessa o Microsoft Access 4,0 ou posterior, o driver expõe o tipo de dado como SQL_CHAR, SQL_VARCHAR ou SQL_LONGVARCHAR mesmo que o Jet 4,0 dê suporte à versão ampla. As versões mais antigas do Jet não dão suporte a SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR. Essa restrição também se aplica nos casos em que os formatos antigos são usados com o Mecanismo de Banco de Dados Jet 4,0.  
  
 Para obter mais informações sobre problemas de Unicode com o ODBC, consulte [Unicode](../../odbc/reference/develop-app/unicode.md) em considerações de programação.
