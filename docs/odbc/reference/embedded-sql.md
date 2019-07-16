---
title: Embedded SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6a7fa2b3105aedee6cb054c5d5dfa76f3c430f35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915420"
---
# <a name="embedded-sql"></a>SQL inserido
A primeira técnica para enviar instruções SQL para o DBMS é incorporada SQL. Porque o SQL não usa variáveis e instruções de controle de fluxo, ele geralmente é usado como um subidioma do banco de dados que pode ser adicionado a um programa gravado em uma linguagem de programação convencional, como C ou COBOL. Essa é uma ideia central do embedded SQL: colocar instruções SQL em um programa gravado em um host de linguagem de programação. Em resumo, as técnicas a seguir são usadas para inserir instruções SQL em uma linguagem de host:  
  
-   Instruções inseridas do SQL são processadas por um pré-compilador especial do SQL. Todas as instruções SQL começam com um introdutor e terminam com um terminador de que a instrução SQL para o pré-compilador do sinalizador. O terminador e Introdutor variam de acordo com o idioma do host. Por exemplo, o Introdutor é "EXEC SQL" em C e "& SQL (" em MUMPS, e o terminador é um ponto e vírgula (;) em C e um parêntese direito em MUMPS.  
  
-   Variáveis do programa de aplicativo, chamadas de variáveis de host, podem ser usadas em instruções inseridas do SQL onde quer que as constantes são permitidas. Eles podem ser usados na entrada para personalizar uma instrução SQL para uma determinada situação e na saída para receber os resultados de uma consulta.  
  
-   Consultas que retornam uma única linha de dados são tratadas com uma instrução SELECT de singleton; Essa instrução Especifica que a consulta e as variáveis de host no qual retornar dados.  
  
-   Consultas que retornam várias linhas de dados são tratadas com cursores. Um cursor mantém o controle da linha atual dentro de um conjunto de resultados. A instrução DECLARE CURSOR define a consulta, a instrução OPEN inicia o processamento de consulta, a instrução FETCH recupera as linhas sucessivas dos dados e a instrução CLOSE termina o processamento de consulta.  
  
-   Enquanto o cursor estiver aberto, instruções delete posicionadas e atualização posicionadas podem ser usadas para atualizar ou excluir a linha selecionada no momento pelo cursor.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Exemplo de SQL inserido](../../odbc/reference/embedded-sql-example.md)  
  
-   [Compilando um programa SQL inserido](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [SQL estático](../../odbc/reference/static-sql.md)  
  
-   [SQL dinâmico](../../odbc/reference/dynamic-sql.md)
