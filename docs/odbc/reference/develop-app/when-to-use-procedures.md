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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31aeea226bc8c8aa41f748d1d9a97d55147c4d67
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81289093"
---
# <a name="when-to-use-procedures"></a>Quando usar procedimentos
Há uma série de vantagens no uso de procedimentos, tudo com base no fato de que o uso de procedimentos move instruções SQL do aplicativo para a fonte de dados. O que resta no aplicativo é uma chamada de procedimento interoperável. Essas vantagens incluem:  
  
-   **Desempenho** do Os procedimentos são geralmente a maneira mais rápida de executar instruções SQL. Como a execução preparada, a instrução é compilada e executada em duas etapas separadas. Diferentemente da execução preparada, os procedimentos são executados somente em tempo de execução. Eles são compilados em um momento diferente.  
  
-   **Regras de negócio** Uma *regra de negócio* é uma regra sobre a maneira como uma empresa faz negócios. Por exemplo, somente alguém com o título Sales vendedor pode ter permissão para adicionar novas ordens de venda. Colocar essas regras em procedimentos permite que empresas individuais personalizem aplicativos verticais reescrevendo os procedimentos chamados pelo aplicativo sem precisar modificar o código do aplicativo. Por exemplo, um aplicativo de entrada de pedido pode chamar o procedimento **InsertOrder** com um número fixo de parâmetros; exatamente como a **InsertOrder** é implementada pode variar de acordo com a empresa.  
  
-   **Reposicionamento** Muito relacionado à colocação de regras de negócio em procedimentos é o fato de que os procedimentos podem ser substituídos sem a recompilação do aplicativo. Se uma regra de negócio for alterada depois que uma empresa tiver comprado e instalado um aplicativo, a empresa poderá alterar o procedimento que contém essa regra. Do ponto de vista do aplicativo, nada mudou; Ele ainda chama um procedimento específico para realizar uma tarefa específica.  
  
-   **SQL específico do DBMS** Os procedimentos fornecem uma maneira de os aplicativos explorarem o SQL específico do DBMS e ainda permanecerem interoperáveis. Por exemplo, um procedimento em um DBMS que dá suporte a instruções de controle de fluxo no SQL pode interceptar e recuperar de erros, enquanto um procedimento em um DBMS que não dá suporte a instruções de controle de fluxo pode simplesmente retornar um erro.  
  
-   Os **procedimentos sobrevivem a transações** Em algumas fontes de dados, os planos de acesso para todas as instruções preparadas em uma conexão são excluídos quando uma transação é confirmada ou revertida. Colocando instruções SQL em procedimentos, que são armazenados permanentemente na fonte de dados, as instruções sobrevivem à transação. Se os procedimentos sobrevivem em um estado preparado, parcialmente preparado ou não preparado são específicos do DBMS.  
  
-   **Desenvolvimento separado** Os procedimentos podem ser desenvolvidos separadamente do restante do aplicativo. Em grandes corporações, isso pode fornecer uma maneira de explorar ainda mais as habilidades de programadores altamente especializados. Em outras palavras, os programadores de aplicativos podem escrever código de interface do usuário e os programadores de banco de dados podem escrever procedimentos.  
  
 Os procedimentos são geralmente usados por aplicativos verticais e personalizados. Esses aplicativos tendem a executar tarefas fixas, e é possível embutir em código as chamadas de procedimento neles. Por exemplo, um aplicativo de entrada de pedidos pode chamar os procedimentos **InsertOrder**, **DeleteOrder**, **UpdateOrder**e **GetOrders**.  
  
 Há pouco motivo para chamar procedimentos de aplicativos genéricos. Os procedimentos geralmente são escritos para executar uma tarefa no contexto de um aplicativo específico e, portanto, não têm uso de aplicativos genéricos. Por exemplo, uma planilha não tem razão para chamar o procedimento **InsertOrder** que acabamos de mencionar. Além disso, aplicativos genéricos não devem construir procedimentos em tempo de execução na esperança de fornecer uma execução de instrução mais rápida; Não só é provável que isso seja mais lento do que a execução preparada ou direta, ele também requer instruções SQL específicas do DBMS.  
  
 Uma exceção a isso são os ambientes de desenvolvimento de aplicativos, que geralmente fornecem uma maneira para os programadores criarem instruções SQL que executam procedimentos e podem fornecer uma maneira para os programadores testarem os procedimentos. Esses ambientes chamam **SQLProcedures** para listar os procedimentos disponíveis e **SQLProcedureColumns** para listar os parâmetros de entrada, entrada/saída e saída, o valor de retorno do procedimento e as colunas de quaisquer conjuntos de resultados criados por um procedimento. No entanto, esses procedimentos devem ser desenvolvidos com antecedência em cada fonte de dados; Isso requer instruções SQL específicas do DBMS.  
  
 Há três desvantagens principais no uso de procedimentos. A primeira é que os procedimentos devem ser escritos e compilados para cada DBMS com o qual o aplicativo será executado. Embora isso não seja um problema para aplicativos personalizados, ele pode aumentar significativamente o tempo de desenvolvimento e manutenção para aplicativos verticais projetados para serem executados com vários DBMSs.  
  
 A segunda desvantagem é que muitos DBMSs não dão suporte a procedimentos. Mais uma vez, é mais provável que seja um problema para aplicativos verticais projetados para execução com vários DBMSs. Para determinar se há suporte para os procedimentos, um aplicativo chama **SQLGetInfo** com a opção SQL_PROCEDURES.  
  
 A terceira desvantagem, que é particularmente aplicável a ambientes de desenvolvimento de aplicativos, é que o ODBC não define uma gramática padrão para a criação de procedimentos. Ou seja, embora os aplicativos possam chamar procedimentos de forma interligada, eles não podem criá-los interopermente.
