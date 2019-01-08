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
manager: craigg
ms.openlocfilehash: 173346c990e388935c800d76069f97ee9cf3f399
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53212515"
---
# <a name="sqlgetinstalleddrivers-function"></a>Função SQLGetInstalledDrivers
**Conformidade com**  
 Versão introduzida: ODBC 1.0  
  
 **Resumo**  
 **SQLGetInstalledDrivers** lê a seção [ODBC Drivers] as informações do sistema e retorna uma lista de descrições dos drivers instalados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszBuf*  
 [Saída] Lista de descrições dos drivers instalados. Para obter informações sobre a estrutura da lista, consulte "Comentários".  
  
 *cbBufMax*  
 [Entrada] Comprimento da *lpszBuf*.  
  
 *pcbBufOut*  
 [Saída] Número total de bytes (excluindo o byte nulo de terminação) retornado em *lpszBuf*. Se o número de bytes disponíveis para retornar for maior que ou igual a *cbBufMax*, a lista de descrições de driver no *lpszBuf* será truncado com *cbBufMax* menos o caractere de finalização null. O *pcbBufOut* argumento pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLGetInstalledDrivers** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O *lpszBuf* argumento era nulo ou inválido, ou o *cbBufMax* argumento era menor que ou igual a 0.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Não foi encontrado no registro do componente|O instalador não foi possível encontrar a seção [ODBC Drivers] no registro.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Descrição de cada driver é encerrada com um byte nulo e a lista inteira é encerrada com um byte nulo. (Ou seja, dois bytes nulos marcam o final da lista.) Se o buffer alocado não for grande o suficiente para manter toda a lista, a lista será truncada sem erro. Um erro será retornado se um ponteiro nulo é passado como *lpszBuf*.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando atributos e descrições de driver|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
