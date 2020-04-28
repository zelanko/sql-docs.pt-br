---
title: Linguagem SQL (SQL) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c669b4424271fc1a3c91dea37159474fb52b97cd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81293386"
---
# <a name="structured-query-language-sql"></a>SQL (Structured Query Language)
Um DBMS típico permite que os usuários armazenem, acessem e modifiquem dados de uma maneira organizada e eficiente. Originalmente, os usuários de DBMS eram programadores. O acesso aos dados armazenados exigia a gravação de um programa em uma linguagem de programação, como o COBOL. Embora esses programas geralmente tenham sido escritos para apresentar uma interface amigável a um usuário não técnico, o acesso aos dados em si exigia os serviços de um programador experiente. O acesso casual aos dados não era prático.  
  
 Os usuários não estavam totalmente satisfeitos com essa situação. Embora eles pudessem acessar dados, muitas vezes exigiam convencer um programador de DBMS a escrever software especial. Por exemplo, se um departamento de vendas quisesse ver o total de vendas no mês anterior por cada um de seus vendedores e quisesse que essas informações fossem classificadas de acordo com o período de serviço de cada vendedor na empresa, ela tinha duas opções: um programa já existia que permitia que as informações fossem acessadas exatamente dessa forma ou que o departamento tivesse de pedir a ele um programa. Em muitos casos, isso era mais trabalho do que era válido e era sempre uma solução cara para consultas unidirecionais, ou ad hoc. À medida que mais e mais usuários queriam acesso fácil, esse problema cresceu maior e maior.  
  
 Permitir que os usuários acessem dados em uma base ad hoc necessária, fornecendo a eles um idioma no qual expressar suas solicitações. Uma única solicitação para um banco de dados é definida como uma consulta; essa linguagem é chamada de linguagem de consulta. Muitas linguagens de consulta foram desenvolvidas para essa finalidade, mas uma delas se tornou a mais popular: linguagem SQL, inventada na IBM na 70. Ele é mais comumente conhecido por seu acrônimo, SQL e é pronunciado como "ESS-Cue-ell" e como "sequência". O SQL tornou-se um padrão ANSI em 1986 e um padrão ISO em 1987; Ele é usado hoje em vários sistemas de gerenciamento de bancos de dados.  
  
 Embora o SQL tenha resolvido as necessidades ad hoc dos usuários, a necessidade de acesso a dados por programas de computador não desaparece. Na verdade, a maior parte do acesso ao banco de dados ainda era (e é) programática, na forma de relatórios agendados regularmente e análises estatísticas, programas de entrada de dados como aqueles usados para a entrada de pedidos e programas de manipulação de dados, como aqueles usados para reconciliar contas e gerar ordens de trabalho.  
  
 Esses programas também usam o SQL, usando uma das três técnicas a seguir:  
  
-   **SQL inserido**, no qual as instruções SQL são inseridas em um idioma de host como C ou COBOL.  
  
-   **Módulos SQL**, nos quais as instruções SQL são compiladas no DBMS e chamadas de um idioma de host.  
  
-   **Interface de nível de chamada**, ou CLI, que consiste em funções chamadas para passar instruções SQL para o DBMS e para recuperar os resultados do DBMS.  
  
> [!NOTE]  
>  É um acidente histórico que o termo interface de nível de chamada é usado em vez da API (interface de programação de aplicativo), outro termo para a mesma coisa. No mundo do banco de dados, a API é usada para descrever o próprio SQL: SQL é a API para um DBMS.  
  
 Dessas opções, o SQL inserido é o mais comumente usado, embora a maioria dos DBMSs ofereçam suporte a CLIs proprietárias.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Processando uma instrução SQL](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [SQL inserido](../../odbc/reference/embedded-sql.md)  
  
-   [Módulos SQL](../../odbc/reference/sql-modules.md)  
  
-   [Interfaces de nível de chamada](../../odbc/reference/call-level-interfaces.md)
