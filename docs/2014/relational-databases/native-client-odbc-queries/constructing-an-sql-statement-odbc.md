---
title: Construindo uma instrução SQL (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC], constructing
- ODBC applications, statements
ms.assetid: 0acc71e2-8004-4dd8-8592-05c022bdd692
author: rothja
ms.author: jroth
ms.openlocfilehash: e9bfe0a51ec33b310dae0c73f51ff72687811d02
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85018605"
---
# <a name="constructing-an-sql-statement-odbc"></a>Construindo uma instrução SQL (ODBC)
  Aplicativos ODBC realizam quase todo o acesso ao banco de dados executando instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. A forma dessas instruções depende dos requisitos do aplicativo. As instruções SQL podem ser construídas das seguintes maneiras:  
  
-   Embutidas em código  
  
     Instruções estáticas executadas por um aplicativo como uma tarefa fixa.  
  
-   Construídas em tempo de execução  
  
     Instruções SQL construídas em tempo de execução que permitem ao usuário adaptar a instrução usando cláusulas comuns, como SELECT, WHERE e ORDER BY. Isso inclui consultas ad hoc inseridas por usuários.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do cliente analisa instruções SQL somente para sintaxe ODBC e ISO sem suporte direto do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , que o driver transforma em [!INCLUDE[tsql](../../includes/tsql-md.md)] . Todas as outras sintaxes SQL são transmitidas inalteradas ao [!INCLUDE[ssDE](../../includes/ssde-md.md)], onde o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determinará se é um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido. Essa abordagem gera dois benefícios:  
  
-   Redução da sobrecarga  
  
     A sobrecarga de processamento do driver é minimizada porque ele só precisa examinar um conjunto pequeno de cláusulas ODBC e ISO.  
  
-   Flexibilidade  
  
     Os programadores podem adaptar a portabilidade dos aplicativos. Para aumentar a portabilidade em vários bancos de dados, use principalmente as sintaxes ISO e ODBC. Para usar aprimoramentos específicos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use a sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] apropriada. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client dá suporte à [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe completa, portanto, os aplicativos baseados em ODBC podem aproveitar todos os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 A lista de colunas em uma instrução SELECT deverá conter apenas as colunas necessárias para executar a tarefa atual. Isso não apenas reduz a quantidade de dados enviados pela rede, mas também reduz o efeito das alterações no banco de dados no aplicativo. Se um aplicativo não fizer referência a uma coluna de uma tabela, ele não será afetado por qualquer alteração feita nessa coluna.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando consultas &#40;ODBC&#41;](executing-queries-odbc.md)  
  
  
