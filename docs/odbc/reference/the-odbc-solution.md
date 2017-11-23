---
title: "A solução ODBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], using ODBC
ms.assetid: 34b80790-e010-4b90-8eaa-03189f5d8986
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 806bc94a3807dbdd658cf710c0d22e2b6116d27b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="the-odbc-solution"></a>A solução ODBC
A pergunta, em seguida, é como o ODBC padronizar o acesso de banco de dados? Há dois requisitos de arquitetura:  
  
-   Aplicativos devem ser capazes de acessar DBMSs múltiplos usando o mesmo código-fonte sem recompilar ou vinculando novamente.  
  
-   Aplicativos devem ser capazes de acessar vários DBMSs simultaneamente.  
  
 E há uma questão mais, devido a realidade de mercado:  
  
-   Quais recursos do DBMS deve expor ODBC? Somente os recursos que são comuns a todos os DBMSs ou qualquer recurso que está disponível em qualquer DBMS?  
  
 ODBC resolve esses problemas, da seguinte maneira:  
  
-   **ODBC é uma interface de nível de chamada.** Para resolver o problema de como os aplicativos acessam DBMSs múltiplos usando o mesmo código de origem, o ODBC define uma CLI padrão. Este arquivo contém todas as funções nas especificações do Open Group e ISO/IEC CLI e fornece funções adicionais normalmente exigidas por aplicativos.  
  
     Uma biblioteca diferente, ou o driver, é necessário para cada DBMS que dá suporte a ODBC. O driver implementa as funções da API do ODBC. Para usar um driver diferente, o aplicativo não precisa ser recompilado ou vinculados novamente. Em vez disso, o aplicativo simplesmente carrega o driver novo e chama as funções nele. Para acessar vários DBMSs simultaneamente, o aplicativo carrega vários drivers. Como há suporte para drivers é específicas do sistema operacional. Por exemplo, no sistema operacional Microsoft® Windows®, os drivers são bibliotecas de vínculo dinâmico (DLLs).  
  
-   **ODBC define uma gramática SQL padrão.** Além de uma interface padrão de nível de chamada ODBC define uma gramática SQL padrão. Esta gramática baseia-se na especificação Open CAE de SQL de grupo. Diferenças entre as duas gramáticas sejam pequenas e principalmente devido a diferenças entre a gramática SQL exigida pelo embedded SQL (Open Group) e uma CLI (ODBC). Também há algumas extensões a gramática para expor recursos de linguagem disponíveis não cobertos pela gramática do Open Group.  
  
     Os aplicativos podem enviar instruções que usam ODBC ou específicos de DBMS gramática. Se uma instrução usa a gramática ODBC que é diferente da gramática de DBMS específico, o driver converte-o antes de enviá-la para a fonte de dados. No entanto, essas conversões são raros, porque mais DBMSs já usam gramática SQL padrão.  
  
-   **ODBC fornece um Gerenciador de Driver para gerenciar o acesso simultâneo a DBMSs múltiplos.** Embora o uso de drivers resolve o problema de acesso a vários DBMSs simultaneamente, o código para fazer isso pode ser complexo. Aplicativos que são projetados para trabalhar com todos os drivers não podem ser vinculados estaticamente para todos os drivers. Em vez disso, eles devem carregar drivers em tempo de execução e chamar as funções da-los por meio de uma tabela de ponteiros de função. A situação se tornará mais complexa se o aplicativo usa vários drivers simultaneamente.  
  
     Em vez de fazer com que cada aplicativo para fazer isso, o ODBC fornece um Gerenciador de Driver. O Gerenciador de Driver implementa todas as funções ODBC — principalmente como passagem chamadas para funções ODBC em drivers — e está estaticamente vinculada ao aplicativo ou carregados pelo aplicativo em tempo de execução. Portanto, o aplicativo chama funções ODBC por nome no Gerenciador de Driver, em vez de ponteiro em cada driver.  
  
     Quando um aplicativo precisa de um driver específico, primeiramente ele solicita um identificador de conexão para identificar o driver e, em seguida, o Gerenciador de Driver carregar o driver de solicitações. O Gerenciador de Driver carrega o driver e armazena o endereço de cada função no driver. Para chamar uma função ODBC no driver, o aplicativo chama essa função no Gerenciador de Driver e transmite o identificador de conexão para o driver. O Gerenciador de Driver, em seguida, chama a função usando o endereço armazenadas antes.  
  
-   **ODBC expõe um número significativo de recursos do DBMS, mas não requerem drivers para dar suporte a todos eles.** Se o ODBC exposta somente os recursos que são comuns a todos os DBMSs, seria de pouco uso; Afinal, o motivo para que muitos DBMSs diferentes existem atualmente é que eles têm recursos diferentes. Se o ODBC exposta a todos os recursos que estão disponível em qualquer DBMS, será impossível drivers implementar.  
  
     Em vez disso, o ODBC expõe um número significativo de recursos — mais do que são suportados pela maioria dos DBMSs —, mas exige drivers para implementar apenas um subconjunto desses recursos. Drivers de implementam os recursos de restantes somente se eles são suportados pelo DBMS subjacente ou se ele optar emulá-los. Portanto, os aplicativos podem ser gravados para explorar os recursos de um único DBMS como exposto pelo driver para que DBMS, para usar somente os recursos usados por todos os DBMSs, ou para verificar se há suporte de um recurso específico e reagir de acordo.  
  
     Para que um aplicativo pode determinar quais recursos de um driver e suporte de DBMS, ODBC fornece duas funções (**SQLGetInfo** e **SQLGetFunctions**) que retornam informações gerais sobre o driver e DBMS recursos e uma lista de funções, o driver dá suporte. O ODBC também define API e SQL níveis de conformidade de gramática, que especificam intervalos amplo de recursos com suporte pelo driver. Para obter mais informações, consulte [níveis de conformidade](../../odbc/reference/develop-app/conformance-levels.md).  
  
     É importante lembrar-se de que o ODBC define uma interface comum para todos os recursos que ele expõe. Por isso, aplicativos contêm recursos específicos código, não código de DBMS específico e podem usar todos os drivers que expõem esses recursos. Uma vantagem disso é que aplicativos não precisam ser atualizados quando os recursos suportados por um DBMS são aprimorados; em vez disso, quando um driver atualizado está instalado, o aplicativo usa automaticamente os recursos porque seu código é recursos específicos, e não específicas do driver ou específicos de DBMS.
