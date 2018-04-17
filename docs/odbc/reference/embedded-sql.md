---
title: Embedded SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], embedded SQL
- ODBC [ODBC], SQL
- embedded SQL [ODBC]
ms.assetid: 8eee3527-f225-4aa2-bd18-a16bd3ab0fb7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e7d51d8ae632f30528510448e52fc6c363d066d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="embedded-sql"></a>Embedded SQL
A primeira técnica para enviar instruções SQL para o DBMS é inserida SQL. Como SQL não usam variáveis e instruções de controle de fluxo, ele geralmente é usado como um subidioma do banco de dados que pode ser adicionado a um programa gravado em uma linguagem de programação convencional, como C ou COBOL. Essa é uma ideia central do embedded SQL: colocar instruções SQL em um programa gravado em um host de linguagem de programação. Em resumo, as técnicas a seguir são usadas para inserir instruções SQL em um idioma do host:  
  
-   Instruções de SQL incorporadas são processadas por um pré-compilador especial do SQL. Todas as instruções SQL começam com um introdutor e terminam com um terminador, que a instrução SQL para o pré-compilador do sinalizador. O terminador e Introdutor variam de acordo com o idioma do host. Por exemplo, o Introdutor é "EXEC SQL" C e "& SQL (" em MUMPS, e o terminador é um ponto e vírgula (;) em C e um parêntese direito no MUMPS.  
  
-   Variáveis do programa aplicativo, chamadas de variáveis do host, podem ser usadas em instruções de SQL incorporadas onde constantes são permitidas. Eles podem ser usados na entrada para personalizar uma instrução SQL para uma determinada situação e na saída para receber os resultados de uma consulta.  
  
-   Consultas que retornam uma única linha de dados são tratadas com uma instrução SELECT de singleton; Essa instrução Especifica que a consulta e as variáveis do host no qual retornar dados.  
  
-   Consultas que retornam várias linhas de dados são tratadas com cursores. Um cursor mantém o controle da linha atual em um conjunto de resultados. A instrução DECLARE CURSOR define a consulta, a instrução OPEN inicia o processamento de consulta, a instrução FETCH recupera linhas sucessivas de dados e a instrução CLOSE termina o processamento de consulta.  
  
-   Enquanto o cursor estiver aberto, posicionada instruções update e delete posicionadas podem ser usadas para atualizar ou excluir a linha selecionada atualmente pelo cursor.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Exemplo de SQL inserido](../../odbc/reference/embedded-sql-example.md)  
  
-   [Compilando um programa SQL inserido](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [SQL estático](../../odbc/reference/static-sql.md)  
  
-   [SQL dinâmico](../../odbc/reference/dynamic-sql.md)
