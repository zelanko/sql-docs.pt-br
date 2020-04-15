---
title: Verificação de valor do argumento | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298814"
---
# <a name="argument-value-checks"></a>Verificações de valor de argumento
O Driver Manager verifica os seguintes tipos de argumentos. Salvo observação em contrário, o Driver Manager retorna SQL_ERROR por erros nos valores de argumento.  
  
-   As alças de ambiente, conexão e declaração geralmente não podem ser ponteiros nulos. O Driver Manager retorna SQL_INVALID_HANDLE quando encontrar uma alça nula.  
  
-   Os argumentos de ponteiro necessários, como *OutputHandlePtr* no **SQLAllocHandle** e *CursorName* no **SQLSetCursorName,** não podem ser ponteiros nulos.  
  
-   As bandeiras de opção que não suportam valores específicos do motorista devem ser um valor legal. Por exemplo, *a operação* em **SQLSetPos** deve ser SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE ou SQL_ADD.  
  
-   Os sinalizadores de opção devem ser suportados na versão do ODBC suportado pelo driver. Por exemplo, *o InfoType* no **SQLGetInfo** não pode ser SQL_ASYNC_MODE (introduzido no ODBC 3.0) ao chamar um driver ODBC 2.0.  
  
-   Os números da coluna e dos parâmetros devem ser maiores ou superiores a 0, dependendo da função. O driver deve verificar o limite superior desses valores de argumento com base no conjunto de resultados atual ou na declaração SQL.  
  
-   Os argumentos de comprimento/indicador e os argumentos de comprimento do buffer de dados devem conter valores apropriados. Por exemplo, o argumento que especifica o comprimento de um nome de tabela em **SQLColumns** *(NameLength3)* deve ser SQL_NTS ou um valor maior que 0; *BufferLength* em **SQLDescribeCol** deve ser maior ou igual a 0. O motorista também pode precisar verificar esses argumentos. Por exemplo, ele pode verificar se *NameLength3* é menor ou igual ao comprimento máximo de um nome de tabela na fonte de dados.
