---
title: Usando autofetch com cursors ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 812f4742dfe8273c4e96fc5205626fe1f6c07347
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298406"
---
# <a name="using-autofetch-with-odbc-cursors"></a>Usando a opção Autofetch com cursores ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Quando conectado a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância de , o driver Cliente Nativo ODBC suporta uma opção de autofetch ao usar qualquer tipo de cursor de servidor. Com o autofetch, a função **SQLExecute** ou **SQLExecDirect** que abre o cursor também tem uma função [sqlfetchscroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)(SQL_FIRST) implícita. As linhas que formam o primeiro conjunto de linhas são retornadas para as variáveis associadas de aplicativo como parte da execução da instrução, evitando outra viagem de ida e volta pela rede até o servidor. [O SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) não é suportado quando a opção autofetch está ativada; as colunas de conjunto de resultados devem ser vinculadas às variáveis do programa.  
  
 Os aplicativos solicitam autofetch definindo o atributo de instrução SQL_SOPT_SS_CURSOR_OPTIONS específico de driver como SQL_CO_AF.  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhes da programação do cursor &#40;&#41;da ODBC](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
