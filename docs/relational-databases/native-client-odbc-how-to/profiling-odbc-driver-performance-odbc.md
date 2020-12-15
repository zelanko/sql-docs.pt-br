---
description: Criar perfil de desempenho do driver ODBC (ODBC)
title: Criando perfil de desempenho do driver ODBC
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 0e6d7aed-28d2-419e-be6a-f60d3729bfd0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 09c5dff41c7865f02c508acbbf718b81cafa932a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469527"
---
# <a name="profiling-odbc-driver-performance-odbc"></a>Criar perfil de desempenho do driver ODBC (ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem duas opções específicas do driver para a criação de perfil de desempenho do driver.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC pode registrar as estatísticas de desempenho no arquivo. O arquivo de log é um arquivo delimitado por tabulação que pode ser analisado em qualquer planilha com suporte para arquivos delimitados por tabulação, como o Microsoft Excel.  
  
 O driver também pode registrar consultas de longa execução (consultas que não obtêm uma resposta do servidor em um intervalo especificado de tempo). Essas consultas podem ser analisadas depois pelos programadores e pelos administradores de banco de dados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Dados de desempenho de driver de perfil &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-data.md)  
  
-   [Consultas de Long-Running de log &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-data-log-long-running-queries.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tópicos de instruções sobre ODBC](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)  
  
  
