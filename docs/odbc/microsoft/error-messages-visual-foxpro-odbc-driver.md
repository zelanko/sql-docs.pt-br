---
title: Mensagens de erro (Driver ODBC do Visual FoxPro) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b24db48d6a76c221e72944e8e5e6826cb8d5d55
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127983"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>Mensagens de erro (Driver ODBC do Visual FoxPro)
Quando ocorre um erro, o driver do Visual FoxPro retorna as seguintes informações:  
  
-   O número de erro nativo e o texto da mensagem de erro  
  
-   O SQLSTATE (um código de erro ODBC) e o texto da mensagem de erro  
  
 Acessar essas informações de erro chamando [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md).  
  
## <a name="native-errors"></a>Erros nativos  
 Para erros que ocorrem na fonte de dados, o driver do Visual FoxPro retorna o número de erro nativo e o texto da mensagem de erro. Para obter uma lista de números de erro nativo, consulte [Visual FoxPro ODBC Driver nativo mensagens de erro](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md).  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (códigos de erro ODBC)  
 Para erros que são detectados e retornados pelo driver do Visual FoxPro, o driver mapeia o número de erro nativo retornado para o SQLSTATE apropriado. Se não tiver um código de erro ODBC para mapear para um número de erro nativo, o driver do Visual FoxPro retornará SQLSTATE S1000 (erro geral).  
  
 Para obter uma lista de valores SQLSTATE gerado pelo Visual FoxPro ODBC Driver para erros do Visual FoxPro correspondentes, consulte [códigos de erro ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).  
  
## <a name="syntax"></a>Sintaxe  
 Mensagens de erro têm o seguinte formato:  
  
 **[** *vendor* **][** *ODBC_component* **]** *error_message*  
  
 Os prefixos de colchetes ([]) identificam a origem do erro, conforme definido na tabela a seguir.  
  
|Fonte de dados|Prefixo|Valor|  
|-----------------|------------|-----------|  
|Gerenciador de Driver|[vendor]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Gerenciador de Driver ODBC]<br />N/D|  
|Driver do Visual FoxPro|vendor]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Driver do Visual FoxPro do ODBC]<br />N/D|  
  
 Por exemplo, se o Driver de ODBC do Visual FoxPro não foi possível encontrar a Employee. dbf de arquivo, ele pode retornar a mensagem de erro a seguir:  
  
 "[*Microsoft*] [*Driver ODBC do Visual FoxPro*] arquivo de 'Employee. dbf' não existe"
