---
title: "Instruções DDL | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], DDL statements
- DDL statements [ODBC]
ms.assetid: 96ac9859-5976-4b06-ae1f-2fec3231e266
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4ebd19e39919265d2161927056bb9a4ebb9d55c2
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="ddl-statements"></a>Instruções DDL
Instruções de Definition Language (DDL) de dados podem variar muito entre DBMSs. SQL ODBC define instruções para as operações de definição de dados mais comuns: criar e remover tabelas, índices e exibições; alterando tabelas; conceder e revogar privilégios. Todas as outras instruções DDL são específico da fonte de dados. Portanto, os aplicativos interoperáveis não é possível executar algumas operações de definição de dados. Em geral, isso não é um problema, porque essas operações tendem a ser altamente específicas do DBMS e são mais à esquerda para o software de administração de banco de dados proprietário acompanha DBMSs maioria dos ou o programa de instalação fornecido com o driver.  
  
 Outro problema na definição de dados é nomes podem variar muito entre DBMSs esse tipo de dados. Em vez de definir nomes de tipo de dados padrão e forçar os drivers para convertê-los para nomes específicos de DBMS, **SQLGetTypeInfo** fornece uma maneira de aplicativos descobrir nomes de tipo de dados DBMS específico. Aplicativos interoperáveis devem usar esses nomes de instruções SQL para criar e alterar tabelas; os nomes listados na [gramática de SQL do apêndice c:](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), e [tipos de dados do apêndice d:](../../../odbc/reference/appendixes/appendix-d-data-types.md), são apenas exemplos.

