---
description: SQLSTATEs
title: Sqlstates | Microsoft Docs
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
ms.openlocfilehash: b32a965779da1669452e9361e38723e29cfb11ca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476388"
---
# <a name="sqlstates"></a>SQLSTATEs
Os sqlstates fornecem informações detalhadas sobre a causa de um aviso ou erro. Os hiperestados neste manual se baseiam naqueles encontrados na especificação da CLI ISO/IEF, embora esses sqlestados que começam com IM sejam específicos do ODBC.  
  
 Ao contrário dos códigos de retorno, os sqlstates neste manual são diretrizes e os drivers não são necessários para retorná-los. Portanto, embora os drivers devam retornar o SQLSTATE adequado para qualquer erro ou aviso que eles sejam capazes de detectar, os aplicativos não devem contar com isso sempre ocorrendo. As razões para essa situação são duplas:  
  
-   **Inintegridade** Embora este manual liste um grande número de erros e avisos e as possíveis causas desses erros e avisos, ele não está completo e provavelmente nunca será; implementações de driver simplesmente variam muito. Qualquer driver específico provavelmente não retornará todos os sqlstates listados neste manual e poderá retornar sqlstates não listados neste manual.  
  
-   **Complexidade** Alguns mecanismos de banco de dados – especialmente mecanismos de banco de dados relacionais – retornam literalmente milhares de erros e avisos. Os drivers para esses mecanismos são improvável de Mapear todos esses erros e avisos para sqlstates devido ao esforço envolvido, à incerteza dos mapeamentos, ao grande tamanho do código resultante e ao valor baixo do código resultante, que geralmente retorna erros de programação que nunca devem ser encontrados em tempo de execução. Portanto, os drivers devem mapear quantos erros e avisos forem razoáveis e não se esqueça de mapear esses erros e avisos em que a lógica do aplicativo pode ser baseada, como o SQLSTATE 01004 (dados truncados).  
  
 Como os sqlstates não são retornados de forma confiável, a maioria dos aplicativos apenas os exibe para o usuário junto com sua mensagem de diagnóstico associada, que geralmente é adaptada para o erro ou aviso específico que ocorreu e o código de erro nativo. Raramente há perda de funcionalidade para fazer isso, porque os aplicativos não podem basear a lógica de programação na maioria dos sqlstates mesmo assim. Por exemplo, suponha que **SQLExecDirect** retorna SQLSTATE 42000 (erro de sintaxe ou violação de acesso). Se a instrução SQL que causou esse erro for embutida em código ou criada pelo aplicativo, esse será um erro de programação e o código precisará ser corrigido. Se a instrução SQL for inserida pelo usuário, esse será um erro de usuário e o aplicativo terá feito tudo o que é possível ao informar o usuário do problema.  
  
 Quando os aplicativos fazem a lógica de programação base em sqlstates, eles devem estar preparados para que o SQLSTATE não seja retornado ou para que um SQLSTATE diferente seja retornado. Exatamente quais sqlstates são retornados de forma confiável podem se basear apenas na experiência com inúmeros drivers. No entanto, uma diretriz geral é que sqlstates para erros que ocorrem no driver ou no Gerenciador de driver, ao contrário da fonte de dados, têm maior probabilidade de serem retornados de forma confiável. Por exemplo, a maioria dos drivers provavelmente retorna SQLSTATE HYC00 (recurso opcional não implementado), enquanto menos drivers provavelmente retornam SQLSTATE 42021 (a coluna já existe).  
  
 Os sqlstates a seguir indicam erros de tempo de execução ou avisos e são bons candidatos nos quais basear a lógica de programação. No entanto, não há nenhuma garantia de que todos os drivers as retornem.  
  
-   01004 (dados truncados)  
  
-   01S02 (valor da opção alterado)  
  
-   HY008 (operação cancelada)  
  
-   HYC00 (recurso opcional não implementado)  
  
-   HYT00 (tempo limite expirado)  
  
 O SQLSTATE HYC00 (recurso opcional não implementado) é particularmente significativo porque é a única maneira na qual um aplicativo pode determinar se um driver dá suporte a uma instrução ou a um atributo de conexão específico.  
  
 Para obter uma lista completa de sqlstates e quais funções os retornam, consulte o [Apêndice a: códigos de erro ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md). Para obter uma explicação detalhada das condições sob as quais cada função pode retornar um SQLSTATE específico, consulte essa função.
