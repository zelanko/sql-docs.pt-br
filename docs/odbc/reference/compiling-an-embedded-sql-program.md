---
title: Compilando um programa SQL inserido | Microsoft Docs
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
- SQL statements [ODBC], embedded SQL
- compiling embedded SQL programs [ODBC]
- embedded SQL [ODBC]
ms.assetid: 9e94146a-5b80-4a01-b586-1e03ff05b9ac
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e4b89a65475b35b50a968b9497c6d90574c6738
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908931"
---
# <a name="compiling-an-embedded-sql-program"></a>Compilando um programa SQL inserido
Como um programa SQL inserido contém uma mistura de instruções de linguagem SQL e host, não podem ser enviado diretamente a um compilador de idioma do host. Em vez disso, ele é compilado por meio de um processo de várias etapas. Embora esse processo é diferente para cada produto, as etapas são aproximadamente o mesmo para todos os produtos.  
  
 Esta ilustração mostra as etapas necessárias para compilar um programa SQL inserido.  
  
 ![Etapas para compilar um programa SQL inserido](../../odbc/reference/media/pr02.gif "pr02")  
  
 Cinco etapas envolvidas ao compilar um programa SQL inserido:  
  
1.  O programa SQL inserido é enviado para o pré-compilador SQL, uma ferramenta de programação. O pré-compilador examina o programa, localiza as instruções SQL inseridas e processá-las. Um pré-compilador diferente é necessária para cada linguagem de programação com suporte do DBMS. Produtos DBMS geralmente oferecem precompilers para um ou mais idiomas, incluindo C, Pascal, COBOL, Fortran, Ada, PL / e várias linguagens de assembly.  
  
2.  O pré-compilador produz dois arquivos de saída. O primeiro arquivo é o arquivo de origem, retirado de suas instruções SQL inseridas. Em seu lugar, o pré-compilador substitui chamadas para rotinas DBMS proprietárias que fornecem o link de tempo de execução entre o programa e o DBMS. Normalmente, os nomes e as sequências de chamada dessas rotinas são conhecidas somente o pré-compilador e DBMS; eles não têm uma interface pública para o DBMS. O segundo arquivo é uma cópia de todas as instruções de SQL incorporadas usada no programa. Esse arquivo também é chamado DBRM ou um módulo de solicitação de banco de dados.  
  
3.  A saída do arquivo de origem do pré-compilador é enviada para o compilador padrão para o host de linguagem (por exemplo, um compilador C ou COBOL) de programação. O compilador processa o código-fonte e gera o código de objeto como sua saída. Observe que esta tabela não tem nada a ver com o DBMS ou SQL.  
  
4.  O vinculador aceita os módulos de objeto gerados pelo compilador, vincula-los com vários rotinas de biblioteca e produz um programa executável. As rotinas de biblioteca vinculadas para o programa executável incluem as rotinas DBMS proprietárias descritas na etapa 2.  
  
5.  O módulo de solicitação de banco de dados gerado pelo pré-compilador é enviado a um utilitário especial de associação. Esse utilitário examina as instruções SQL, analisa, valida e otimiza-las e, em seguida, gera um plano de acesso para cada instrução. O resultado é um plano de acesso combinado para todo o programa, que representa uma versão executável das instruções SQL inseridas. O utilitário de associação armazena o plano no banco de dados, geralmente atribuindo-o nome do programa aplicativo que irá usá-la. Se esta etapa ocorre em tempo de execução ou tempo de compilação depende do DBMS.  
  
 Observe que as etapas usadas para compilar um programa SQL inserido correlacionam em conjunto com as etapas descritas anteriormente na [processar uma instrução SQL](../../odbc/reference/processing-a-sql-statement.md). Em particular, observe que o pré-compilador separa as instruções SQL de código de idioma do host, e o utilitário de associação analisa e valida as instruções SQL e cria os planos de acesso. Em DBMSs onde a etapa 5 ocorre em tempo de compilação, as quatro primeiras etapas de processamento de uma instrução SQL ocorrem em tempo de compilação, enquanto a última etapa (execução) ocorre em tempo de execução. Isso tem o efeito de tornar a execução da consulta em tais DBMSs muito rápidos.
