---
title: Modificações registradas em log versus não registradas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 922d4c7be51e92b02ea904d5b4917f7ccbeec28c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760612"
---
# <a name="logged-vs-unlogged-modifications"></a>Modificações registradas vs. não registradas
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Um aplicativo pode solicitar que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client não faça log de modificações de **Text**, **ntext**e **Image** . No entanto, tome cuidado ao usar essa opção. Ele deve ser usado somente para as situações em que os dados **Text**, **ntext**ou **Image** não são críticos e os proprietários de dados estão dispostos a compensar a capacidade de recuperar dados para um melhor desempenho.  
  
 O registro em log de modificações de **Text**, **ntext**e **Image** é controlado chamando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) com o parâmetro de *atributo* definido como SQL_SOPT_SS_ TEXTPTR_LOGGING e *ValuePtr* definido como SQL_TL_ON ou SQL_TL_OFF.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciando colunas de texto e imagem](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
