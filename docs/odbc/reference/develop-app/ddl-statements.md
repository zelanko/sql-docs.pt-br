---
title: Declarações de DDL | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cae06efe6dd11e651e8553fa5c1004c2fa145478
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302987"
---
# <a name="ddl-statements"></a>Instruções DDL
As instruções ddl (Data Definition Language, linguagem de definição de dados) variam tremendamente entre dbmss. O ODBC SQL define as instruções para as operações de definição de dados mais comuns: criação e queda de tabelas, índices e visualizações; alterar tabelas; e concedendo e revogando privilégios. Todas as outras instruções de DDL são específicas da fonte de dados. Portanto, os aplicativos interoperáveis não podem realizar algumas operações de definição de dados. Em geral, isso não é um problema, pois tais operações tendem a ser altamente específicas do DBMS e são melhor deixadas para o software de administração de banco de dados proprietário enviado com a maioria dos DBMSs ou o programa de configuração enviado com o driver.  
  
 Outro problema na definição de dados é que os nomes de tipos de dados variam tremendamente entre os DBMSs. Em vez de definir nomes de tipo de dados padrão e forçar os drivers a convertê-los em nomes específicos do DBMS, **o SQLGetTypeInfo** fornece uma maneira de os aplicativos descobrirem nomes de tipos de dados específicos do DBMS. Os aplicativos interoperáveis devem usar esses nomes em instruções SQL para criar e alterar tabelas; os nomes listados no [apêndice C: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)e [Apêndice D: Tipos de Dados,](../../../odbc/reference/appendixes/appendix-d-data-types.md)são apenas exemplos.
