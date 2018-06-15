---
title: Função SQLPostInstallerError | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b34cef9e116bd75b5394cfe86e5f8784f0ff152
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916881"
---
# <a name="sqlpostinstallererror-function"></a>Função SQLPostInstallerError
**Conformidade**  
 Versão introduzidas: ODBC 3.0  
  
 **Resumo**  
 **SQLPostInstallerError** fornece um mecanismo para uma biblioteca de instalação de driver ou conversor para relatar erros para o **ConfigDriver**, **ConfigDSN**, e **ConfigTranslator**  funções para a fila de erros do instalador. Aplicativos não usar essa API; eles usam **SQLInstallerError** para recuperar o erro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>Argumentos  
 *fErrorCode*  
 [Entrada] Código de erro do instalador.  
  
 *szErrorMsg*  
 [Entrada] Texto da mensagem de erro.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS ou SQL_ERROR.  
  
## <a name="diagnostics"></a>diagnóstico  
 **SQLPostInstallerError** não lançar valores de erro para si mesmo. Se o erro foi lançado com êxito para a fila de erros do instalador (recuperáveis usando **SQLInstallerError**), SQL_SUCCESS é retornado. SQL_ERROR será retornado se o valor de *dwErrorCode* argumento não é um dos códigos de erro de instalador especificado.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionar, modificar ou remover um driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|Adicionar, modificar ou remover fontes de dados|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|Definir uma opção de conversão|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|
