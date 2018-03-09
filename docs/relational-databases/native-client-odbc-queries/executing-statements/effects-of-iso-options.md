---
title: "Efeitos de opções ISO | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-queries
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ISO options (ODBC)
- ODBC applications, ISO options
- ODBC applications, statements
- SQL Server Native Client ODBC driver, ISO options
- statements [ODBC], ISO options
ms.assetid: 813f1397-fa0b-45ec-a718-e13fe2fb88ac
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2267290d43ec746fd3f2d11597eeefa498651e62
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="effects-of-iso-options"></a>Efeitos das opções ISO
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  O padrão ODBC corresponde bastante ao padrão ISO e os aplicativos ODBC esperam o comportamento padrão de um driver ODBC. Para fazer seu comportamento se conformar melhor com que definido no padrão ODBC, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client sempre usa qualquer opção ISO disponível na versão do SQL Server com o qual ele se conecta.  
  
 Quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client se conecta a uma instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o servidor detecta que o cliente está usando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client e ativa várias opções.  
  
 O próprio driver emite estas instruções; o aplicativo ODBC não faz nada para solicitá-las. A configuração dessas opções permite que os aplicativos ODBC que usam o driver sejam mais portáteis, pois o comportamento do servidor corresponde então ao padrão ISO.  
  
 Em geral, os aplicativos baseados na DB-Library não ativam essas opções. Sites que observam diferentes pontos de comportamento entre clientes ODBC ou DB-Library ao executar a mesma instrução SQL não deve presumir que isso a um problema com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client. Eles devem primeiro execute a instrução novamente no ambiente DB-Library com as mesmas opções SET que seriam usadas pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client.  
  
 Como as opções SET podem ser ativadas e desativadas a qualquer momento por usuários e aplicativos, os desenvolvedores de procedimentos armazenados e de gatilhos também devem tomar o cuidado de testar seus procedimentos e gatilhos com as opções SET listadas acima ativadas e desativadas. Isso garante que os procedimentos e gatilhos funcionem corretamente, independentemente das opções que uma conexão específica possa ter ativado ao invocar o procedimento ou o gatilho. Os gatilhos ou os procedimentos armazenados que necessitam de uma determinada configuração para uma dessas opções deve emitir uma instrução SET no início do gatilho ou do procedimento armazenado. Essa instrução SET permanece em vigor apenas para a execução do gatilho ou do procedimento armazenado; quando o procedimento ou o gatilho é concluído, a configuração original é restaurada.  
  
 Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], uma quarta opção SET, CONCAT_NULL_YIELDS_NULL, também é ativada. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client não define essas opções se AnsiNPW = não é especificado na fonte de dados ou em [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) ou [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md).  
  
 Como as opções ISO observadas anteriormente, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client não ativa a opção QUOTED_IDENTIFIER se QuotedID = não é especificado na fonte de dados ou em **SQLDriverConnect** ou  **SQLBrowseConnect**.  
  
 Para permitir que o driver saiba o estado atual das opções SET, os aplicativos ODBC não devem usar a instrução SET do [!INCLUDE[tsql](../../../includes/tsql-md.md)] para definir essas opções. Eles devem definir essas opções usando apenas a fonte de dados ou as opções de conexão. Se o aplicativo emitir instruções SET, o driver poderá gerar instruções SQL incorretas.  
  
## <a name="see-also"></a>Consulte também  
 [Executar instruções &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)   
 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)   
 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)  
  
  
