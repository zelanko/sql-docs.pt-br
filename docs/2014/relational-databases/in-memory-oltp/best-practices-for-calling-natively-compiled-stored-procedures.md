---
title: Práticas recomendadas para chamar procedimentos armazenados compilados nativamente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f39fc1c7-cfec-4a95-97f6-6b95954694bb
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 5439f539e126a64cff92065e049da359e89345b4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119519"
---
# <a name="best-practices-for-calling-natively-compiled-stored-procedures"></a>Práticas recomendadas para chamar procedimentos armazenados compilados nativamente
  Estes são os procedimentos armazenados compilados nativamente:  
  
-   Geralmente usados em partes essenciais do desempenho de um aplicativo.  
  
-   Executados com frequência.  
  
-   Espera-se que sejam muito rápidos.  
  
 O benefício em termos de desempenho com o uso de um procedimento armazenado compilado nativamente aumenta com o crescente número de linhas e a quantidade de lógica que é processada pelo procedimento. Por exemplo, um procedimento armazenado compilado nativamente exibirá o melhor desempenho se ele usar um ou mais dos seguintes itens:  
  
-   Agregação.  
  
-   Junções de loops aninhados.  
  
-   Operações de seleção, inserção, atualização e exclusão com várias instruções.  
  
-   Expressões complexas.  
  
-   Lógica de procedimento, como instruções condicionais e loops.  
  
 Se você precisa processar apenas uma única linha, usar um procedimento armazenado compilado nativamente talvez não traga um benefício em termos de desempenho.  
  
 Para evitar que o servidor precise mapear nomes de parâmetro e converter tipos:  
  
-   Faça a correspondência dos tipos dos parâmetros passados para o procedimento com os tipos contidos na definição de procedimento.  
  
-   Use parâmetros ordinais (sem nome) ao chamar procedimentos armazenados compilados nativamente. Para uma execução mais eficiente, não use parâmetros nomeados.  
  
 O uso de parâmetros nomeados (ineficientes) com procedimentos armazenados compilados nativamente poderá ser detectado com o XEvent `hekaton_slow_parameter_passing`, com `reason=named_parameters`.  
  
 Da mesma forma, você pode detectar o uso de tipos incompatíveis através do mesmo XEvent `hekaton_slow_parameter_passing`, com `reason=parameter_conversion`.  
  
 Como você precisará implementar uma lógica de repetição ao usar tabelas com otimização de memória (em vários cenários) e precisará respeitar determinadas limitações de recurso, talvez queira criar um procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado por wrapper. Para obter um exemplo, consulte [diretrizes para lógica de repetição para transações em tabelas com otimização de memória](memory-optimized-tables.md).  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados compilados nativamente](natively-compiled-stored-procedures.md)  
  
  