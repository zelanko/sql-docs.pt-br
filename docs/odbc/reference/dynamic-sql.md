---
title: SQL Dinâmico | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56419723540114f122be2582f0de7c7e7d0c54f3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306684"
---
# <a name="dynamic-sql"></a>SQL dinâmico
Embora o SQL estático funcione bem em muitas situações, há uma classe de aplicativos em que o acesso aos dados não pode ser determinado com antecedência. Por exemplo, suponha que uma planilha permita que um usuário insira uma consulta, que a planilha então envia ao DBMS para recuperar dados. O conteúdo desta consulta obviamente não pode ser conhecido pelo programador quando o programa de planilha é escrito.  
  
 Para resolver esse problema, a planilha usa uma forma de SQL embarcada chamada SQL dinâmico. Ao contrário das instruções estáticas de SQL, que são codificadas no programa, as instruções SQL dinâmicas podem ser construídas em tempo de execução e colocadas em uma variável host de seqüência de strings. Em seguida, são enviados ao DBMS para processamento. Como o DBMS deve gerar um plano de acesso em tempo de execução para demonstrações SQL dinâmicas, o SQL dinâmico é geralmente mais lento do que o SQL estático. Quando um programa contendo instruções SQL dinâmicas é compilado, as instruções SQL dinâmicas não são retiradas do programa, como no SQL estático. Em vez disso, eles são substituídos por uma chamada de função que passa a declaração para o DBMS; As instruções Estáticas SQL no mesmo programa são tratadas normalmente.  
  
 A maneira mais simples de executar uma declaração SQL dinâmica é com uma declaração EXECUTE IMMEDIATE. Esta declaração passa a declaração SQL para o DBMS para compilação e execução.  
  
 Uma desvantagem da declaração EXECUTE IMMEDIATE é que o DBMS deve passar por cada uma das cinco etapas de processamento de uma declaração SQL cada vez que a declaração é executada. A sobrecarga envolvida neste processo pode ser significativa se muitas declarações forem executadas dinamicamente, e é um desperdício se essas declarações forem semelhantes. Para lidar com essa situação, o SQL dinâmico oferece uma forma otimizada de execução chamada execução preparada, que utiliza as seguintes etapas:  
  
1.  O programa constrói uma declaração SQL em um buffer, assim como faz para a declaração EXECUTE IMMEDIATE. Em vez de variáveis de host, um ponto de interrogação (?) pode ser substituído por uma constante em qualquer lugar do texto da declaração para indicar que um valor para a constante será fornecido mais tarde. O ponto de interrogação é chamado de marcador de parâmetro.  
  
2.  O programa passa a declaração SQL para o DBMS com uma declaração PREPARATÓRIA, que solicita que o DBMS analise, valide e otimize a declaração e gere um plano de execução para ele. Em seguida, o programa usa uma declaração EXECUTE (não uma declaração EXECUTE IMMEDIATE) para executar a declaração PREPARE-se posteriormente. Ele passa valores de parâmetros para a declaração através de uma estrutura de dados especial chamada SQL Data Area ou SQLDA.  
  
3.  O programa pode usar a declaração EXECUTE repetidamente, fornecendo diferentes valores de parâmetro cada vez que a declaração dinâmica é executada.  
  
 Execução preparada ainda não é o mesmo que SQL estático. No SQL estático, as quatro primeiras etapas do processamento de uma declaração SQL ocorrem no momento da compilação. Na execução preparada, essas etapas ainda ocorrem em tempo de execução, mas são realizadas apenas uma vez; execução do plano só ocorre quando EXECUTE é chamado. Isso ajuda a eliminar algumas das desvantagens de desempenho inerentes à arquitetura do SQL dinâmico. A próxima ilustração mostra as diferenças entre SQL estático, SQL dinâmico com execução imediata e SQL dinâmico com execução preparada.
