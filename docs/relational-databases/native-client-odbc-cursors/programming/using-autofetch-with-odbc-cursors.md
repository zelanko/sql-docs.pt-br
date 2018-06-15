---
title: Usando a opção Autofetch com cursores ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-cursors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 557009d82a3136599795eb2412c2d216946d2dc8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32948421"
---
# <a name="using-autofetch-with-odbc-cursors"></a>Usando a opção Autofetch com cursores ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Quando conectado a uma instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece suporte a uma opção de autofetch ao usar qualquer tipo de cursor de servidor. Com a opção de autofetch, o **SQLExecute** ou **SQLExecDirect** função que abre o cursor também tem um implícita [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)função (SQL_FIRST). As linhas que formam o primeiro conjunto de linhas são retornadas para as variáveis associadas de aplicativo como parte da execução da instrução, evitando outra viagem de ida e volta pela rede até o servidor. [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) não é suportado quando a opção autofetch está habilitada, as colunas do conjunto de resultados devem ser associadas a variáveis de programa.  
  
 Os aplicativos solicitam autofetch definindo o atributo de instrução SQL_SOPT_SS_CURSOR_OPTIONS específico de driver como SQL_CO_AF.  
  
## <a name="see-also"></a>Consulte também  
 [Detalhes da programação de cursor &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
