---
title: Linguagem (SQL) | Microsoft Docs
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
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9a8464fb7ff4e971c1d67d270ffa021d0dca1910
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="structured-query-language-sql"></a>SQL (Structured Query Language)
Um DBMS típico permite aos usuários armazenar, acessar e modificar dados de uma maneira organizada e eficiente. Originalmente, os usuários de DBMSs foram programadores. Acessar os dados armazenados, é necessário escrever um programa em uma linguagem de programação como COBOL. Enquanto esses programas foram escritos com frequência para apresentar uma interface amigável para um usuário sem conhecimento técnico, o acesso aos dados em si necessário os serviços de um programador experiente. Casual acesso aos dados não era prático.  
  
 Os usuários não foram totalmente satisfeitos com essa situação. Enquanto eles podem acessar os dados, geralmente necessário convencer um programador DBMS para gravar um software especial. Por exemplo, se um departamento de vendas quisesse ver o total de vendas do mês anterior por seus vendedores e quisesse essas informações classificadas em ordem por comprimento de cada vendedor de serviço da empresa, ele tinha duas opções: ou um programa já existia que permitido as informações sejam acessados exatamente dessa forma, ou o departamento precisava pedir um programador para escrever um programa. Em muitos casos, isso era mais trabalho do que era vale a pena e sempre foi uma solução dispendiosa para consultas únicas ou ad hoc. Como os usuários mais desejavam acesso fácil, esse problema cresceu maiores.  
  
 Permitir que os usuários acessem os dados em uma base ad hoc necessário lhes um idioma no qual expressar suas solicitações. Uma única solicitação para um banco de dados é definida como uma consulta; Essa é uma linguagem é chamada de uma linguagem de consulta. Muitas linguagens de consulta foram desenvolvidas para essa finalidade, mas uma destas opções se tornaram mais populares: Structured Query Language, criado no IBM no 1970s. Ele é mais comumente conhecido por sua acrônimo, SQL e é pronunciado como "ell de sinalização ESSO" e "sequel"; esse manual usa a pronúncia anterior. SQL se tornou um padrão em 1986 de ANSI e um arquivo ISO padrão em 1987; ele é usado atualmente em um grande muitos sistemas de gerenciamento de banco de dados.  
  
 Embora a solução do SQL ad hoc necessidades dos usuários, a necessidade de acesso a dados por programas de computador não desaparecer. Na verdade, a maioria dos acesso de banco de dados ainda era (e é) programático, na forma de relatórios agendados regularmente e análise estatística, programas de entrada de dados, como aqueles usados para entrada de pedido e dados de programas de manipulação, como aqueles usados para reconciliar as contas e Gere ordens de trabalho.  
  
 Esses programas também usam SQL, usando uma das três seguintes técnicas:  
  
-   **Embedded SQL**, no qual o SQL são incorporadas em uma linguagem de host como C ou COBOL.  
  
-   **Os módulos SQL**, nos quais instruções SQL são compiladas no DBMS e chamadas de uma linguagem host.  
  
-   **Interface de nível de chamada**, ou o CLI, que consiste de funções chamadas para transmitir instruções SQL para o DBMS e recuperar os resultados de DBMS.  
  
> [!NOTE]  
>  É um acidente de histórico que o termo interface de nível de chamada é usado em vez de programação de aplicativo (API) de interface outro termo para a mesma coisa. No mundo de banco de dados, API é usada para descrever SQL em si: SQL é a API de um DBMS.  
  
 Dessas opções, embedded SQL é mais comumente usadas, embora DBMSs de maioria dos principais oferecer suporte a CLIs proprietárias.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Processar uma instrução SQL](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [SQL inserido](../../odbc/reference/embedded-sql.md)  
  
-   [Módulos SQL](../../odbc/reference/sql-modules.md)  
  
-   [Interfaces de nível de chamada](../../odbc/reference/call-level-interfaces.md)
