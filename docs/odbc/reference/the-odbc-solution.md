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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b35883ff4d621f0ecc092020ad744455281dd63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286749"
---
# <a name="the-odbc-solution"></a>A solução ODBC
A questão, então, é como o ODBC padroniza o acesso ao banco de dados? Existem dois requisitos arquitetônicos:  
  
-   Os aplicativos devem ser capazes de acessar vários DBMSs usando o mesmo código-fonte sem recompilar ou revincular.  
  
-   Os aplicativos devem ser capazes de acessar vários DBMSs simultaneamente.  
  
 E há mais uma pergunta, devido à realidade do mercado:  
  
-   Quais recursos de DBMS o ODBC deve expor? Apenas recursos que são comuns a todos os DBMSs ou qualquer recurso que esteja disponível em qualquer DBMS?  
  
 A ODBC resolve esses problemas da seguinte maneira:  
  
-   **ODBC é uma interface de nível de chamada.** Para resolver o problema de como os aplicativos acessam vários DBMSs usando o mesmo código-fonte, o ODBC define um CLI padrão. Isso contém todas as funções nas especificações CLI do Open Group e ISO/IEC e fornece funções adicionais comumente exigidas pelos aplicativos.  
  
     Uma biblioteca diferente, ou driver, é necessária para cada DBMS que suporta ODBC. O driver implementa as funções na API ODBC. Para usar um driver diferente, o aplicativo não precisa ser recompilado ou religado. Em vez disso, o aplicativo simplesmente carrega o novo driver e chama as funções nele. Para acessar vários DBMSs simultaneamente, o aplicativo carrega vários drivers. A forma como os drivers são suportados é específica do sistema operacional. Por exemplo, no sistema operacional Microsoft® Windows®, os drivers são bibliotecas de links dinâmicos (DLLs).  
  
-   **O DBC define uma gramática SQL padrão.** Além de uma interface padrão de nível de chamada, o ODBC define uma gramática SQL padrão. Esta gramática é baseada na especificação Open Group SQL CAE. As diferenças entre as duas gramáticas são menores e principalmente devido às diferenças entre a gramática SQL exigida pelo SQL incorporado (Open Group) e um CLI (ODBC). Há também algumas extensões à gramática para expor características de linguagem comumente disponíveis não cobertas pela gramática do Grupo Aberto.  
  
     Os aplicativos podem enviar declarações usando gramática específica do ODBC ou DBMS. Se uma instrução usar gramática ODBC diferente da gramática específica do DBMS, o driver converte-a antes de enviá-la para a fonte de dados. No entanto, tais conversões são raras porque a maioria dos DBMSs já usam gramática SQL padrão.  
  
-   **O ODBC fornece um Driver Manager para gerenciar o acesso simultâneo a vários DBMSs.** Embora o uso de drivers resolva o problema de acessar vários DBMSs simultaneamente, o código para fazer isso pode ser complexo. Aplicativos projetados para trabalhar com todos os drivers não podem ser estáticamente ligados a nenhum driver. Em vez disso, eles devem carregar os drivers em tempo de execução e chamar as funções neles através de uma tabela de ponteiros de função. A situação se torna mais complexa se o aplicativo usar vários drivers simultaneamente.  
  
     Em vez de forçar cada aplicativo a fazer isso, o ODBC fornece um Driver Manager. O Driver Manager implementa todas as funções do ODBC - principalmente como chamadas de passagem para funções ODBC em drivers - e está estáticamente ligado ao aplicativo ou carregado pelo aplicativo em tempo de execução. Assim, o aplicativo chama funções ODBC pelo nome no Driver Manager, em vez de por ponteiro em cada driver.  
  
     Quando um aplicativo precisa de um driver específico, primeiro solicita uma alça de conexão com a qual identificar o motorista e, em seguida, solicita que o Driver Manager carregue o driver. O Driver Manager carrega o driver e armazena o endereço de cada função no driver. Para chamar uma função ODBC no driver, o aplicativo liga para essa função no Driver Manager e passa a alça de conexão para o driver. Em seguida, o Driver Manager chama a função usando o endereço armazenado anteriormente.  
  
-   **O ODBC expõe um número significativo de recursos DBMS, mas não requer drivers para suportar todos eles.** Se o ODBC expôs apenas características comuns a todos os DBMSs, seria de pouca utilidade; afinal, a razão pela qual existem tantos DBMSs diferentes hoje em dia é que eles têm características diferentes. Se o ODBC expôs todos os recursos disponíveis em qualquer DBMS, seria impossível para os drivers implementarem.  
  
     Em vez disso, o ODBC expõe um número significativo de recursos - mais do que são suportados pela maioria dos DBMSs - mas exige que os drivers implementem apenas um subconjunto desses recursos. Os drivers implementam os recursos restantes somente se forem suportados pelo DBMS subjacente ou se optarem por emulá-los. Assim, os aplicativos podem ser escritos para explorar os recursos de um único DBMS exposto pelo driver para esse DBMS, para usar apenas os recursos usados por todos os DBMSs, ou para verificar o suporte de um determinado recurso e reagir de acordo.  
  
     Para que um aplicativo possa determinar quais recursos de suporte a driver e DBMS, o ODBC fornece duas funções (**SQLGetInfo** e **SQLGetFunctions**) que retornam informações gerais sobre os recursos do driver e DBMS e uma lista de funções que o driver suporta. O ODBC também define os níveis de conformidade gramatical API e SQL, que especificam amplas faixas de recursos suportados pelo driver. Para obter mais informações, consulte [Níveis de Conformidade](../../odbc/reference/develop-app/conformance-levels.md).  
  
     É importante lembrar que o ODBC define uma interface comum para todos os recursos que expõe. Por causa disso, os aplicativos contêm código específico de recursos, não código específico do DBMS, e podem usar quaisquer drivers que exponham esses recursos. Uma vantagem disso é que os aplicativos não precisam ser atualizados quando os recursos suportados por um DBMS são aprimorados; em vez disso, quando um driver atualizado é instalado, o aplicativo usa automaticamente os recursos porque seu código é específico do recurso, não específico do driver ou específico do DBMS.
