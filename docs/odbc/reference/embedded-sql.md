---
title: SQL incorporado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], embedded SQL
- ODBC [ODBC], SQL
- embedded SQL [ODBC]
ms.assetid: 8eee3527-f225-4aa2-bd18-a16bd3ab0fb7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ad6fd2753d026f026d72a7aa8f68d5d48ce03cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306669"
---
# <a name="embedded-sql"></a>SQL inserido
A primeira técnica para enviar instruções SQL para o DBMS é incorporada SQL. Como o SQL não usa variáveis e demonstrações de controle de fluxo, muitas vezes é usado como uma sublinguagem de banco de dados que pode ser adicionada a um programa escrito em uma linguagem de programação convencional, como C ou COBOL. Esta é uma idéia central de SQL incorporado: colocar declarações SQL em um programa escrito em uma linguagem de programação de host. Resumidamente, as seguintes técnicas são usadas para incorporar instruções SQL em um idioma host:  
  
-   As instruções SQL incorporadas são processadas por um pré-compilador SQL especial. Todas as instruções SQL começam com um introdutor e terminam com um exterminador, ambos sinalizam a instrução SQL para o pré-compilador. O introdutor e o exterminador variam com a linguagem do hospedeiro. Por exemplo, o introdutor é "EXEC SQL" em C e "&SQL" em MUMPS, e o exterminador é um ponto e vírgula (;) em C e um parêntese direito em MUMPS.  
  
-   As variáveis do programa de aplicativo, chamadas variáveis host, podem ser usadas em declarações SQL incorporadas onde as constantes forem permitidas. Estes podem ser usados na entrada para adaptar uma declaração SQL a uma situação específica e na saída para receber os resultados de uma consulta.  
  
-   As consultas que retornam uma única linha de dados são tratadas com uma declaração select singleton; esta declaração especifica tanto a consulta quanto as variáveis host em que retornar dados.  
  
-   As consultas que retornam várias linhas de dados são tratadas com cursores. Um cursor mantém o controle da linha atual dentro de um conjunto de resultados. A declaração DECLARE CURSOR define a consulta, a declaração OPEN inicia o processamento da consulta, a declaração FETCH recupera sucessivas linhas de dados e a declaração CLOSE encerra o processamento da consulta.  
  
-   Enquanto um cursor estiver aberto, as instruções de exclusão posicionadas e posicionadas podem ser usadas para atualizar ou excluir a linha atualmente selecionada pelo cursor.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Exemplo de SQL inserido](../../odbc/reference/embedded-sql-example.md)  
  
-   [Compilando um programa SQL inserido](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [SQL estático](../../odbc/reference/static-sql.md)  
  
-   [SQL dinâmico](../../odbc/reference/dynamic-sql.md)
