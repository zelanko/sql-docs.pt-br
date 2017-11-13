---
title: "Função SQLPostInstallerError | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f7d3a6bec7c12e271c073d5665c0a4e9b227ceef
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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

