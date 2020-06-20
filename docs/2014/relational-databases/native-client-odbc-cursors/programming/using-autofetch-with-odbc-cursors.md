---
title: Usando a busca prévia com cursores ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
author: rothja
ms.author: jroth
ms.openlocfilehash: e3d9374cf9ceab4a7e73cc0059783486f2bf9c41
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85020760"
---
# <a name="using-autofetch-with-odbc-cursors"></a>Usando a opção Autofetch com cursores ODBC
  Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client dá suporte a uma opção de AutoBusca ao usar qualquer tipo de cursor do servidor. Com a busca prévia, a função **SQLExecute** ou **SQLExecDirect** que abre o cursor também tem uma função implícita de [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)(SQL_FIRST). As linhas que formam o primeiro conjunto de linhas são retornadas para as variáveis associadas de aplicativo como parte da execução da instrução, evitando outra viagem de ida e volta pela rede até o servidor. Não há suporte para [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) quando a opção de AutoBusca está habilitada; as colunas do conjunto de resultados devem estar associadas a variáveis de programa.  
  
 Os aplicativos solicitam autofetch definindo o atributo de instrução SQL_SOPT_SS_CURSOR_OPTIONS específico de driver como SQL_CO_AF.  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhes de programação do cursor &#40;&#41;ODBC](cursor-programming-details-odbc.md)  
  
  
