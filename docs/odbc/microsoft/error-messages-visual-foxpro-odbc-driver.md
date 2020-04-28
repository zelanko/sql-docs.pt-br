---
title: Mensagens de erro (driver ODBC do Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286396"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>Mensagens de erro (Driver ODBC do Visual FoxPro)
Quando ocorre um erro, o driver do Visual FoxPro retorna as seguintes informações:  
  
-   O número do erro nativo e o texto da mensagem de erro  
  
-   O SQLSTATE (um código de erro ODBC) e o texto da mensagem de erro  
  
 Você acessa essas informações de erro chamando [SqlError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md).  
  
## <a name="native-errors"></a>Erros nativos  
 Para erros que ocorrem na fonte de dados, o driver do Visual FoxPro retorna o número de erro nativo e o texto da mensagem de erro. Para obter uma lista de números de erro nativos, consulte [mensagens de erro nativo do driver ODBC do Visual FoxPro](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md).  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (códigos de erro ODBC)  
 Para erros detectados e retornados pelo driver do Visual FoxPro, o driver mapeia o número de erro nativo retornado para o SQLSTATE apropriado. Se um número de erro nativo não tiver um código de erro ODBC para mapear, o driver do Visual FoxPro retornará SQLSTATE S1000 (erro geral).  
  
 Para obter uma lista de valores SQLSTATE gerados pelo driver ODBC do Visual FoxPro para erros correspondentes do Visual FoxPro, consulte [códigos de erro ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).  
  
## <a name="syntax"></a>Sintaxe  
 As mensagens de erro têm o seguinte formato:  
  
 **[** *fornecedor* **] [** *ODBC_component* **]** *ERROR_MESSAGE*  
  
 Os prefixos entre colchetes ([]) identificam a origem do erro, conforme definido na tabela a seguir.  
  
|Fonte de dados|Prefixo|Valor|  
|-----------------|------------|-----------|  
|Gerenciador de Driver|fabricante<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Gerenciador de driver ODBC]<br />N/D|  
|Driver do Visual FoxPro|fabricante<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Driver ODBC do Visual FoxPro]<br />N/D|  
  
 Por exemplo, se o driver ODBC do Visual FoxPro não pôde localizar o arquivo Employee. dbf, ele pode retornar a seguinte mensagem de erro:  
  
 O arquivo ' Employee. dbf '*do [Microsoft*] [*Driver do ODBC Visual FoxPro*] não existe "
