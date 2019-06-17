---
title: Verificações de valor do argumento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3dfee0dd00e30f6446430156617ba45a5a39b994
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288546"
---
# <a name="argument-value-checks"></a>Verificações de valor de argumento
O Gerenciador de Driver verifica os seguintes tipos de argumentos. A menos que indicado o contrário, o Gerenciador de Driver retornará SQL_ERROR para erros em valores de argumento.  
  
-   Identificadores de ambiente, conexão e instrução geralmente não podem ser ponteiros nulos. O Gerenciador de Driver retorne SQL_INVALID_HANDLE quando ele encontra um identificador nulo.  
  
-   Necessários argumentos de ponteiro, como *OutputHandlePtr* na **SQLAllocHandle** e *CursorName* na **SQLSetCursorName**, não pode ser Ponteiros nulos.  
  
-   Sinalizadores de opção que não dão suporte a valores específicos de driver devem ser um valor válido. Por exemplo, *operação* na **SQLSetPos** deve ser SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE ou SQL_ADD.  
  
-   Sinalizadores de opção devem ter suporte na versão do ODBC com suporte pelo driver. Por exemplo, *tipo de informação* na **SQLGetInfo** não pode ser SQL_ASYNC_MODE (introduzida no ODBC 3.0) ao chamar um driver ODBC 2.0.  
  
-   Números de coluna e o parâmetro devem ser maior que 0 ou maior ou igual a 0, dependendo da função. O driver deve verificar o limite superior desses valores de argumento com base no conjunto de resultados atual ou instrução SQL.  
  
-   Argumentos de comprimento/indicador e argumentos de comprimento de buffer de dados devem conter valores apropriados. Por exemplo, o argumento que especifica o comprimento de um nome de tabela em **SQLColumns** (*NameLength3*) deve ser SQL_NTS ou um valor maior que 0. *BufferLength* na **SQLDescribeCol** deve ser maior que ou igual a 0. O driver também talvez seja necessário verificar esses argumentos. Por exemplo, é possível verificar que *NameLength3* é menor que ou igual ao comprimento máximo de um nome de tabela na fonte de dados.
