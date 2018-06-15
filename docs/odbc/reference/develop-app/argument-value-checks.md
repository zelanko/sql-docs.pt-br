---
title: Verificações de valor do argumento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 46a947e362f9c6e614d4e28c50b7046048bf8fa0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908341"
---
# <a name="argument-value-checks"></a>Verificações de valor de argumento
O Gerenciador de Driver verifica os seguintes tipos de argumentos. Salvo indicação em contrário, o Gerenciador de Driver retornará SQL_ERROR para erros em valores de argumento.  
  
-   Geralmente, os identificadores de ambiente, conexão e instrução não podem ser ponteiros nulos. O Gerenciador de Driver retorne SQL_INVALID_HANDLE quando encontra um identificador nulo.  
  
-   Necessários argumentos de ponteiro, como *OutputHandlePtr* na **SQLAllocHandle** e *CursorName* na **SQLSetCursorName**, não pode ser Ponteiros nulos.  
  
-   Sinalizadores de opção que não oferecem suporte a valores específicos de driver devem ser um valor válido. Por exemplo, *operação* na **SQLSetPos** deve ser SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE ou SQL_ADD.  
  
-   Sinalizadores de opção devem ter suporte na versão do ODBC com suporte pelo driver. Por exemplo, *informação* na **SQLGetInfo** não pode ser SQL_ASYNC_MODE (introduzido no ODBC 3.0) ao chamar um driver ODBC 2.0.  
  
-   Números de coluna e o parâmetro devem ser maior que 0 ou maior que ou igual a 0, dependendo da função. O driver deve verificar o limite superior desses valores de argumento com base no conjunto de resultados atual ou instrução SQL.  
  
-   Argumentos de comprimento/indicador e argumentos de comprimento de buffer de dados devem conter valores apropriados. Por exemplo, o argumento que especifica o comprimento de um nome de tabela em **SQLColumns** (*NameLength3*) deve ser SQL_NTS ou um valor maior que 0; *BufferLength* na **SQLDescribeCol** deve ser maior que ou igual a 0. O driver também precisará verificar esses argumentos. Por exemplo, ele pode verificar que *NameLength3* é menor ou igual ao comprimento máximo de um nome de tabela na fonte de dados.
