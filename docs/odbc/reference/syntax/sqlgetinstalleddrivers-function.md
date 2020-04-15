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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24793473bf4f25253ac11673df852d10cfb2c558
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303323"
---
# <a name="sqlgetinstalleddrivers-function"></a>Função SQLGetInstalledDrivers
**Conformidade**  
 Versão introduzida: ODBC 1.0  
  
 **Resumo**  
 **SQLGetInstalledDrivers** lê a seção [Drivers ODBC] das informações do sistema e retorna uma lista de descrições dos drivers instalados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
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
  
 *pcbbufOut*  
 [Saída] Número total de bytes (excluindo o byte de rescisão nula) retornado em *lpszBuf*. Se o número de bytes disponíveis para retornar for maior ou igual ao *cbBufMax,* a lista de descrições de driver em *lpszBuf* é truncada para *cbBufMax* menos o caractere de rescisão nula. O *argumento pcbBufOut* pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **sqlGetInstalledDrivers** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O argumento *lpszBuf* era NULO ou inválido, ou o argumento *cbBufMax* era menor ou igual a 0.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente não encontrado no registro|O instalador não conseguiu encontrar a seção [Drivers ODBC] no registro.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Cada descrição do driver é terminada com um byte nulo, e toda a lista é encerrada com um byte nulo. (Ou seja, dois bytes nulos marcam o fim da lista.) Se o buffer alocado não for grande o suficiente para manter a lista inteira, a lista será truncada sem erro. Um erro é devolvido se um ponteiro nulo for aprovado como *lpszBuf*.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando descrições e atributos do driver|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
