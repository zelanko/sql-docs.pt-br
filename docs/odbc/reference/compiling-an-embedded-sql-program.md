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
manager: craigg
ms.openlocfilehash: bc8133241ad0b76579e87164350a5c6fe2a39f2e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63186335"
---
# <a name="compiling-an-embedded-sql-program"></a>Compilar um programa SQL inserido
Como um programa SQL inserido contém uma mistura de instruções de linguagem SQL e o host, não podem ser enviado diretamente para um compilador para a linguagem host. Em vez disso, ele é compilado por meio de um processo de várias etapas. Embora esse processo é diferente de produto para produto, as etapas são basicamente as mesmas para todos os produtos.  
  
 Esta ilustração mostra as etapas necessárias para compilar um programa SQL inserido.  
  
 ![Etapas para compilar um programa SQL inserido](../../odbc/reference/media/pr02.gif "pr02")  
  
 Cinco etapas envolvidas na compilação de um programa SQL inserido:  
  
1.  O programa SQL inserido é enviado para o pré-compilador SQL, uma ferramenta de programação. O pré-compilador examina o programa, localiza as instruções SQL inseridas e as processa. Um pré-compilador diferente é necessária para cada linguagem de programação com suporte pelo DBMS. Normalmente, os produtos DBMS oferecem precompilers para um ou mais idiomas, incluindo C, Pascal, COBOL, Fortran, Ada, PL / eu e várias linguagens de assembly.  
  
2.  O pré-compilador produz dois arquivos de saída. O primeiro arquivo é o arquivo de origem, tem suas instruções SQL inseridas. Em seu lugar, o pré-compilador substitui por chamadas para rotinas DBMS proprietárias que fornecem o link de tempo de execução entre o programa e o DBMS. Normalmente, os nomes e as sequências de chamada essas rotinas são conhecidas somente o pré-compilador e o DBMS; eles não são uma interface pública para o DBMS. O segundo arquivo é uma cópia de todas as instruções de SQL inseridas usada no programa. Esse arquivo é chamado, às vezes, um módulo de solicitação do banco de dados ou DBRM.  
  
3.  A saída do arquivo de origem do pré-compilador é enviada para o compilador padrão para o host linguagem (por exemplo, um compilador C ou COBOL) de programação. O compilador processa o código-fonte e produz o código de objeto como sua saída. Observe que essa etapa tem nada a ver com o DBMS ou com o SQL.  
  
4.  O vinculador aceita os módulos de objeto gerados pelo compilador, vincula-os com várias rotinas de biblioteca e produz um programa executável. As rotinas de biblioteca vinculadas ao programa executável incluem as rotinas DBMS proprietárias descritas na etapa 2.  
  
5.  O módulo de solicitação do banco de dados gerado pelo pré-compilador é enviado a um utilitário especial de associação. Esse utilitário examina as instruções SQL, analisa, valida, otimiza-os e, em seguida, produz um plano de acesso para cada instrução. O resultado é um plano de acesso combinado para todo o programa, que representa uma versão executável das instruções SQL inseridas. O utilitário de associação armazena o plano no banco de dados, normalmente, atribuindo a ela o nome do programa aplicativo que irá usá-lo. Se esta etapa ocorre no tempo de execução ou tempo de compilação depende do DBMS.  
  
 Observe que as etapas usadas para compilar um programa SQL inserido de forma bastante aproximada correlacionam com as etapas descritas anteriormente na [processar uma instrução SQL](../../odbc/reference/processing-a-sql-statement.md). Em particular, observe que o pré-compilador separa as instruções SQL a partir do código de idioma do host, e o utilitário de associação analisa e valida as instruções SQL e cria os planos de acesso. Em DBMSs onde a etapa 5 ocorre em tempo de compilação, as quatro primeiras etapas de processamento de uma instrução SQL ocorrem em tempo de compilação, enquanto a última etapa (execução) ocorre em tempo de execução. Isso tem o efeito de tornar a execução da consulta em tais DBMSs muito rápidos.
