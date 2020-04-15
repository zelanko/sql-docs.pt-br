---
title: Compilando um programa SQL incorporado | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb801dc532009410055b67031b3e036cc6b9c3d0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306527"
---
# <a name="compiling-an-embedded-sql-program"></a>Compilar um programa SQL inserido
Como um programa SQL incorporado contém uma mistura de instruções de sql e idioma de host, ele não pode ser submetido diretamente a um compilador para o idioma host. Em vez disso, é compilado através de um processo multipassos. Embora este processo difere de produto para produto, as etapas são aproximadamente as mesmas para todos os produtos.  
  
 Esta ilustração mostra as etapas necessárias para compilar um programa SQL incorporado.  
  
 ![Etapas para compilar um programa SQL inserido](../../odbc/reference/media/pr02.gif "pr02")  
  
 Cinco etapas estão envolvidas na compilação de um programa SQL incorporado:  
  
1.  O programa SQL incorporado é submetido ao pré-compilador SQL, uma ferramenta de programação. O pré-compilador verifica o programa, encontra as instruções SQL incorporadas e as processa. Um pré-compilador diferente é necessário para cada linguagem de programação suportada pelo DBMS. Os produtos DBMS normalmente oferecem precompiladores para um ou mais idiomas, incluindo C, Pascal, COBOL, Fortran, Ada, PL/I e várias línguas de montagem.  
  
2.  O pré-compilador produz dois arquivos de saída. O primeiro arquivo é o arquivo de origem, despojado de suas instruções SQL incorporadas. Em seu lugar, o pré-compilador substitui as chamadas para rotinas dbms proprietárias que fornecem o link de tempo de execução entre o programa e o DBMS. Normalmente, os nomes e as seqüências de chamadas dessas rotinas são conhecidos apenas pelo pré-compilador e pelo DBMS; eles não são uma interface pública para o DBMS. O segundo arquivo é uma cópia de todas as declarações SQL incorporadas usadas no programa. Este arquivo às vezes é chamado de módulo de solicitação de banco de dados, ou DBRM.  
  
3.  A saída do arquivo de origem do pré-compilador é submetida ao compilador padrão para a linguagem de programação do host (como um compilador C ou COBOL). O compilador processa o código-fonte e produz o código do objeto como sua saída. Observe que esta etapa não tem nada a ver com o DBMS ou com o SQL.  
  
4.  O linker aceita os módulos de objeto gerados pelo compilador, os conecta com várias rotinas de biblioteca e produz um programa executável. As rotinas de biblioteca vinculadas ao programa executável incluem as rotinas proprietárias de DBMS descritas na etapa 2.  
  
5.  O módulo de solicitação de banco de dados gerado pelo pré-compilador é submetido a um utilitário de vinculação especial. Este utilitário examina as instruções SQL, analisa, valida e otimiza e produz um plano de acesso para cada declaração. O resultado é um plano de acesso combinado para todo o programa, representando uma versão executável das instruções SQL incorporadas. O utilitário vinculativo armazena o plano no banco de dados, geralmente atribuindo-o o nome do programa de aplicação que irá usá-lo. Se essa etapa ocorre no tempo de compilação ou tempo de execução depende do DBMS.  
  
 Observe que as etapas utilizadas para compilar um programa SQL incorporado se correlacionam muito de perto com as etapas descritas anteriormente no [processamento de uma declaração SQL](../../odbc/reference/processing-a-sql-statement.md). Em particular, observe que o pré-compilador separa as instruções SQL do código de idioma host, e o utilitário de vinculação analisa e valida as instruções SQL e cria os planos de acesso. Em DBMSs, onde a etapa 5 ocorre no momento da compilação, as quatro primeiras etapas do processamento de uma declaração SQL ocorrem no momento da compilação, enquanto a última etapa (execução) ocorre no tempo de execução. Isso tem o efeito de fazer a execução de consulta em tais DBMSs muito rápido.
