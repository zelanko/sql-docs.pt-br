---
title: Quando usar procedimentos | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], about procedures
ms.assetid: 7dc9e327-dd54-4b10-9f66-9ef5c074f122
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a7bae5e984d66d8b71a9e4b84708f3ea126c1e0b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="when-to-use-procedures"></a>Quando usar procedimentos
Há inúmeras vantagens de usar os procedimentos, todos com base no fato de que usando procedimentos move instruções SQL do aplicativo para a fonte de dados. O restante do aplicativo é uma chamada de procedimento interoperável. Essas vantagens incluem:  
  
-   **Desempenho** procedimentos geralmente são a maneira mais rápida para executar instruções SQL. Como uma execução preparada, a instrução é compilada e executada em duas etapas separadas. Ao contrário de execução preparada, procedimentos são executados somente em tempo de execução. Eles são compilados em um horário diferente.  
  
-   **Regras de negócio** um *regra de negócio* é uma regra sobre a forma em que uma empresa faz negócios. Por exemplo, somente uma pessoa com o título do vendedor poderá adicionar novas ordens de venda. Colocar essas regras em procedimentos permite que empresas individuais para personalizar aplicativos verticais, recriando os procedimentos chamados pelo aplicativo sem a necessidade de modificar o código do aplicativo. Por exemplo, um aplicativo de entrada de pedidos pode chamar o procedimento **InsertOrder** com um número fixo de parâmetros, exatamente como **InsertOrder** é implementada pode variar da empresa.  
  
-   **Replaceability** estreitamente relacionados à colocação de regras de negócios em procedimentos é o fato de que os procedimentos podem ser substituídos sem recompilar o aplicativo. Se uma regra de negócio for alterado depois que uma empresa tem comprar e instalar um aplicativo, a empresa pode alterar o procedimento que contém a regra. Do ponto de vista do aplicativo, nada foi alterado; ele ainda chama um procedimento para realizar uma tarefa específica.  
  
-   **SQL DBMS específico** procedimentos fornecem uma maneira de aplicativos explorar SQL específicas do DBMS e ainda permanecer interoperável. Por exemplo, um procedimento em um DBMS que dá suporte a instruções de controle de fluxo em SQL pode interceptar e recuperar de erros, enquanto um procedimento em um DBMS que não dá suporte a instruções de controle de fluxo pode simplesmente retornar um erro.  
  
-   **Procedimentos sobrevivem transações** em algumas fontes de dados, os planos de acesso para instruções preparadas tudo em uma conexão são excluídos quando uma transação é confirmada ou revertida. Colocando em instruções SQL em procedimentos, que são armazenados permanentemente na fonte de dados, as instruções sobrevivem a transação. Se os procedimentos sobrevivem preparada, parcialmente preparados, ou estado DESPREPARADA é específica do DBMS.  
  
-   **Separar desenvolvimento** procedimentos podem ser desenvolvidos separadamente do restante do aplicativo. Em grandes empresas, isso pode fornecer uma maneira de explorar mais as habilidades de programadores altamente especializadas. Em outras palavras, os programadores de aplicativos podem escrever código de interface do usuário e programadores de banco de dados podem gravar procedimentos.  
  
 Os procedimentos são geralmente usados por aplicativos verticais e personalizados. Esses aplicativos tendem a executar tarefas fixas, e é possível para chamadas de procedimento de embutir em código neles. Por exemplo, um aplicativo de entrada de pedidos pode chamar os procedimentos **InsertOrder**, **DeleteOrder**, **UpdateOrder**, e **GetOrders** .  
  
 Há poucos motivos para chamar procedimentos de aplicativos genéricos. Procedimentos geralmente são gravados para executar uma tarefa no contexto de um aplicativo específico e, portanto não use aplicativos genéricos. Por exemplo, uma planilha não tem nenhum motivo para chamar o **InsertOrder** procedimento mencionados acima. Além disso, aplicativos genéricos não devem criar procedimentos em tempo de execução para tentar fornecer execução mais rápida de instrução; não é apenas nesse provavelmente será mais lento do que a execução direta ou preparada, também é necessário instruções SQL de DBMS específico.  
  
 Uma exceção a isso é ambientes de desenvolvimento de aplicativos, que geralmente fornecem uma maneira para os programadores a criar instruções SQL que executam procedimentos e podem fornecer uma maneira para que os programadores testar procedimentos. Essa chamada de ambientes **SQLProcedures** para procedimentos disponíveis da lista e **SQLProcedureColumns** para listar a entrada, entrada/saída e parâmetros de saída, o procedimento retorna o valor e as colunas de Nenhum conjunto de resultados foi criado por um procedimento. No entanto, esses procedimentos devem ser desenvolvidos com antecedência em cada fonte de dados; fazer isso exige instruções SQL de DBMS específico.  
  
 Há três principais desvantagens procedimentos. A primeira é que procedimentos devem ser escritos e compilados para cada DBMS com a qual o aplicativo será executado. Embora não seja um problema para aplicativos personalizados, ele pode aumentar significativamente o tempo de desenvolvimento e manutenção de aplicativos verticais projetado para ser executado com um número de DBMSs.  
  
 A segunda desvantagem é que muitas DBMSs não dão suporte a procedimentos. Novamente, isso é provavelmente um problema para aplicativos verticais projetado para ser executado com um número de DBMSs. Para determinar se há suporte para procedimentos, um aplicativo chama **SQLGetInfo** com a opção SQL_PROCEDURES.  
  
 A desvantagem de terceira, que é aplicável principalmente a ambientes de desenvolvimento de aplicativos, é que o ODBC não define uma gramática padrão para a criação de procedimentos. Ou seja, embora os aplicativos podem chamar procedimentos interoperably, eles não é possível criá-los interoperably.

