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
ms.openlocfilehash: ac7fb545938a0ec5f212e9c0da867fbea5db4817
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536621"
---
# <a name="sqlpostinstallererror-function"></a>Função SQLPostInstallerError
**Conformidade com**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLPostInstallerError** fornece um mecanismo para uma biblioteca de instalação de driver ou conversor para relatar erros para o **ConfigDriver**, **ConfigDSN**, e **ConfigTranslator**  funções para a fila de erros do instalador. Os aplicativos não usam essa API; eles usam **SQLInstallerError** para recuperar o erro.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
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
