---
title: Mensagens de erro (driver Visual FoxPro ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- SQLSTATE [ODBC]
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 58ea9734-4edf-44da-ba80-938aa7b340e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31f894e58da93fe6091dba306f8b765d14bac2cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286396"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>Mensagens de erro (Driver ODBC do Visual FoxPro)
Quando ocorre um erro, o driver Visual FoxPro retorna as seguintes informações:  
  
-   O número de erro nativo e o texto da mensagem de erro  
  
-   O sqlstate (um código de erro ODBC) e o texto da mensagem de erro  
  
 Você acessa essas informações de erro ligando para [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md).  
  
## <a name="native-errors"></a>Erros nativos  
 Para erros que ocorrem na fonte de dados, o driver Visual FoxPro retorna o número de erro nativo e o texto da mensagem de erro. Para obter uma lista de números de erro nativos, consulte [Visual FoxPro ODBC Driver Native Error Messages](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md).  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (códigos de erro ODBC)  
 Para erros detectados e devolvidos pelo driver Visual FoxPro, o driver mapeia o número de erro nativo devolvido para o SQLSTATE apropriado. Se um número de erro nativo não tiver um código de erro ODBC para mapear, o driver Visual FoxPro retorna SQLSTATE S1000 (erro geral).  
  
 Para obter uma lista de valores SQLSTATE gerados pelo Driver Visual FoxPro ODBC para erros correspondentes do Visual FoxPro, consulte Códigos de [erro ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).  
  
## <a name="syntax"></a>Sintaxe  
 As mensagens de erro têm o seguinte formato:  
  
 **[** *vendor* **[ODBC_component]** *ODBC_component* **]** *error_message*  
  
 Os prefixos entre parênteses ([]) identificam a origem do erro conforme definido na tabela a seguir.  
  
|Fonte de dados|Prefixo|Valor|  
|-----------------|------------|-----------|  
|Gerenciador de Driver|[fornecedor]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Gerente de Driver ODBC]<br />N/D|  
|Driver FoxPro visual|fornecedor]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Driver ODBC Visual FoxPro]<br />N/D|  
  
 Por exemplo, se o driver Visual FoxPro ODBC não conseguiu encontrar o arquivo employee.dbf, ele pode retornar a seguinte mensagem de erro:  
  
 *"[Microsoft*][*ODBC Visual FoxPro Driver*]Arquivo 'employee.dbf' não existe"
