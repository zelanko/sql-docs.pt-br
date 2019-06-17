---
title: A solução ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], using ODBC
ms.assetid: 34b80790-e010-4b90-8eaa-03189f5d8986
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5adf32800f4c2bc2b4a0874ca7efc22f04ffd110
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200478"
---
# <a name="the-odbc-solution"></a>A solução ODBC
A pergunta, em seguida, é como o ODBC padronizar o acesso de banco de dados? Há dois requisitos de arquitetura:  
  
-   Aplicativos devem ser capazes de acessar vários DBMSs usando o mesmo código-fonte sem recompilar ou nova vinculação.  
  
-   Aplicativos devem ser capazes de acessar vários DBMSs simultaneamente.  
  
 E há mais uma pergunta, devido a realidade do marketplace:  
  
-   Quais recursos do DBMS deve expor ODBC? Somente os recursos que são comuns a todos os DBMSs ou qualquer recurso que está disponível em qualquer DBMS?  
  
 ODBC resolve esses problemas da seguinte maneira:  
  
-   **O ODBC é uma interface de nível de chamada.** Para resolver o problema de como os aplicativos acessam DBMSs múltiplos usando o mesmo código-fonte, o ODBC define um padrão CLI. Este arquivo contém todas as funções nas especificações do Open Group e ISO/IEC CLI e fornece funções adicionais normalmente exigidas por aplicativos.  
  
     Uma outra biblioteca ou driver, é necessário para cada DBMS que oferece suporte ao ODBC. O driver implementa as funções na API do ODBC. Para usar um driver diferente, o aplicativo não precisa ser recompilado ou vinculados novamente. Em vez disso, o aplicativo simplesmente carrega o driver novo e chama as funções nela. Para acessar vários DBMSs simultaneamente, o aplicativo carrega vários drivers. Como há suporte para drivers é específico do sistema operacional. Por exemplo, no sistema operacional Microsoft® Windows®, os drivers são bibliotecas de vínculo dinâmico (DLLs).  
  
-   **ODBC define uma gramática SQL padrão.** Além de uma interface de nível de chamada padrão, o ODBC define uma gramática SQL padrão. Essa gramática baseia-se na especificação aberta CAE de SQL de grupo. Diferenças entre as duas gramáticas são pequenas e principalmente devido a diferenças entre a gramática SQL necessários para embedded SQL (Open Group) e uma CLI (ODBC). Também há algumas extensões para a gramática para expor recursos de linguagem geralmente disponíveis não são cobertos pela gramática do Open Group.  
  
     Os aplicativos podem enviar instruções que usam ODBC ou específicos de DBMS de gramática. Se uma instrução usa a gramática ODBC que é diferente da gramática de DBMS específico, o driver converterá antes de enviá-la para a fonte de dados. No entanto, essas conversões são raros, porque DBMSs a maioria dos já usam a gramática SQL padrão.  
  
-   **O ODBC fornece um Gerenciador de Driver para gerenciar o acesso simultâneo a várias DBMSs.** Embora o uso de drivers resolve o problema de acessar vários DBMSs simultaneamente, o código para fazer isso pode ser complexo. Aplicativos que são projetados para funcionar com todos os drivers não podem ser vinculados estaticamente para todos os drivers. Em vez disso, eles devem carregar drivers em tempo de execução e chamar as funções eles por meio de uma tabela de ponteiros de função. A situação se torna mais complexa se o aplicativo usa vários drivers simultaneamente.  
  
     Em vez de forçar a cada aplicativo para fazer isso, o ODBC fornece um Gerenciador de Driver. O Gerenciador de Driver implementa todas as funções ODBC - principalmente como passagem chamadas para funções ODBC em drivers - e é estaticamente vinculado ao aplicativo ou carregado pelo aplicativo em tempo de execução. Portanto, o aplicativo chama funções ODBC por nome no Gerenciador de Driver, em vez de ponteiro em cada driver.  
  
     Quando um aplicativo precisar de um driver específico, ele primeiro solicita um identificador de conexão para identificar o driver e, em seguida, o Gerenciador de Driver carregar o driver de solicitações. O Gerenciador de Driver carrega o driver e armazena o endereço de cada função no driver. Para chamar uma função ODBC no driver, o aplicativo chama essa função no Gerenciador de Driver e transmite o identificador de conexão para o driver. O Gerenciador de Driver, em seguida, chama a função usando o endereço que ele armazenou anteriormente.  
  
-   **ODBC expõe um número significativo de recursos do DBMS, mas não exige drivers para dar suporte a todos eles.** Se o ODBC exposto somente os recursos que são comuns a todos os DBMSs, seria de pouco uso; Afinal de contas, o motivo para que muitos DBMSs diferentes existem atualmente é que eles têm recursos diferentes. Se o ODBC exposta a todos os recursos que estão disponível em qualquer DBMS, seria impossível para drivers de implementar.  
  
     Em vez disso, o ODBC expõe um número significativo de recursos – mais do que são compatíveis com a maioria dos DBMSs - mas exige drivers para implementar apenas um subconjunto desses recursos. Drivers de implementam os recursos restantes somente se eles são suportados pelo DBMS subjacente ou se eles optarem por emulá-los. Assim, os aplicativos podem ser escritos para explorar os recursos de um único DBMS, como exposto pelo driver para desse DBMS, usar apenas os recursos usados por todos os DBMSs, ou para verificar se há suporte de um determinado recurso e reagir de acordo.  
  
     Para que um aplicativo pode determinar quais recursos um driver e suporte do DBMS, o ODBC fornece duas funções (**SQLGetInfo** e **SQLGetFunctions**) que retornam informações gerais sobre o driver e o DBMS recursos e uma lista de funções, o driver dá suporte. O ODBC também define a API e SQL níveis de conformidade de gramática, que especifiquem intervalos amplos de recursos com suporte pelo driver. Para obter mais informações, consulte [níveis de conformidade](../../odbc/reference/develop-app/conformance-levels.md).  
  
     É importante lembrar-se de que o ODBC define uma interface comum para todos os recursos que ele expõe. Por causa disso, os aplicativos contêm código de recurso específico, não o código específico do DBMS e podem usar todos os drivers que expõem esses recursos. Uma vantagem disso é que aplicativos não precisam ser atualizado quando os recursos compatíveis com um DBMS são aprimorados; em vez disso, quando um driver atualizado está instalado, o aplicativo usa automaticamente os recursos porque seu código é específico de recurso, não específicos do driver ou específicos de DBMS.
