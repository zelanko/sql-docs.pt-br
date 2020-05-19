---
title: Modificações registradas em log versus não registradas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3635fee71c92196cbc9408db1487e95da2b489ea
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718763"
---
# <a name="logged-vs-unlogged-modifications"></a>Modificações registradas vs. não registradas
  Um aplicativo pode solicitar que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client não faça log de modificações de **Text**, **ntext**e **Image** . No entanto, tome cuidado ao usar essa opção. Ele deve ser usado somente para as situações em que os dados **Text**, **ntext**ou **Image** não são críticos e os proprietários de dados estão dispostos a compensar a capacidade de recuperar dados para um melhor desempenho.  
  
 O registro em log de modificações de **Text**, **ntext**e **Image** é controlado chamando [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) com o parâmetro de *atributo* definido como SQL_SOPT_SS_ TEXTPTR_LOGGING e *ValuePtr* definido como SQL_TL_ON ou SQL_TL_OFF.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciando colunas de texto e imagem](managing-text-and-image-columns.md)  
  
  
