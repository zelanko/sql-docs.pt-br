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
manager: craigg
ms.openlocfilehash: 8dc70580de4f759a5adb6a501ac5dc200b62cba5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47716646"
---
# <a name="sqlpostinstallererror-function"></a>Função SQLPostInstallerError
**Conformidade com**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLPostInstallerError** fornece um mecanismo para uma biblioteca de instalação de driver ou conversor para relatar erros para o **ConfigDriver**, **ConfigDSN**, e **ConfigTranslator**  funções para a fila de erros do instalador. Os aplicativos não usam essa API; eles usam **SQLInstallerError** para recuperar o erro.  
  
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
  
## <a name="diagnostics"></a>Diagnóstico  
 **SQLPostInstallerError** não poste os valores de erro para si mesmo. Se o erro foi lançado com êxito para a fila de erros do instalador (usando recuperáveis **SQLInstallerError**), SQL_SUCCESS é retornado. SQL_ERROR será retornado se o valor de *dwErrorCode* argumento não é um dos códigos de erro de instalador especificado.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionar, modificar ou remover um driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|Adicionar, modificar ou remover fontes de dados|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|Definir uma opção de tradução|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|
