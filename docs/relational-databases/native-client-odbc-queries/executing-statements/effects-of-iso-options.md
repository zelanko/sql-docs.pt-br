---
title: Efeitos das opções ISO | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ISO options (ODBC)
- ODBC applications, ISO options
- ODBC applications, statements
- SQL Server Native Client ODBC driver, ISO options
- statements [ODBC], ISO options
ms.assetid: 813f1397-fa0b-45ec-a718-e13fe2fb88ac
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: adf37d03f5ea4f06be4d58e60deca68e10d45abb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297927"
---
# <a name="effects-of-iso-options"></a>Efeitos das opções ISO
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O padrão ODBC corresponde bastante ao padrão ISO e os aplicativos ODBC esperam o comportamento padrão de um driver ODBC. Para tornar seu comportamento mais próximo do definido no padrão [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC, o driver ODBC do Cliente Nativo sempre usa quaisquer opções ISO disponíveis na versão do SQL Server com a qual ele se conecta.  
  
 Quando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o driver ODBC do Cliente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Nativo se conecta a uma instância [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de , o servidor detecta que o cliente está usando o driver ODBC do Cliente Nativo e define várias opções.  
  
 O próprio driver emite estas instruções; o aplicativo ODBC não faz nada para solicitá-las. A configuração dessas opções permite que os aplicativos ODBC que usam o driver sejam mais portáteis, pois o comportamento do servidor corresponde então ao padrão ISO.  
  
 Em geral, os aplicativos baseados na DB-Library não ativam essas opções. Sites que observam diferentes comportamentos entre clientes ODBC ou DB-Library ao executar a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mesma declaração SQL não devem assumir que isso aponta para um problema com o driver ODBC do Cliente Nativo. Eles devem primeiro reexecutar a declaração no ambiente DB-Library com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] as mesmas opções SET que seriam usadas pelo driver Cliente Nativo ODBC.  
  
 Como as opções SET podem ser ativadas e desativadas a qualquer momento por usuários e aplicativos, os desenvolvedores de procedimentos armazenados e de gatilhos também devem tomar o cuidado de testar seus procedimentos e gatilhos com as opções SET listadas acima ativadas e desativadas. Isso garante que os procedimentos e gatilhos funcionem corretamente, independentemente das opções que uma conexão específica possa ter ativado ao invocar o procedimento ou o gatilho. Os gatilhos ou os procedimentos armazenados que necessitam de uma determinada configuração para uma dessas opções deve emitir uma instrução SET no início do gatilho ou do procedimento armazenado. Essa instrução SET permanece em vigor apenas para a execução do gatilho ou do procedimento armazenado; quando o procedimento ou o gatilho é concluído, a configuração original é restaurada.  
  
 Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], uma quarta opção SET, CONCAT_NULL_YIELDS_NULL, também é ativada. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Cliente Nativo não define essas opções se O AnsiNPW=NO for especificado na fonte de dados ou no [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) ou [no SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md).  
  
 Como as opções ISO [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] observadas anteriormente, o driver Nativo Cliente ODBC não ativa a opção QUOTED_IDENTIFIER se QuotedID=NO for especificado na fonte de dados ou no **SQLDriverConnect** ou **no SQLBrowseConnect**.  
  
 Para permitir que o driver saiba o estado atual das opções SET, os aplicativos ODBC não devem usar a instrução SET do [!INCLUDE[tsql](../../../includes/tsql-md.md)] para definir essas opções. Eles devem definir essas opções usando apenas a fonte de dados ou as opções de conexão. Se o aplicativo emitir instruções SET, o driver poderá gerar instruções SQL incorretas.  
  
## <a name="see-also"></a>Consulte Também  
 [Execução de Declarações &#40;&#41;Da ODBC](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)   
 [Sqldriverconnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)   
 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)  
  
  
