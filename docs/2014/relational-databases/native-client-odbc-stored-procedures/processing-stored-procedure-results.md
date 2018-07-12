---
title: Processando resultados do procedimento armazenado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], results
ms.assetid: 788ef2a4-17de-4526-960b-46bf29aafc9f
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 767eb56845429a19575d1339976a014ec3ea5288
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411023"
---
# <a name="processing-stored-procedure-results"></a>Processando resultados do procedimento armazenado
  Os procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm quatro mecanismos usados para retornar dados:  
  
-   Cada instrução SELECT no procedimento gera um conjunto de resultados.  
  
-   O procedimento pode retornar dados através de parâmetros de saída.  
  
-   Um parâmetro de saída de cursor pode devolver um cursor de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   O procedimento pode ter um código de retorno de inteiro.  
  
 Os aplicativos devem conseguir tratar todas essas saídas dos procedimentos armazenados. A instrução CALL ou EXECUTE deve incluir marcadores de parâmetro para o código de retorno e parâmetros de saída. Use [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) vinculá-las como parâmetros de saída e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client irá transferir os valores de saída para as variáveis associadas. Parâmetros de saída e códigos de retorno são os últimos itens retornados ao cliente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; eles não são retornados para o aplicativo até que [SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md) retorne SQL_NO_DATA.  
  
 O ODBC não dá suporte à associação de parâmetros de cursor do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Como todos os parâmetros de saída devem ser associados antes de executar um procedimento, todos os procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] que contêm um parâmetro de cursor de saída não podem ser chamados por aplicativos ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Executando procedimentos armazenados](running-stored-procedures.md)  
  
  
