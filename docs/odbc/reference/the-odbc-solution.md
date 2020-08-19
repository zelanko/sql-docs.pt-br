---
description: A solução ODBC
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f1a1c216dc67c33eadc9a058263087978f176297
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428858"
---
# <a name="the-odbc-solution"></a>A solução ODBC
A pergunta, então, é como o ODBC padroniza o acesso ao banco de dados? Há dois requisitos de arquitetura:  
  
-   Os aplicativos devem ser capazes de acessar vários DBMSs usando o mesmo código-fonte sem recompilação ou revinculação.  
  
-   Os aplicativos devem ser capazes de acessar vários DBMSs simultaneamente.  
  
 E há mais uma pergunta, devido à realidade do Marketplace:  
  
-   Quais recursos do DBMS o ODBC deve expor? Somente recursos que são comuns a todos os DBMSs ou qualquer recurso que esteja disponível em qualquer DBMS?  
  
 O ODBC resolve esses problemas da seguinte maneira:  
  
-   **O ODBC é uma interface de nível de chamada.** Para resolver o problema de como os aplicativos acessam vários DBMSs usando o mesmo código-fonte, o ODBC define uma CLI padrão. Ele contém todas as funções nas especificações da CLI de Open Group e ISO/IEC e fornece funções adicionais normalmente exigidas pelos aplicativos.  
  
     Uma biblioteca ou driver diferente é necessário para cada DBMS que dá suporte a ODBC. O Driver implementa as funções na API ODBC. Para usar um driver diferente, o aplicativo não precisa ser recompilado ou revinculado. Em vez disso, o aplicativo simplesmente carrega o novo driver e chama as funções nele. Para acessar vários DBMSs simultaneamente, o aplicativo carrega vários drivers. A forma como os drivers têm suporte é específica do sistema operacional. Por exemplo, no sistema operacional Microsoft® Windows®, os drivers são DLLs (bibliotecas de vínculo dinâmico).  
  
-   **O ODBC define uma gramática SQL padrão.** Além de uma interface de nível de chamada padrão, o ODBC define uma gramática SQL padrão. Essa gramática se baseia na especificação CAE do SQL do grupo aberto. As diferenças entre as duas gramáticas são secundárias e, principalmente, devido às diferenças entre a gramática do SQL exigida pelo SQL inserido (Open Group) e uma CLI (ODBC). Também há algumas extensões para a gramática para expor os recursos de linguagem comumente disponíveis não cobertos pela gramática do grupo aberto.  
  
     Os aplicativos podem enviar instruções usando o ODBC ou a gramática específica do DBMS. Se uma instrução usar a gramática ODBC diferente da gramática específica do DBMS, o driver a converterá antes de enviá-la para a fonte de dados. No entanto, essas conversões são raras porque a maioria dos DBMSs já usa a gramática SQL padrão.  
  
-   **O ODBC fornece um Gerenciador de driver para gerenciar o acesso simultâneo a vários DBMSs.** Embora o uso de drivers resolva o problema de acesso a vários DBMSs simultaneamente, o código para fazer isso pode ser complexo. Os aplicativos projetados para funcionar com todos os drivers não podem ser vinculados estaticamente a nenhum driver. Em vez disso, eles devem carregar drivers em tempo de execução e chamar as funções neles por meio de uma tabela de ponteiros de função. A situação se tornará mais complexa se o aplicativo usar vários drivers simultaneamente.  
  
     Em vez de forçar cada aplicativo a fazer isso, o ODBC fornece um Gerenciador de driver. O Gerenciador de Driver implementa todas as funções ODBC, principalmente como chamadas de passagem para funções ODBC em drivers, e é vinculado estaticamente ao aplicativo ou carregado pelo aplicativo em tempo de execução. Portanto, o aplicativo chama funções ODBC por nome no Gerenciador de driver, em vez de por ponteiro em cada driver.  
  
     Quando um aplicativo precisa de um driver específico, ele primeiro solicita um identificador de conexão com o qual identificar o driver e solicita que o Gerenciador de driver carregue o driver. O Gerenciador de driver carrega o driver e armazena o endereço de cada função no driver. Para chamar uma função ODBC no driver, o aplicativo chama essa função no Gerenciador de driver e passa o identificador de conexão para o driver. Em seguida, o Gerenciador de driver chama a função usando o endereço que ela armazenou anteriormente.  
  
-   **O ODBC expõe um número significativo de recursos do DBMS, mas não requer drivers para dar suporte a todos eles.** Se o ODBC expôs apenas os recursos que são comuns a todos os DBMSs, seria de pouco uso; Afinal, o motivo para que muitos DBMSs diferentes existam hoje é que eles têm recursos diferentes. Se o ODBC tiver exposto todos os recursos disponíveis em qualquer DBMS, seria impossível para os drivers implementarem.  
  
     Em vez disso, o ODBC expõe um número significativo de recursos, mais do que o suporte da maioria dos DBMSs, mas requer que os drivers implementem apenas um subconjunto desses recursos. Os drivers implementarão os recursos restantes somente se tiverem suporte do DBMS subjacente ou se optarem por emular. Assim, os aplicativos podem ser escritos para explorar os recursos de um único DBMS, como exposto pelo driver para esse DBMS, para usar somente os recursos usados por todos os DBMSs ou para verificar o suporte de um recurso específico e reagir de acordo.  
  
     Para que um aplicativo possa determinar quais recursos um driver e suporte do DBMS, o ODBC fornece duas funções (**SQLGetInfo** e **SQLGetFunctions**) que retornam informações gerais sobre os recursos do driver e do DBMS e uma lista de funções às quais o driver dá suporte. O ODBC também define os níveis de conformidade da gramática do SQL e da API, que especificam grandes intervalos de recursos suportados pelo driver. Para obter mais informações, consulte [níveis de conformidade](../../odbc/reference/develop-app/conformance-levels.md).  
  
     É importante lembrar que o ODBC define uma interface comum para todos os recursos que ele expõe. Por isso, os aplicativos contêm código específico do recurso, não um código específico do DBMS, e podem usar quaisquer drivers que exponham esses recursos. Uma vantagem disso é que os aplicativos não precisam ser atualizados quando os recursos com suporte de um DBMS são aprimorados; em vez disso, quando um driver atualizado é instalado, o aplicativo usa automaticamente os recursos porque seu código é específico do recurso, não específico do driver ou do DBMS.
