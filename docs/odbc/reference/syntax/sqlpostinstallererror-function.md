---
title: Função de erro do SQLPostInstaller | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cdceff5c4e175ba9f135c6e5e4405933b1a86b7c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306887"
---
# <a name="sqlpostinstallererror-function"></a>Função SQLPostInstallerError
**Conformidade**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **O SQLPostInstallerError** fornece um mecanismo para que uma biblioteca de configuração de driver ou tradutor reporte erros para as funções **ConfigDriver,** **ConfigDSN**e **ConfigTranslator** na fila de erros do instalador. Os aplicativos não usam esta API; eles usam **SQLInstallerError** para recuperar o erro.  
  
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
 [Entrada] Texto de mensagem de erro.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS ou SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLPostInstallerError** não posta valores de erro para si mesmo. Se o erro foi postado com sucesso na fila de erros do instalador (recuperável usando **SQLInstallerError),** SQL_SUCCESS será devolvido. SQL_ERROR serão devolvidos se o valor no argumento *dwErrorCode* não for um dos códigos de erro do instalador especificado.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo um driver|[Driver de configuração](../../../odbc/reference/syntax/configdriver-function.md)|  
|Adicionando, modificando ou removendo fontes de dados|[Configdsn](../../../odbc/reference/syntax/configdsn-function.md)|  
|Definindo uma opção de tradução|[Tradutor de config](../../../odbc/reference/syntax/configtranslator-function.md)|
