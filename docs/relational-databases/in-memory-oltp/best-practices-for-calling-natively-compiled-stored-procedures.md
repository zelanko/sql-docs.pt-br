---
title: Práticas recomendadas para chamar procedimentos armazenados compilados nativamente | Microsoft Docs
ms.custom: ''
ms.date: 03/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f39fc1c7-cfec-4a95-97f6-6b95954694bb
caps.latest.revision: 8
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: a9aa49591ccf91880a9f64153d42001114954443
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39564450"
---
# <a name="best-practices-for-calling-natively-compiled-stored-procedures"></a>Práticas recomendadas para chamar procedimentos armazenados compilados nativamente
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
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
  
 Ineficiências em parâmetros com procedimentos armazenados compilados nativamente podem ser detectadas com o XEvent **natively_compiled_proc_slow_parameter_passing**:
 - Tipos incompatíveis: **reason=parameter_conversion**
 - Parâmetros nomeados: **reason=named_parameters**
 - Valores PADRÃO: **reason=default** 
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
