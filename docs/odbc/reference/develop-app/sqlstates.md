---
title: SQLSTATEs | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ad31d9fd07e0b9f7bdf633f8ed546331880787c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149036"
---
# <a name="sqlstates"></a>SQLSTATEs
SQLSTATEs fornecem informações detalhadas sobre a causa de um aviso ou erro. Os SQLSTATEs neste manual baseadas nesses encontrada na especificação de CLI IEF/ISO, embora esses SQLSTATEs que começam com mensagens Instantâneas são específicas para ODBC.  
  
 Ao contrário de códigos de retorno, os SQLSTATEs deste manual são diretrizes e drivers não são necessários para retorná-los. Portanto, enquanto os drivers devem retornar o SQLSTATE apropriado para qualquer erro ou aviso, que eles são capazes de detectar, aplicativos não devem contar com esse sempre que ocorrem. Os motivos para essa situação são dois:  
  
-   **Incompletude** embora deste manual lista um grande número de erros e avisos e as possíveis causas para esses erros e avisos, ele não está completo e provavelmente nunca estará; implementações de driver simplesmente variam muito. Qualquer driver específico provavelmente não retornará todos os SQLSTATEs listados neste manual e podem retornar SQLSTATEs não listadas neste manual.  
  
-   **Complexidade** alguns mecanismos de banco de dados - mecanismos de banco de dados relacional particularmente - retornam literalmente milhares de erros e avisos. Os drivers para esses mecanismos são provavelmente não mapear todos esses erros e avisos a serem SQLSTATEs por causa do esforço envolvido, o inexactness dos mapeamentos, o tamanho grande de código resultante e o valor baixo do código resultante, que geralmente retorna programação erros que nunca devem ser encontrados em tempo de execução. Portanto, drivers devem ser mapeado como muitos erros e avisos que parece razoável e certifique-se de mapear esses erros e avisos no qual a lógica do aplicativo podem se basear, como o SQLSTATE 01004 (dados truncados).  
  
 Como SQLSTATEs não são retornados de forma confiável, a maioria dos aplicativos exibi-los apenas para o usuário, juntamente com sua mensagem de diagnóstico associado, geralmente é adaptado para o erro ou aviso que ocorreu e o código de erro nativo. Não há raramente qualquer perda de funcionalidade ao fazer isso, porque os aplicativos não podem basear lógica de programação na maioria dos SQLSTATEs mesmo assim. Por exemplo, suponha **SQLExecDirect** retornará SQLSTATE 42000 (sintaxe ou violação de acesso). Se a instrução SQL que causou este erro é embutido em código ou criada pelo aplicativo, isso é um erro de programação e o código precisa ser corrigido. Se a instrução SQL é inserida pelo usuário, esse é um erro de usuário e o aplicativo fez tudo o que é possível por meio de informando ao usuário do problema.  
  
 Quando aplicativos basear a lógica de programação em SQLSTATEs, deve estar preparados para o SQLSTATE não deve ser retornado ou um SQLSTATE diferente a serem retornados. Exatamente qual SQLSTATEs são retornados de forma confiável podem ser com base apenas na experiência com vários drivers. No entanto, a diretriz geral é que SQLSTATEs para erros que ocorrem no driver ou do Gerenciador de Driver, em vez de fonte de dados, são mais probabilidade de ser retornado de forma confiável. Por exemplo, a maioria dos drivers provavelmente retornará SQLSTATE HYC00 (recurso opcional não implementado), enquanto os drivers menos provavelmente retornam SQLSTATE 42021 (a coluna já existe).  
  
 As seguir SQLSTATEs indicam erros de tempo de execução ou avisos e são bons candidatos no qual basear a lógica de programação. No entanto, não há nenhuma garantia de que todos os drivers de retorná-los.  
  
-   01004 (dados truncados)  
  
-   01S02 (valor de opção alterado)  
  
-   HY008 (operação cancelada)  
  
-   HYC00 (recurso opcional não implementado)  
  
-   HYT00 (tempo limite expirado)  
  
 SQLSTATE HYC00 (recurso opcional não implementado) é significativo principalmente porque é a única maneira na qual um aplicativo pode determinar se um driver dá suporte a um determinado atributo de instrução ou a conexão.  
  
 Para obter uma lista completa de SQLSTATEs e quais funções retornarão-los, consulte [apêndice a: Códigos de erro ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md). Para obter uma explicação detalhada das condições sob as quais cada função pode retornar um SQLSTATE específico, consulte essa função.
