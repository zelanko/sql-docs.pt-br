---
title: Verificações de valor de argumento | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c6e4de16c4a1a80be893acbc7a1993b375f2fee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298814"
---
# <a name="argument-value-checks"></a>Verificações de valor de argumento
O Gerenciador de driver verifica os seguintes tipos de argumentos. Salvo indicação em contrário, o Gerenciador de driver retorna SQL_ERROR para erros em valores de argumento.  
  
-   Os identificadores de ambiente, de conexão e de instrução geralmente não podem ser ponteiros nulos. O Gerenciador de driver retorna SQL_INVALID_HANDLE quando encontra um identificador nulo.  
  
-   Argumentos de ponteiro necessários, como *OutputHandlePtr* em **SQLAllocHandle** e *cursorname* em **SQLSetCursorName**, não podem ser ponteiros nulos.  
  
-   Sinalizadores de opção que não dão suporte a valores específicos de driver devem ser um valor válido. Por exemplo, a *operação* em **SQLSetPos** deve ser SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE ou SQL_ADD.  
  
-   Os sinalizadores de opção devem ter suporte na versão do ODBC com suporte do driver. Por exemplo, *InfoType* em **SQLGetInfo** não pode ser SQL_ASYNC_MODE (introduzido no ODBC 3,0) ao chamar um driver ODBC 2,0.  
  
-   Os números de coluna e parâmetro devem ser maiores que 0 ou maiores ou iguais a 0, dependendo da função. O driver deve verificar o limite superior desses valores de argumento com base no conjunto de resultados atual ou na instrução SQL.  
  
-   Argumentos de comprimento/indicador e argumentos de comprimento do buffer de dados devem conter valores apropriados. Por exemplo, o argumento que especifica o comprimento de um nome de tabela em **SQLColumns** (*NameLength3*) deve ser SQL_NTS ou um valor maior que 0; *BufferLength* em **SQLDescribeCol** deve ser maior ou igual a 0. O driver também pode precisar verificar esses argumentos. Por exemplo, ele pode verificar se *NameLength3* é menor ou igual ao comprimento máximo de um nome de tabela na fonte de dados.
