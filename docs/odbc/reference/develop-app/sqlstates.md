---
title: SQLSTATES | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], sqlstates
- SQLSTATE [ODBC]
ms.assetid: f29fff2e-3d09-4a8c-a2f9-2059062cbebf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be4bca929b8d48c301c6e71917503387004a6ec5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299723"
---
# <a name="sqlstates"></a>SQLSTATEs
Os SQLSTATEs fornecem informações detalhadas sobre a causa de um aviso ou erro. Os SQLSTATEs neste manual são baseados nos encontrados na especificação ISO/IEF CLI, embora os SQLSTATEs que começam com IM sejam específicos do ODBC.  
  
 Ao contrário dos códigos de retorno, os SQLSTATEs neste manual são diretrizes, e os drivers não são obrigados a devolvê-los. Portanto, enquanto os motoristas devem retornar o SQLSTATE adequado para qualquer erro ou aviso que eles são capazes de detectar, os aplicativos não devem contar com isso sempre ocorrendo. As razões para esta situação são duplas:  
  
-   **Incompletude** Embora este manual liste um grande número de erros e avisos e possíveis causas para esses erros e avisos, ele não está completo e provavelmente nunca será; implementações de driver simplesmente variam muito. Qualquer driver dado provavelmente não retornará todos os SQLSTATEs listados neste manual e poderá retornar SQLSTATEs não listados neste manual.  
  
-   **Complexidade** Alguns mecanismos de banco de dados - particularmente motores de banco de dados relacionais - retornam literalmente milhares de erros e avisos. É improvável que os drivers para tais motores mapeiem todos esses erros e avisos para SQLSTATEs devido ao esforço envolvido, a inexatidão dos mapeamentos, o grande tamanho do código resultante e o baixo valor do código resultante, que muitas vezes retorna erros de programação que nunca devem ser encontrados em tempo de execução. Portanto, os drivers devem mapear tantos erros e avisos quanto parecer razoável e não se esqueça de mapear esses erros e avisos sobre quais lógicas de aplicativos podem ser baseadas, como sQLSTATE 01004 (dados truncados).  
  
 Como os SQLSTATEs não são devolvidos de forma confiável, a maioria dos aplicativos apenas os exibe para o usuário juntamente com sua mensagem de diagnóstico associada, que muitas vezes é adaptada ao erro ou aviso específico que ocorreu, e código de erro nativo. Raramente há qualquer perda de funcionalidade em fazer isso, porque os aplicativos não podem basear a lógica de programação na maioria dos SQLSTATEs de qualquer maneira. Por exemplo, suponha que **o SQLExecDirect** devolva o SQLSTATE 42000 (erro de sintaxe ou violação de acesso). Se a declaração SQL que causou esse erro for codificada ou construída pelo aplicativo, este é um erro de programação e o código precisa ser corrigido. Se a declaração SQL for inserida pelo usuário, este é um erro do usuário e o aplicativo fez tudo o que é possível informando o usuário do problema.  
  
 Quando as aplicações fazem a lógica de programação base em SQLSTATEs, elas devem estar preparadas para que o SQLSTATE não seja devolvido ou para que um SQLSTATE diferente seja devolvido. Exatamente quais SQLSTATEs são devolvidos de forma confiável podem ser baseados apenas na experiência com inúmeros drivers. No entanto, uma diretriz geral é que os SQLSTATEs para erros que ocorrem no driver ou driver manager, ao contrário da fonte de dados, são mais propensos a serem devolvidos de forma confiável. Por exemplo, a maioria dos drivers provavelmente retorna SQLSTATE HYC00 (recurso opcional não implementado), enquanto menos drivers provavelmente retornam SQLSTATE 42021 (A coluna já existe).  
  
 Os SQLSTATEs a seguir indicam erros ou avisos de tempo de execução e são bons candidatos para basear a lógica de programação. No entanto, não há garantia de que todos os motoristas os devolvam.  
  
-   01004 (Dados truncados)  
  
-   01S02 (Valor da opção alterado)  
  
-   HY008 (Operação cancelada)  
  
-   HYC00 (Recurso opcional não implementado)  
  
-   HYT00 (Tempo expirado)  
  
 SQLSTATE HYC00 (recurso opcional não implementado) é particularmente significativo porque é a única maneira pela qual um aplicativo pode determinar se um driver suporta uma declaração ou atributo de conexão particular.  
  
 Para obter uma lista completa de SQLSTATEs e quais funções os retornam, consulte [Apêndice A: Códigos de erro ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md). Para uma explicação detalhada das condições sob as quais cada função pode retornar um SQLSTATE específico, consulte essa função.
