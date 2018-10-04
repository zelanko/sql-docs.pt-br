---
title: Quando usar procedimentos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], about procedures
ms.assetid: 7dc9e327-dd54-4b10-9f66-9ef5c074f122
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 82e71e6849902eb2f02423560c534056112a139a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47854510"
---
# <a name="when-to-use-procedures"></a>Quando usar procedimentos
Há uma série de vantagens no uso de procedimentos, tudo com base no fato de que usando procedimentos move instruções SQL do aplicativo para a fonte de dados. O restante do aplicativo é uma chamada de procedimento interoperável. Essas vantagens incluem:  
  
-   **Desempenho** procedimentos geralmente são a maneira mais rápida para executar instruções SQL. Como a execução preparada, a instrução é compilada e executada em duas etapas separadas. Ao contrário de execução preparado, procedimentos são executados somente em tempo de execução. Eles são compilados em um momento diferente.  
  
-   **Regras de negócio** um *regra de negócio* é uma regra sobre a maneira na qual uma empresa faz negócios. Por exemplo, somente alguém com o título do vendedor pode ter permissão para adicionar novas ordens de venda. Colocando essas regras em procedimentos permite que empresas individuais personalizar aplicativos verticais reescrevendo os procedimentos chamados pelo aplicativo sem ter que modificar o código do aplicativo. Por exemplo, um aplicativo de entrada de pedidos pode chamar o procedimento **InsertOrder** com um número fixo de parâmetros; exatamente como **InsertOrder** é implementado pode variar da empresa.  
  
-   **Replaceability** intimamente relacionados à colocação de regras de negócio nos procedimentos é o fato de que os procedimentos podem ser substituídos sem recompilar o aplicativo. Se uma regra de negócio for alterado depois que uma empresa tem comprou e instalou um aplicativo, a empresa pode alterar o procedimento que contém essa regra. Do ponto de vista do aplicativo, nada foi alterado; ainda, ele chama um procedimento específico para realizar uma tarefa em particular.  
  
-   **Específicos de DBMS SQL** procedimentos fornecem uma maneira para os aplicativos explorar o SQL específicas do DBMS e ainda permanecer interoperável. Por exemplo, um procedimento em um DBMS que dá suporte a instruções de controle de fluxo no SQL pode interceptar e se recuperar de erros, enquanto um procedimento em um DBMS que não oferece suporte a instruções de controle de fluxo pode simplesmente retornar um erro.  
  
-   **Procedimentos sobrevivem transações** em algumas fontes de dados, os planos de acesso para instruções preparadas tudo em uma conexão são excluídos quando uma transação é confirmada ou revertida. Colocando instruções SQL em procedimentos, que são armazenados permanentemente na fonte de dados, as instruções de sobrevivem a transação. Se os procedimentos sobrevivem preparada, parcialmente preparados, ou despreparados é específico do DBMS.  
  
-   **Separar o desenvolvimento** procedimentos podem ser desenvolvidos separadamente do restante do aplicativo. Em grandes empresas, isso pode oferecer uma maneira de explorar ainda mais as habilidades de programadores altamente especializados. Em outras palavras, os programadores de aplicativos podem escrever um código de interface do usuário e os programadores do banco de dados podem gravar procedimentos.  
  
 Procedimentos são geralmente usados pelos aplicativos personalizados e verticais. Esses aplicativos tendem a realizar tarefas fixas e é possível para chamadas de procedimento de codificar neles. Por exemplo, um aplicativo de entrada de pedidos pode chamar os procedimentos **InsertOrder**, **DeleteOrder**, **UpdateOrder**, e **GetOrders** .  
  
 Há poucos motivos para chamar procedimentos de aplicativos genéricos. Geralmente, os procedimentos são escritos para executar uma tarefa no contexto de um aplicativo específico e, portanto nenhum uso para aplicativos genéricos. Por exemplo, uma planilha não tem motivo para chamar o **InsertOrder** procedimento que acabei de mencionar. Além disso, aplicativos genéricos não devem criar procedimentos no tempo de execução na esperança de fornecer execução mais rápida de instrução; não é apenas isso provavelmente ser mais lento do que a execução preparada ou direta, ela também exige que as instruções SQL específicas do DBMS.  
  
 Uma exceção a isso é os ambientes de desenvolvimento de aplicativos, que geralmente fornecem uma maneira para os programadores a criar instruções SQL que executam procedimentos e podem fornecer uma maneira para os programadores a procedimentos de teste. Essa chamada de ambientes **SQLProcedures** aos procedimentos disponíveis da lista e **SQLProcedureColumns** para listar a entrada, entrada/saída e parâmetros de saída, o procedimento retornar valor e as colunas de Nenhum conjunto de resultados foi criado por um procedimento. No entanto, esses procedimentos devem ser desenvolvidos com antecedência em cada fonte de dados; Isso requer a instruções SQL específicas do DBMS.  
  
 Há três desvantagens principais para o uso de procedimentos. A primeira é que procedimentos devem ser gravados e compilados para cada DBMS com a qual o aplicativo será executado. Embora isso não seja um problema para aplicativos personalizados, ele pode aumentar significativamente o tempo de desenvolvimento e manutenção de aplicativos verticais projetado para ser executado com um número de DBMSs.  
  
 A segunda desvantagem é que muitos DBMSs têm suporte para procedimentos. Novamente, isso é mais provável de ser um problema para aplicativos verticais projetado para ser executado com um número de DBMSs. Para determinar se há suporte para procedimentos, um aplicativo chama **SQLGetInfo** com a opção SQL_PROCEDURES.  
  
 A desvantagem de terceiro, que é especialmente adequada para ambientes de desenvolvimento de aplicativos, é que o ODBC não define uma gramática padrão para a criação de procedimentos. Ou seja, embora os aplicativos podem chamar procedimentos interoperably, eles não é possível criá-los interoperably.
