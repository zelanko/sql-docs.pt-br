---
title: Linguagem de consulta estruturada (SQL) | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293386"
---
# <a name="structured-query-language-sql"></a>SQL (Structured Query Language)
Um DBMS típico permite que os usuários armazenem, acessem e modifiquem dados de forma organizada e eficiente. Originalmente, os usuários de DBMSs eram programadores. Acessar os dados armazenados exigia escrever um programa em uma linguagem de programação como COBOL. Embora esses programas fossem frequentemente escritos para apresentar uma interface amigável a um usuário não técnico, o acesso aos dados em si exigia os serviços de um programador experiente. O acesso casual aos dados não era prático.  
  
 Os usuários não estavam totalmente satisfeitos com esta situação. Embora pudessem acessar dados, muitas vezes era necessário convencer um programador DBMS a escrever um software especial. Por exemplo, se um departamento de vendas queria ver o total de vendas no mês anterior por cada um de seus vendedores e queria que essas informações fossem classificadas em ordem pelo tempo de serviço de cada vendedor na empresa, ele tinha duas opções: Ou existia um programa que permitisse que as informações fossem acessadas exatamente dessa forma, ou o departamento tinha que pedir a um programapara escrever tal programa. Em muitos casos, isso era mais trabalho do que valia a pena, e sempre foi uma solução cara para consultas únicas, ou ad hoc. À medida que mais e mais usuários queriam fácil acesso, esse problema cresceu cada vez mais.  
  
 Permitir que os usuários acessem dados em uma base ad hoc exigia dar-lhes um idioma no qual expressar suas solicitações. Uma única solicitação a um banco de dados é definida como uma consulta; tal idioma é chamado de linguagem de consulta. Muitas linguagens de consulta foram desenvolvidas para este fim, mas uma delas se tornou a mais popular: Structured Query Language, inventada na IBM na década de 1970. É mais conhecido por sua sigla, SQL, e é pronunciado tanto como "ess-cue-ell" quanto como "sequela". O SQL tornou-se um padrão ANSI em 1986 e um padrão ISO em 1987; é usado hoje em muitos sistemas de gerenciamento de banco de dados.  
  
 Embora o SQL tenha resolvido as necessidades ad hoc dos usuários, a necessidade de acesso de dados por programas de computador não diminuiu. Na verdade, a maior parte do acesso ao banco de dados ainda era (e é) programática, sob a forma de relatórios regularmente agendados e análises estatísticas, programas de entrada de dados, como os utilizados para entrada de pedidos, e programas de manipulação de dados, como aqueles utilizados para conciliar contas e gerar ordens de serviço.  
  
 Esses programas também utilizam SQL, usando uma das três técnicas a seguir:  
  
-   **Embedded SQL**, no qual as instruções SQL são incorporadas em um idioma host, como C ou COBOL.  
  
-   **Módulos SQL**, nos quais as instruções SQL são compiladas no DBMS e chamadas de um idioma host.  
  
-   **Interface de nível de**chamada , ou CLI, que consiste em funções chamadas para passar instruções SQL para o DBMS e para recuperar resultados do DBMS.  
  
> [!NOTE]  
>  É um acidente histórico que o termo interface de nível de chamada seja usado em vez de a API (Application Programming Interface, interface de programação de aplicativos), outro termo para a mesma coisa. No mundo do banco de dados, a API é usada para descrever o próprio SQL: SQL é a API de um DBMS.  
  
 Dessas opções, o SQL incorporado é o mais usado, embora a maioria dos principais DBMSs suportem CLIs proprietários.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Processando uma declaração SQL](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [SQL inserido](../../odbc/reference/embedded-sql.md)  
  
-   [Módulos SQL](../../odbc/reference/sql-modules.md)  
  
-   [Interfaces de nível de chamada](../../odbc/reference/call-level-interfaces.md)
