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
ms.openlocfilehash: 9100405c91387faa66b714a94b8259167ae31899
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267653"
---
# <a name="ddl-statements"></a>Instruções DDL
Instruções de Definition Language (DDL) de dados podem variar muito entre DBMSs. SQL ODBC define as instruções para as operações de definição de dados mais comuns: criar e Descartar tabelas, índices e exibições; alterando tabelas; e conceder e revogar privilégios. Todas as outras instruções DDL são específicos da fonte de dados. Portanto, os aplicativos interoperáveis não podem executar algumas operações de definição de dados. Em geral, isso não é um problema, porque essas operações tendem a ser altamente específicas do DBMS e são melhor esquerda para o software de administração de banco de dados proprietário fornecidos com a maioria dos DBMSs ou o programa de instalação fornecido com o driver.  
  
 Outro problema na definição de dados é esse tipo de dados nomes podem variar muito entre DBMSs. Em vez de definir os nomes de tipo de dados padrão e forçando drivers convertê-las em nomes específicos de DBMS, **SQLGetTypeInfo** fornece uma maneira para os aplicativos descobrir os nomes de tipo de dados específicos de DBMS. Aplicativos interoperáveis devem usar esses nomes em instruções SQL para criar e alterar as tabelas; os nomes listados na [apêndice c: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), e [apêndice d: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md), são apenas exemplos.
