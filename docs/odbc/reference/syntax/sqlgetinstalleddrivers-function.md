---
title: Função SQLGetInstalledDrivers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetInstalledDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInstalledDrivers
helpviewer_keywords:
- SQLGetInstalledDrivers function [ODBC]
ms.assetid: a1983a2e-0edf-422e-bd1b-ec5db40a34bc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9e7b079e2b66f4e1ba7b3233a6aaa20cd9908a67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061520"
---
# <a name="sqlgetinstalleddrivers-function"></a>Função SQLGetInstalledDrivers
**Conformidade**  
 Versão introduzida: ODBC 1,0  
  
 **Resumo**  
 O **SQLGetInstalledDrivers** lê a seção [drivers ODBC] das informações do sistema e retorna uma lista de descrições dos drivers instalados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszBuf*  
 Der Lista de descrições dos drivers instalados. Para obter informações sobre a estrutura da lista, consulte "Comentários".  
  
 *cbBufMax*  
 Entrada Comprimento de *lpszBuf*.  
  
 *pcbBufOut*  
 Der Número total de bytes (excluindo o byte de terminação nula) retornado em *lpszBuf*. Se o número de bytes disponíveis para retornar for maior ou igual a *cbBufMax*, a lista de descrições de driver em *lpszBuf* será truncada para *cbBufMax* menos o caractere de terminação nula. O argumento *pcbBufOut* pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLGetInstalledDrivers** retorna false, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|DESCRIÇÃO|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O argumento *lpszBuf* era nulo ou inválido, ou o argumento *cbBufMax* era menor ou igual a 0.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente não encontrado no registro|O instalador não pôde localizar a seção [drivers ODBC] no registro.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Cada descrição de driver é encerrada com um byte nulo e a lista inteira é encerrada com um byte nulo. (Ou seja, dois bytes nulos marcam o final da lista.) Se o buffer alocado não for grande o suficiente para manter a lista inteira, a lista será truncada sem erros. Um erro será retornado se um ponteiro NULL for passado como *lpszBuf*.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando descrições e atributos de driver|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
