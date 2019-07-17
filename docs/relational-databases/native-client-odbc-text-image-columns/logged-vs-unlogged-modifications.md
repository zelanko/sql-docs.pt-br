---
title: Modificações registradas vs. Não registradas modificações | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 91e832a0f2abdfea91a63f17414bf431e7275103
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128897"
---
# <a name="logged-vs-unlogged-modifications"></a>Modificações registradas vs. não registradas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Um aplicativo pode solicitar que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client não log **texto**, **ntext**, e **imagem** modificações. No entanto, tome cuidado ao usar essa opção. Ele deve ser usado somente para as situações em que o **texto**, **ntext**, ou **imagem** dados não são críticos e os proprietários de dados estão dispostos a trocar a possibilidade de recuperar dados para maior desempenho.  
  
 O registro em log do **texto**, **ntext**, e **imagem** modificações é controlado pela chamada [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) com o  *Atributo* parâmetro definido como sql_sopt_ss _ TEXTPTR_LOGGING e *ValuePtr* definido como SQL_TL_ON ou SQL_TL_OFF.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando colunas Text e Image](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
