---
title: Logado vs. Modificações Não Registradas | Microsoft Docs
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
ms.openlocfilehash: dc7fb913bef4083b045a0c1c010bdedbc43135c5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297637"
---
# <a name="logged-vs-unlogged-modifications"></a>Modificações registradas vs. não registradas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Um aplicativo pode [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicitar que o driver ODBC do Cliente Nativo não registre **texto,** **ntext**e modificações **de imagem.** No entanto, tome cuidado ao usar essa opção. Ele deve ser usado apenas para as situações em que o **texto**, **ntext**, ou dados **de imagem** não são críticos e os proprietários de dados estão dispostos a negociar a capacidade de recuperar dados para um desempenho mais elevado.  
  
 O registro de **texto,** **ntext**e modificações **de imagem** é controlado ligando para [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) com o parâmetro *Atributo* definido para SQL_SOPT_SS_ TEXTPTR_LOGGING e *ValuePtr* definido como SQL_TL_ON ou SQL_TL_OFF.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciando colunas de texto e imagem](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
