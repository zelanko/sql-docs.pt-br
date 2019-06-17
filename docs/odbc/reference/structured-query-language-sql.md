---
title: Linguagem (SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 86f9dd843171c02654302694c669f40b6b51ab78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232087"
---
# <a name="structured-query-language-sql"></a>SQL (Structured Query Language)
Um típico DBMS permite aos usuários armazenar, acessar e modificar dados de forma eficiente e organizada. Originalmente, os usuários de DBMSs eram os programadores. Acessar os dados armazenados, é necessário escrever um programa em uma linguagem de programação como COBOL. Embora muitas vezes, esses programas foram escritos para apresentar uma interface amigável para um usuário não técnico, acesso aos dados em si os serviços necessários de um programador experiente. Casual acesso aos dados não era prático.  
  
 Os usuários não foram totalmente satisfeitos com essa situação. Enquanto eles poderiam acessar dados, muitas vezes necessário convencendo um programador DBMS para escrever software especial. Por exemplo, se um departamento de vendas queria ver o total de vendas do mês anterior por cada um de seus vendedores e quisesse essas informações classificadas em ordem pelo comprimento de cada vendedor de serviço da empresa, ele tinha duas opções: Ou um programa já existia que as informações sejam acessados exatamente dessa forma de permissão ou o departamento precisava pedir que um programador de escrever um programa desse tipo. Em muitos casos, isso era mais trabalho do que valeu a pena e sempre foi uma solução dispendiosa para consultas ocasionais ou ad-hoc. Conforme mais e mais usuários quisesse acesso fácil, esse problema cresceu maiores.  
  
 Permitir que os usuários acessem os dados em uma base ad hoc necessário dando-lhes um idioma no qual expressar suas solicitações. Uma única solicitação para um banco de dados é definida como uma consulta; Essa é uma linguagem é chamada de uma linguagem de consulta. Muitas linguagens de consulta foram desenvolvidas para essa finalidade, mas uma destas opções se tornaram mais populares: Linguagem de consulta estruturada, inventou na IBM na década de 1970. Ele é mais conhecido por seu acrônimo, SQL e é pronunciado como "ell de sinalização ess" e "continuação". SQL se tornou um padrão em 1986 de ANSI e um arquivo ISO padrão em 1987; ele é usado atualmente em um ótimo muitos sistemas de gerenciamento de banco de dados.  
  
 Embora o SQL resolvido ad-hoc necessidades dos usuários, a necessidade de acesso a dados por programas de computador não vão embora. Na verdade, a maioria dos acesso de banco de dados ainda era (e é) através de programação, na forma de relatórios agendados regularmente e análise estatística, programas de entrada de dados, como aquelas usadas para entrada de pedido e dados de programas de manipulação, como aqueles usados para reconciliar contas e Gere ordens de trabalho.  
  
 Esses programas também usam o SQL, usando um dos três seguintes técnicas:  
  
-   **Embedded SQL**, no qual o SQL são incorporadas em uma linguagem de host, como C ou COBOL.  
  
-   **Módulos SQL**em quais instruções SQL são compiladas no DBMS e são chamadas de uma linguagem host.  
  
-   **Interface de nível de chamada**, ou a CLI, que consiste em funções chamadas para passar instruções SQL para o DBMS e recuperar os resultados do DBMS.  
  
> [!NOTE]  
>  É um acidente de histórico que o termo de interface de nível de chamada é usado em vez de programação de aplicativo (API) de interface outro termo para a mesma coisa. No mundo do banco de dados, a API é usada para descrever SQL em si: SQL é a API de um DBMS.  
  
 Uma dessas opções, embedded SQL é mais comumente usados, embora DBMSs da maioria dos principais oferecer suporte a CLIs proprietárias.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Processar uma instrução SQL](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [SQL inserido](../../odbc/reference/embedded-sql.md)  
  
-   [Módulos SQL](../../odbc/reference/sql-modules.md)  
  
-   [Interfaces de nível de chamada](../../odbc/reference/call-level-interfaces.md)
