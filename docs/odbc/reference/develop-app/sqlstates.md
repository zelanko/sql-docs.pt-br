---
title: SQLSTATEs | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], sqlstates
- SQLSTATE [ODBC]
ms.assetid: f29fff2e-3d09-4a8c-a2f9-2059062cbebf
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 92e36a33efeade353f77f476bfc9ef12ce53608b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlstates"></a>SQLSTATEs
SQLSTATEs fornecem informações detalhadas sobre a causa de um aviso ou erro. SQLSTATEs neste manual são baseadas nos encontrada na especificação ISO/IEF CLI, embora esses SQLSTATEs que começam com mensagens Instantâneas são específicas para ODBC.  
  
 Ao contrário de códigos de retorno, SQLSTATEs neste manual são diretrizes e drivers não são necessários para retorná-las. Portanto, enquanto drivers devem retornar o SQLSTATE apropriado para qualquer erro ou aviso são capazes de detectar, aplicativos não devem contar com essa sempre que ocorrem. As razões para essa situação são dois:  
  
-   **Incompletude** Embora este guia lista um grande número de erros e avisos e as possíveis causas para esses erros e avisos, ele não está completo e provavelmente nunca será; implementações de driver simplesmente variam muito. Qualquer driver específico provavelmente não retornará todas as SQLSTATEs listados neste manual e podem retornar SQLSTATEs não listadas neste manual.  
  
-   **Complexidade** alguns mecanismos de banco de dados — mecanismos de banco de dados relacional particularmente — retornar literalmente milhares de erros e avisos. Os drivers para esses mecanismos são provavelmente não mapear todos esses erros e avisos para SQLSTATEs devido o esforço envolvido, inexactness dos mapeamentos, o tamanho grande do código resultante e o valor baixo do código resultante, que geralmente retorna programação erros que nunca devem ser encontrados em tempo de execução. Portanto, drivers devem ser mapeado como muitos erros e avisos que parece razoável e mapeie os erros e avisos no qual a lógica do aplicativo podem estar baseados, como o SQLSTATE 01004 (dados truncados).  
  
 Como SQLSTATEs não são retornados com confiança, a maioria dos aplicativos exibem apenas-los para o usuário junto com sua mensagem de diagnóstico associado, que geralmente é personalizado para o erro ou aviso ocorreu e o código de erro nativo. Não há raramente qualquer perda de funcionalidade ao fazer isso, porque os aplicativos não é possível basear lógica de programação na maioria dos SQLSTATEs mesmo assim. Por exemplo, suponha que **SQLExecDirect** retornará SQLSTATE 42000 (sintaxe ou violação de acesso). Se a instrução SQL que causou este erro é embutido ou criada pelo aplicativo, este é um erro de programação e o código precisa ser corrigido. Se a instrução SQL é inserida pelo usuário, esse é um erro de usuário e o aplicativo tiver feito tudo o que é possível, informando ao usuário do problema.  
  
 Quando aplicativos basear a lógica de programação em SQLSTATEs, eles devem estar preparados para o SQLSTATE não deve ser retornado ou um SQLSTATE diferente a ser retornado. Exatamente qual SQLSTATEs são retornados de forma confiável podem se basear somente experiência com vários drivers. No entanto, uma diretriz geral é que SQLSTATEs para erros que ocorrem no driver ou o Gerenciador de Driver, em vez de fonte de dados, têm mais probabilidade de ser retornado de forma confiável. Por exemplo, a maioria dos drivers provavelmente retornará SQLSTATE HYC00 (recurso opcional não implementado), enquanto drivers menos provavelmente retornam SQLSTATE 42021 (já existe uma coluna).  
  
 As seguir SQLSTATEs indicam erros ou avisos e são bons candidatos para basear a lógica de programação. No entanto, não há nenhuma garantia de que todos os drivers de retorná-los.  
  
-   01004 (dados truncados)  
  
-   01S02 (valor da opção alterado)  
  
-   HY008 (operação cancelada)  
  
-   HYC00 (recurso opcional não implementado)  
  
-   HYT00 (tempo limite esgotado)  
  
 SQLSTATE HYC00 (recurso opcional não implementado) é particularmente importante porque ele é o único modo no qual um aplicativo pode determinar se um driver oferece suporte a um determinado atributo de instrução ou a conexão.  
  
 Para obter uma lista completa de SQLSTATEs e quais funções retornarão-los, consulte [códigos de erro de ODBC do apêndice a:](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md). Para obter uma explicação detalhada sobre as condições sob as quais cada função pode retornar um SQLSTATE específico, consulte essa função.
