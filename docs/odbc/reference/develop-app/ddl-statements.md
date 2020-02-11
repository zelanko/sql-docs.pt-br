---
title: Instruções DDL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], DDL statements
- DDL statements [ODBC]
ms.assetid: 96ac9859-5976-4b06-ae1f-2fec3231e266
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97541c9d594b282b871cb7869d0e8c2d2224205d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076862"
---
# <a name="ddl-statements"></a>Instruções DDL
As instruções DDL (linguagem de definição de dados) variam enormemente entre DBMSs. O ODBC SQL define instruções para as operações de definição de dados mais comuns: Criando e descartando tabelas, índices e exibições; alterando tabelas; e concessão e revogação de privilégios. Todas as outras instruções DDL são específicas da fonte de dados. Portanto, os aplicativos interoperáveis não podem executar algumas operações de definição de dados. Em geral, isso não é um problema, pois essas operações tendem a ser altamente específicas de DBMS e são mais bem deixadas para o software de administração de banco de dados proprietário fornecido com a maioria dos DBMSs ou o programa de instalação fornecido com o driver.  
  
 Outro problema na definição de dados é que os nomes de tipo de dados variam enormemente entre os DBMSs. Em vez de definir nomes de tipo de dados padrão e forçar drivers para convertê-los em nomes específicos do DBMS, o **SQLGetTypeInfo** fornece uma maneira para os aplicativos descobrirem nomes de tipo de dados específicos do DBMS. Aplicativos interoperáveis devem usar esses nomes em instruções SQL para criar e alterar tabelas; os nomes listados no [Apêndice C: SQL Grammar](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)e [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md), são apenas exemplos.
