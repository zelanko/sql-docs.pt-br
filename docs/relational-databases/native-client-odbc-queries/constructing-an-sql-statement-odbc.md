---
title: Construindo uma instrução SQL (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC], constructing
- ODBC applications, statements
ms.assetid: 0acc71e2-8004-4dd8-8592-05c022bdd692
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 96e3c04692360bd13010fe40063b0e761d60b2ce
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779983"
---
# <a name="constructing-an-sql-statement-odbc"></a>Construindo uma instrução SQL (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Aplicativos ODBC realizam quase todo o acesso ao banco de dados executando instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. A forma dessas instruções depende dos requisitos do aplicativo. As instruções SQL podem ser construídas das seguintes maneiras:  
  
-   Embutidas em código  
  
     Instruções estáticas executadas por um aplicativo como uma tarefa fixa.  
  
-   Construídas em tempo de execução  
  
     Instruções SQL construídas em tempo de execução que permitem ao usuário adaptar a instrução usando cláusulas comuns, como SELECT, WHERE e ORDER BY. Isso inclui consultas ad hoc inseridas por usuários.  
  
 O driver ODBC do cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] analisa instruções SQL somente para sintaxe ODBC e ISO sem suporte direto pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)], que o driver transforma em [!INCLUDE[tsql](../../includes/tsql-md.md)]. Todas as outras sintaxes SQL são transmitidas inalteradas ao [!INCLUDE[ssDE](../../includes/ssde-md.md)], onde o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determinará se é um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido. Essa abordagem gera dois benefícios:  
  
-   Redução da sobrecarga  
  
     A sobrecarga de processamento do driver é minimizada porque ele só precisa examinar um conjunto pequeno de cláusulas ODBC e ISO.  
  
-   Flexibilidade  
  
     Os programadores podem adaptar a portabilidade dos aplicativos. Para aumentar a portabilidade em vários bancos de dados, use principalmente as sintaxes ISO e ODBC. Para usar aprimoramentos específicos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use a sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] apropriada. O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte à sintaxe de [!INCLUDE[tsql](../../includes/tsql-md.md)] completa, portanto, os aplicativos baseados em ODBC podem aproveitar todos os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A lista de colunas em uma instrução SELECT deverá conter apenas as colunas necessárias para executar a tarefa atual. Isso não apenas reduz a quantidade de dados enviados pela rede, mas também reduz o efeito das alterações no banco de dados no aplicativo. Se um aplicativo não fizer referência a uma coluna de uma tabela, ele não será afetado por qualquer alteração feita nessa coluna.  
  
## <a name="see-also"></a>Consulte também  
 [Executando consultas &#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
