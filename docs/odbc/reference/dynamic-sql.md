---
title: SQL dinâmico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], dynamic SQL
- SQL statements [ODBC], embedded SQL
- dynamic SQL [ODBC]
- SQL [ODBC], dynamic SQL
- embedded SQL [ODBC]
ms.assetid: 0bfb9ab7-9c15-4433-93bc-bad8b6c9d287
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 465f9785436880fce74136dd293abab33d1d2b4c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="dynamic-sql"></a>SQL dinâmico
Embora o SQL estática funciona bem em muitas situações, há uma classe de aplicativos no qual o acesso a dados não pode ser determinado com antecedência. Por exemplo, suponha que uma planilha permite que um usuário insira uma consulta, que envia a planilha para o DBMS para recuperar dados. O conteúdo dessa consulta, obviamente, não pode ser conhecido para o programador quando o programa de planilha é gravado.  
  
 Para resolver esse problema, a planilha usa um formulário do embedded SQL chamado SQL dinâmico. Ao contrário das instruções SQL estáticas, que são codificados no programa, instruções SQL dinâmicas podem ser criadas em tempo de execução e colocadas em uma variável de host de cadeia de caracteres. Em seguida, elas são enviadas para o DBMS para processamento. Como o DBMS deve gerar um plano de acesso em tempo de execução para instruções SQL dinâmicas, SQL dinâmico é geralmente mais lento do que o SQL estático. Quando um programa que contém instruções SQL dinâmicas é compilado, as instruções SQL dinâmicas não são eliminadas do programa, como SQL estático. Em vez disso, elas serão substituídas por uma chamada de função que passa a instrução para o DBMS; instruções SQL estáticas no mesmo programa são tratadas normalmente.  
  
 É a maneira mais simples para executar uma instrução SQL dinâmica com uma instrução EXECUTE imediata. Essa instrução passa a instrução SQL para o DBMS para compilação e execução.  
  
 Uma desvantagem da instrução EXECUTE imediato é que o DBMS devem passar por cada uma das cinco etapas de processamento de uma instrução SQL cada vez que a instrução é executada. A sobrecarga envolvida nesse processo pode ser significativa se muitas instruções são executadas dinamicamente e é desnecessário se essas instruções são semelhantes. Para resolver essa situação, o SQL dinâmico oferece uma forma otimizada de execução chamada execução preparada, que usa as seguintes etapas:  
  
1.  O programa cria uma instrução SQL em um buffer, assim como faz para a instrução EXECUTE imediata. Em vez de variáveis de host, um ponto de interrogação (?) podem ser substituído por uma constante em qualquer lugar no texto da instrução para indicar que um valor para a constante será fornecido posteriormente. O ponto de interrogação é chamado de um marcador de parâmetro.  
  
2.  O programa passa a instrução SQL para o DBMS com a instrução PREPARE, quais solicitações que o DBMS analisar, validar e otimizar a instrução e gerar uma execução de plano para ela. O programa usa uma instrução EXECUTE (não uma instrução EXECUTE IMMEDIATE) para executar a instrução PREPARE mais tarde. Ele passa valores de parâmetro para a instrução através de uma estrutura de dados especial chamada de área de dados do SQL ou sqlda não.  
  
3.  O programa pode usar a instrução EXECUTE repetidamente, fornecendo valores de parâmetros diferentes cada vez que a instrução dinâmica é executada.  
  
 Execução preparada ainda não é o mesmo SQL estático. No SQL estático, as quatro primeiras etapas de processamento de uma instrução SQL ocorrem em tempo de compilação. Na execução preparada, essas etapas ainda ocorrem em tempo de execução, mas elas são executadas apenas uma vez; execução do plano ocorre somente quando EXECUTE é chamado. Isso ajuda a eliminar algumas das desvantagens inerentes à arquitetura do SQL dinâmico de desempenho. A ilustração a seguir mostra as diferenças entre SQL estático, SQL dinâmico com execução imediata e SQL dinâmico com execução preparada.
