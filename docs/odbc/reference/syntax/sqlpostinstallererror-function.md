---
title: Função SQLPostInstallerError | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPostInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPostInstallerError
helpviewer_keywords:
- SQLPostInstallerError function [ODBC]
ms.assetid: 4c60d827-b2d2-4f27-b220-daa9e1fcdd8d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0d5e0a10b8c530494fa3c026be0d36fde066a97c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053674"
---
# <a name="sqlpostinstallererror-function"></a>Função SQLPostInstallerError
**Conformidade**  
 Versão introduzida: ODBC 3,0  
  
 **Resumo**  
 O **SQLPostInstallerError** fornece um mecanismo para uma biblioteca de instalação de driver ou tradutor para relatar erros para as funções **ConfigDriver**, **ConfigDSN**e **ConfigTranslator** para a fila de erros do instalador. Os aplicativos não usam essa API; Eles usam **SQLInstallerError** para recuperar o erro.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>Argumentos  
 *fErrorCode*  
 Entrada Código de erro do instalador.  
  
 *szErrorMsg*  
 Entrada Texto da mensagem de erro.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS ou SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLPostInstallerError** não publica valores de erro para si mesmo. Se o erro foi Postado com êxito na fila de erros do instalador (recuperável usando **SQLInstallerError**), SQL_SUCCESS será retornado. SQL_ERROR será retornado se o valor no argumento *dwErrorCode* não for um dos códigos de erro do instalador especificados.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo um driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|Adicionando, modificando ou removendo fontes de dados|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|Configurando uma opção de conversão|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|
