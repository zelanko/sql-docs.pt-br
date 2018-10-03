---
title: Escolhendo uma gramática SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], SQL grammar
- SQL grammar [ODBC], selecting
ms.assetid: 4e0d189b-e407-47e0-92a9-f9982230dd0e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 670ed0adbbd5ad993af0942d492ee19f75fa9628
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848024"
---
# <a name="choosing-an-sql-grammar"></a>Escolher uma gramática SQL
A primeira decisão a tomar ao construindo instruções SQL é qual gramática para usar. Além das gramáticas disponíveis em vários órgãos de padrões, como Open Group, ANSI e ISO, praticamente todos os fornecedores DBMS define sua própria gramatical, cada uma delas varia um pouco do padrão.  
  
 [Apêndice c: gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), descreve a gramática SQL mínima que devem oferecer suporte a todos os drivers ODBC. Essa gramática é um subconjunto do nível de entrada do SQL-92. Drivers podem dar suporte a gramática adicional de acordo com o intermediário, completo ou FIPS 127-2 níveis de transição definidos pelo SQL-92. Para obter mais informações, consulte [gramática do mínimo de SQL](../../../odbc/reference/appendixes/sql-minimum-grammar.md) no Apêndice c: gramática do SQL e SQL-92.  
  
 Apêndice C também define *sequências de escape* que contém a gramática padrão para recursos de linguagem geralmente disponíveis, como junções externas, que não são cobertas pela gramática de SQL-92. Para obter mais informações, consulte [sequências de Escape de ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) na gramática de SQL do apêndice c:, e [sequências de Escape](../../../odbc/reference/develop-app/escape-sequences.md), mais adiante nesta seção.  
  
 A gramática escolhido afeta como o driver processa a instrução. Drivers modifique SQL-92 SQL e as sequências de escape definidas pelo ODBC para SQL específicas do DBMS. Como a maioria das gramáticas SQL se baseiam em um ou mais dos vários padrões, a maioria dos drivers fazer pouco ou nenhum para atender a esse requisito. Ele geralmente consiste apenas pesquisando as sequências de escape definidas pelo ODBC e substituí-los com a gramática específica do DBMS. Quando um driver encontra gramática não reconhece, ele pressupõe que a gramática específicos de DBMS e passa a instrução SQL sem modificação à fonte de dados para execução.  
  
 Portanto, realmente há duas opções de gramática usar: a gramática de SQL-92 (e o sequências de escape de ODBC) e uma gramática específicos de DBMS. Dos dois, somente a gramática de SQL-92 é interoperável, portanto, todos os aplicativos interoperáveis devem usá-lo. Aplicativos que não são interoperáveis podem usar a gramática de SQL-92 ou uma gramática específicos de DBMS. Específicos de DBMS gramáticas tem duas vantagens: eles podem explorar os recursos não cobertos por SQL-92, e eles são um pouco mais rápidos porque o driver não precisa modificá-los. O segundo recurso pode ser imposto parcialmente, definindo o atributo de instrução SQL_ATTR_NOSCAN, que interrompe o driver de pesquisando e substituindo as sequências de escape.  
  
 Se a gramática de SQL-92 for usada, o aplicativo pode descobrir como ele é modificado pelo driver chamando **SQLNativeSql**. Isso geralmente é útil ao depurar aplicativos. **SQLNativeSql** aceita uma instrução SQL e retorna-a depois que o driver foi modificado. Como essa função está em nível de conformidade de interface de núcleo, ele é compatível com todos os drivers.
