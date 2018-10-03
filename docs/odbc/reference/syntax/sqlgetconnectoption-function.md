---
title: Função SQLGetConnectOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectOption
helpviewer_keywords:
- SQLGetConnectOption function [ODBC]
ms.assetid: 59cde899-7957-4b5e-8677-f34d3b859bfd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44504acd59b19b8e23b97149ed94ed0f79016d16
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722384"
---
# <a name="sqlgetconnectoption-function"></a>Função SQLGetConnectOption
**Conformidade com**  
 Versão introduziu: Conformidade de padrões 1.0 ODBC: Deprecated  
  
 **Resumo**  
 Em ODBC 3 *. x*, o ODBC 2 *. x* função **SQLGetConnectOption** foi substituído pelo **SQLGetConnectAttr**. Para obter mais informações, consulte [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 2 *. x* aplicativo está funcionando com um ODBC 3 *. x* driver, consulte [preterido funções de mapeamento de](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores.  
  
> [!NOTE]  
>  Não há suporte para o atributo SQL_ASYNC_DBC_FUNCTION_ENABLE introduzidas no ODBC 3.8 por **SQLGetConnectOption**. Aplicativos que usam a operação assíncrona em um identificador de conexão devem usar **SQLGetConnectAttr**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
