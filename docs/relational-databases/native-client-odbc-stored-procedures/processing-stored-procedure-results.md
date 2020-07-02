---
title: Processando resultados de procedimento armazenado | Microsoft Docs
description: Saiba mais sobre os mecanismos que SQL Server procedimentos armazenados usam para retornar dados aos aplicativos. Os aplicativos devem ser capazes de lidar com todos esses tipos.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], results
ms.assetid: 788ef2a4-17de-4526-960b-46bf29aafc9f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ac787d3aa33828447cf9f6630fc9814ba3cfa45e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85659289"
---
# <a name="processing-stored-procedure-results"></a>Processando resultados do procedimento armazenado
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Os procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm quatro mecanismos usados para retornar dados:  
  
-   Cada instrução SELECT no procedimento gera um conjunto de resultados.  
  
-   O procedimento pode retornar dados através de parâmetros de saída.  
  
-   Um parâmetro de saída de cursor pode devolver um cursor de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   O procedimento pode ter um código de retorno de inteiro.  
  
 Os aplicativos devem conseguir tratar todas essas saídas dos procedimentos armazenados. A instrução CALL ou EXECUTE deve incluir marcadores de parâmetro para o código de retorno e parâmetros de saída. Use [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) para associá-los todos como parâmetros de saída e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client irá transferir os valores de saída para as variáveis associadas. Os parâmetros de saída e os códigos de retorno são os últimos itens retornados para o cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; eles não são retornados para o aplicativo até que [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) retorne SQL_NO_DATA.  
  
 O ODBC não dá suporte à associação de parâmetros de cursor do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Como todos os parâmetros de saída devem ser associados antes de executar um procedimento, todos os procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] que contêm um parâmetro de cursor de saída não podem ser chamados por aplicativos ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando procedimentos armazenados](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
