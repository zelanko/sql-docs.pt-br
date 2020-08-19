---
description: Função SQLGetConnectOption
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df3fd7dc9a024348c4371fabdbcabfab63a6f071
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421280"
---
# <a name="sqlgetconnectoption-function"></a>Função SQLGetConnectOption
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: preterida  
  
 **Resumo**  
 No ODBC *3. x*, a função ODBC *2. x* **SQLGetConnectOption** foi substituída por **SQLGetConnectAttr**. Para obter mais informações, consulte [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md).  
  
> [!NOTE]
>  Para obter mais informações sobre como o Gerenciador de driver mapeia essa função quando um aplicativo ODBC *2. x* está trabalhando com um driver ODBC *3. x* , consulte [mapeando funções preteridas](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) no apêndice G: diretrizes de driver para compatibilidade com versões anteriores.  
> 
> [!NOTE]
>  O atributo SQL_ASYNC_DBC_FUNCTION_ENABLE introduzido no ODBC 3,8 não é suportado pelo **SQLGetConnectOption**. Os aplicativos que usam a operação assíncrona em um identificador de conexão devem usar **SQLGetConnectAttr**.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
