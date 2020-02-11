---
title: Compilando um programa SQL inserido | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- compiling embedded SQL programs [ODBC]
- embedded SQL [ODBC]
ms.assetid: 9e94146a-5b80-4a01-b586-1e03ff05b9ac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9ef460a7d004227e34e0043223abdf3769c92520
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135659"
---
# <a name="compiling-an-embedded-sql-program"></a>Compilar um programa SQL inserido
Como um programa SQL inserido contém uma combinação de instruções de linguagem de host e SQL, ele não pode ser enviado diretamente a um compilador para o idioma do host. Em vez disso, ele é compilado por meio de um processo de várias etapas. Embora esse processo seja diferente do produto para o produto, as etapas são aproximadamente as mesmas para todos os produtos.  
  
 Esta ilustração mostra as etapas necessárias para compilar um programa SQL inserido.  
  
 ![Etapas para compilar um programa SQL inserido](../../odbc/reference/media/pr02.gif "pr02")  
  
 Cinco etapas estão envolvidas na compilação de um programa SQL inserido:  
  
1.  O programa SQL inserido é enviado para o pré-compilador do SQL, uma ferramenta de programação. O pré-compilador examina o programa, localiza as instruções SQL inseridas e as processa. Um pré-compilador diferente é necessário para cada linguagem de programação com suporte do DBMS. Os produtos DBMS normalmente oferecem pré-compiladores para uma ou mais linguagens, incluindo C, Pascal, COBOL, Fortran, Ada, PL/I e várias linguagens de assembly.  
  
2.  O pré-compilador produz dois arquivos de saída. O primeiro arquivo é o arquivo de origem, extraído de suas instruções SQL inseridas. Em seu lugar, o pré-compilador substitui chamadas a rotinas de DBMS proprietárias que fornecem o link de tempo de execução entre o programa e o DBMS. Normalmente, os nomes e as sequências de chamada dessas rotinas são conhecidos apenas para o pré-compilador e o DBMS; Eles não são uma interface pública para o DBMS. O segundo arquivo é uma cópia de todas as instruções SQL inseridas usadas no programa. Esse arquivo é, às vezes, chamado de um módulo de solicitação de banco de dados ou DBRM.  
  
3.  A saída do arquivo de origem do pré-compilador é enviada para o compilador padrão para a linguagem de programação de host (como um compilador C ou COBOL). O compilador processa o código-fonte e produz o código do objeto como sua saída. Observe que essa etapa não tem nada a ver com o DBMS ou com o SQL.  
  
4.  O vinculador aceita os módulos de objeto gerados pelo compilador, vincula-os com várias rotinas de biblioteca e produz um programa executável. As rotinas de biblioteca vinculadas ao programa executável incluem as rotinas de DBMS proprietárias descritas na etapa 2.  
  
5.  O módulo de solicitação de banco de dados gerado pelo pré-compilador é enviado para um utilitário de ligação especial. Esse utilitário examina as instruções SQL, analisa, valida e otimiza-as e, em seguida, produz um plano de acesso para cada instrução. O resultado é um plano de acesso combinado para todo o programa, representando uma versão executável das instruções SQL inseridas. O utilitário de associação armazena o plano no banco de dados, normalmente atribuindo-lhe o nome do programa de aplicativo que o usará. Se essa etapa ocorre no momento da compilação ou o tempo de execução depende do DBMS.  
  
 Observe que as etapas usadas para compilar um programa SQL inserido correlacionam-se muito com as etapas descritas anteriormente no [processamento de uma instrução SQL](../../odbc/reference/processing-a-sql-statement.md). Em particular, observe que o pré-compilador separa as instruções SQL do código de idioma do host, e o utilitário de ligação analisa e valida as instruções SQL e cria os planos de acesso. Em DBMSs em que a etapa 5 ocorre no momento da compilação, as quatro primeiras etapas do processamento de uma instrução SQL ocorrem no momento da compilação, enquanto a última etapa (execução) ocorre no tempo de execução. Isso tem o efeito de tornar a execução da consulta nesses DBMS muito rápida.
