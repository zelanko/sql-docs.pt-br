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
manager: craigg
ms.openlocfilehash: 14d9eb18a5c6c3cbd62cea0c668f3c53f8da48f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626674"
---
# <a name="ddl-statements"></a>Instruções DDL
Instruções de Definition Language (DDL) de dados podem variar muito entre DBMSs. SQL ODBC define as instruções para as operações de definição de dados mais comuns: criar e Descartar tabelas, índices e exibições; alterando tabelas; e conceder e revogar privilégios. Todas as outras instruções DDL são específico da fonte de dados. Portanto, os aplicativos interoperáveis não podem executar algumas operações de definição de dados. Em geral, isso não é um problema, porque essas operações tendem a ser altamente específicas do DBMS e são melhor esquerda para o software de administração de banco de dados proprietário fornecidos com a maioria dos DBMSs ou o programa de instalação fornecido com o driver.  
  
 Outro problema na definição de dados é esse tipo de dados nomes podem variar muito entre DBMSs. Em vez de definir os nomes de tipo de dados padrão e forçando drivers convertê-las em nomes específicos de DBMS, **SQLGetTypeInfo** fornece uma maneira para os aplicativos descobrir os nomes de tipo de dados específicos de DBMS. Aplicativos interoperáveis devem usar esses nomes em instruções SQL para criar e alterar as tabelas; os nomes listados na [apêndice c: SQL gramática](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), e [tipos de dados do apêndice d:](../../../odbc/reference/appendixes/appendix-d-data-types.md), são apenas exemplos.
