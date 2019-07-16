---
title: SQL dinâmico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], dynamic SQL
- SQL statements [ODBC], embedded SQL
- dynamic SQL [ODBC]
- SQL [ODBC], dynamic SQL
- embedded SQL [ODBC]
ms.assetid: 0bfb9ab7-9c15-4433-93bc-bad8b6c9d287
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 131abdd4a401e336ccd78ca79fdf6666b1911fee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915451"
---
# <a name="dynamic-sql"></a>SQL dinâmico
Embora o SQL estático funciona bem em muitas situações, há uma classe de aplicativos no qual o acesso a dados não pode ser determinado com antecedência. Por exemplo, suponha que uma planilha permite que o usuário insira uma consulta, que envia a planilha para o DBMS para recuperar dados. O conteúdo dessa consulta, obviamente, não pode ser conhecido para o programador quando o programa de planilha é gravado.  
  
 Para resolver esse problema, a planilha usa um formulário do embedded SQL chamado SQL dinâmico. Ao contrário de instruções SQL estáticas, o que são codificados no programa, instruções SQL dinâmicas podem ser criadas em tempo de execução e colocadas em uma variável de host da cadeia de caracteres. Eles são então enviados para o DBMS para processamento. Como o DBMS deve gerar um plano de acesso em tempo de execução para instruções SQL dinâmicas, o SQL dinâmico é geralmente mais lento do que o SQL estático. Quando um programa que contém instruções SQL dinâmicas é compilado, as instruções SQL dinâmicas não são eliminadas do programa, como no SQL estático. Em vez disso, elas serão substituídas por uma chamada de função que passa a instrução para o DBMS; instruções SQL estáticas no mesmo programa são tratadas normalmente.  
  
 É a maneira mais simples para executar uma instrução SQL dinâmica com uma instrução EXECUTE imediata. Essa instrução passa a instrução SQL para o DBMS para compilação e execução.  
  
 Uma desvantagem da instrução EXECUTE imediato é que o DBMS deve percorrer cada uma das cinco etapas de processamento de uma instrução SQL cada vez que a instrução é executada. A sobrecarga envolvida nesse processo pode ser significativa, se muitas instruções são executadas dinamicamente e é um desperdício se essas instruções são semelhantes. Para resolver essa situação, o SQL dinâmico oferece uma forma otimizada de execução chamada execução preparada, que usa as seguintes etapas:  
  
1.  O programa constrói uma instrução SQL em um buffer, assim como faz para a instrução EXECUTE imediata. Em vez de variáveis de host, um ponto de interrogação (?) podem ser substituído por uma constante em qualquer lugar no texto da instrução para indicar que um valor para a constante será fornecido posteriormente. O ponto de interrogação é chamado como um marcador de parâmetro.  
  
2.  O programa passa a instrução SQL para o DBMS com a instrução PREPARE, que solicita que o DBMS analisar, validar e otimizar a instrução e gerar uma execução planejá-la. O programa, em seguida, usa uma instrução EXECUTE (não uma instrução EXECUTE IMMEDIATE) para executar a instrução PREPARE em um momento posterior. Ele passa os valores de parâmetro para a instrução através de uma estrutura de dados especial chamada de área de dados SQL ou SQLDA.  
  
3.  O programa pode usar a instrução EXECUTE repetidamente, fornecendo valores de parâmetros diferentes sempre que a instrução dinâmica é executada.  
  
 Execução preparada ainda não é o mesmo SQL estático. No SQL estático, as quatro primeiras etapas de processamento de uma instrução SQL ocorrem em tempo de compilação. Na execução preparada, essas etapas ainda ocorrem em tempo de execução, mas elas são executadas apenas uma vez. execução do plano ocorre somente quando EXECUTE é chamado. Isso ajuda a eliminar algumas das desvantagens de desempenho inerentes na arquitetura do SQL dinâmico. A ilustração a seguir mostra as diferenças entre SQL estático, dinâmico SQL com execução imediata e SQL dinâmico com a execução preparada.
