---
title: SQL dinâmico | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2020
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa4ac69602761f7c2a8d28e56db76bbfc39fc753
ms.sourcegitcommit: dc6ea6665cd2fb58a940c722e86299396b329fec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84423250"
---
# <a name="dynamic-sql"></a>SQL dinâmico
Embora o SQL estático funcione bem em muitas situações, há uma classe de aplicativos em que o acesso a dados não pode ser determinado com antecedência. Por exemplo, suponha que uma planilha permita que um usuário insira uma consulta, que a planilha enviará ao DBMS para recuperar dados. O conteúdo dessa consulta obviamente não pode ser conhecido pelo programador quando o programa de planilha é escrito.  
  
 Para resolver esse problema, a planilha usa um formulário de SQL inserido chamado SQL dinâmico. Ao contrário de instruções SQL estáticas, que são embutidas em código no programa, instruções SQL dinâmicas podem ser criadas em tempo de execução e colocadas em uma variável de host de cadeia de caracteres. Em seguida, eles são enviados para o DBMS para processamento. Como o DBMS deve gerar um plano de acesso em tempo de execução para instruções SQL dinâmicas, o SQL dinâmico geralmente é mais lento do que o SQL estático. Quando um programa que contém instruções SQL dinâmicas é compilado, as instruções SQL dinâmicas não são removidas do programa, como no SQL estático. Em vez disso, eles são substituídos por uma chamada de função que passa a instrução para o DBMS; as instruções SQL estáticas no mesmo programa são tratadas normalmente.  
  
 A maneira mais simples de executar uma instrução SQL dinâmica é com uma instrução EXECUTE IMMEDIATE. Essa instrução passa a instrução SQL para o DBMS para compilação e execução.  
  
 Uma desvantagem da instrução EXECUTE IMMEDIATE é que o DBMS deve passar por cada uma das cinco etapas do processamento de uma instrução SQL cada vez que a instrução é executada. A sobrecarga envolvida nesse processo pode ser significativa se muitas instruções forem executadas dinamicamente, e será um desperdício se essas instruções forem semelhantes. Para resolver essa situação, o SQL dinâmico oferece uma forma otimizada de execução chamada execução preparada, que usa as seguintes etapas:  
  
1.  O programa constrói uma instrução SQL em um buffer, assim como faz para a instrução EXECUTE IMMEDIATE. Em vez de variáveis de host, um ponto de interrogação (?) pode ser substituído por uma constante em qualquer lugar no texto da instrução para indicar que um valor para a constante será fornecido posteriormente. O ponto de interrogação é chamado como um marcador de parâmetro.  
  
2.  O programa passa a instrução SQL para o DBMS com uma instrução PREPARE, que solicita que o DBMS analise, valide e otimize a instrução e gere um plano de execução para ela. Em seguida, o programa usa uma instrução EXECUTE (não uma instrução EXECUTE IMMEDIATE) para executar a instrução PREPARE posteriormente. Ele passa valores de parâmetro para a instrução por meio de uma estrutura de dados especial chamada área de dados SQL ou SQLDA.  
  
3.  O programa pode usar a instrução EXECUTE repetidamente, fornecendo valores de parâmetros diferentes cada vez que a instrução dinâmica é executada.  
  
 A execução preparada ainda não é a mesma que a SQL estática. No SQL estático, as quatro primeiras etapas do processamento de uma instrução SQL ocorrem no momento da compilação. Na execução preparada, essas etapas ainda ocorrem em tempo de execução, mas são executadas apenas uma vez; a execução do plano ocorre somente quando EXECUTE é chamado. Isso ajuda a eliminar algumas das desvantagens de desempenho inerentes à arquitetura do SQL dinâmico.
