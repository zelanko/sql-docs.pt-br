---
title: Função SQLGetInstalledDrivers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae0e24a902fdd3b021cfd6991edd3cf6f71099bf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetinstalleddrivers-function"></a>Função SQLGetInstalledDrivers
**Conformidade**  
 Versão introduzidas: ODBC 1.0  
  
 **Resumo**  
 **SQLGetInstalledDrivers** lê a seção [Drivers ODBC] as informações do sistema e retorna uma lista de descrições dos drivers instalados.  
  
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
 [Entrada] Comprimento de *lpszBuf*.  
  
 *pcbBufOut*  
 [Saída] Número total de bytes (excluindo o byte nulo de terminação) retornado em *lpszBuf*. Se o número de bytes disponíveis para retornar é maior que ou igual a *cbBufMax*, a lista de descrições de driver em *lpszBuf* será truncado para *cbBufMax* menos de caractere de terminação nula. O *pcbBufOut* argumento pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLGetInstalledDrivers** retorna FALSE, um tipo de  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O *lpszBuf* argumento era nulo ou inválido, ou o *cbBufMax* argumento era menor ou igual a 0.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente não encontrado no registro|O instalador não foi possível encontrar a seção [Drivers ODBC] no registro.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido a uma falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Cada descrição do driver é encerrada com um byte nulo e a lista inteira é encerrada com um byte nulo. (Ou seja, dois bytes nulos marcar o fim da lista.) Se o buffer alocado não for grande o suficiente para manter toda a lista, a lista será truncada sem erro. Um erro será retornado se um ponteiro nulo é passado como *lpszBuf*.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando atributos e descrições de driver|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
