---
description: SQL inserido
title: SQL inserido | Microsoft Docs
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
ms.openlocfilehash: 7b52c5a87d1df03460a833a27fcb5523b80cd1f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487409"
---
# <a name="embedded-sql"></a>SQL inserido
A primeira técnica para enviar instruções SQL para o DBMS é inserida no SQL. Como o SQL não usa variáveis e instruções de controle de fluxo, ele é frequentemente usado como uma sublinguagem de banco de dados que pode ser adicionada a um programa escrito em uma linguagem de programação convencional, como C ou COBOL. Esta é uma ideia central de SQL inserido: colocando instruções SQL em um programa escrito em uma linguagem de programação de host. Resumidamente, as seguintes técnicas são usadas para inserir instruções SQL em um idioma de host:  
  
-   Instruções SQL inseridas são processadas por um SQL PreCompiler especial. Todas as instruções SQL começam com um apresentador e terminam com um terminador, ambos sinalizam a instrução SQL para o pré-compilador. O apresentador e o terminador variam de acordo com o idioma do host. Por exemplo, o apresentador é "EXEC SQL" em C e "&SQL (" em MUMPS, e o terminador é um ponto-e-vírgula (;) em C e um parêntese direito em MUMPS.  
  
-   Variáveis do programa de aplicativo, chamadas de variáveis de host, podem ser usadas em instruções SQL inseridas sempre que forem permitidas constantes. Eles podem ser usados na entrada para personalizar uma instrução SQL para uma situação específica e na saída para receber os resultados de uma consulta.  
  
-   As consultas que retornam uma única linha de dados são manipuladas com uma instrução SELECT singleton; Essa instrução especifica a consulta e as variáveis de host nas quais retornar dados.  
  
-   As consultas que retornam várias linhas de dados são tratadas com cursores. Um cursor mantém o controle da linha atual em um conjunto de resultados. A instrução DECLARE CURSOR define a consulta, a instrução OPEN começa o processamento da consulta, a instrução FETCH recupera linhas sucessivas de dados e a instrução CLOSE encerra o processamento da consulta.  
  
-   Enquanto um cursor está aberto, as instruções DELETE de atualização e posicionadas posicionadas podem ser usadas para atualizar ou excluir a linha selecionada no momento pelo cursor.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Exemplo de SQL inserido](../../odbc/reference/embedded-sql-example.md)  
  
-   [Compilando um programa SQL inserido](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [SQL estático](../../odbc/reference/static-sql.md)  
  
-   [SQL dinâmico](../../odbc/reference/dynamic-sql.md)
