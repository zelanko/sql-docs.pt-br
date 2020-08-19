---
description: Função SQLGetTranslator
title: Função SQLGetTranslator | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTranslator
helpviewer_keywords:
- SQLGetTranslator function [ODBC]
ms.assetid: 33879db3-5ef9-4585-9be5-69376157e017
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d30268c846af4e95298d00edcd13def97c20c77d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421220"
---
# <a name="sqlgettranslator-function"></a>Função SQLGetTranslator
**Conformidade**  
 Versão introduzida: ODBC 2,0  
  
 **Resumo**  
 **SQLGetTranslator** exibe uma caixa de diálogo da qual um usuário pode selecionar um tradutor.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLGetTranslator(  
     HWND      hwndParent,  
     LPSTR     lpszName,  
     WORD      cbNameMax,  
     WORD *    pcbNameOut,  
     LPSTR     lpszPath,  
     WORD      cbPathMax,  
     WORD *    pcbPathOut,  
     DWORD *   pvOption);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hwndParent*  
 Entrada Identificador de janela pai.  
  
 *lpszName*  
 [Entrada/saída] Nome do tradutor a partir das informações do sistema.  
  
 *cbNameMax*  
 Entrada Comprimento máximo do buffer *lpszName* .  
  
 *pcbNameOut*  
 [Entrada/saída] Número total de bytes (exceto o byte de terminação nula) passados ou retornados em *lpszName*. Se o número de bytes disponíveis para retornar for maior ou igual a *cbNameMax*, o nome do tradutor em *lpszName* será truncado para *cbNameMax* menos o caractere de terminação nula. O argumento *pcbNameOut* pode ser um ponteiro nulo.  
  
 *lpszPath*  
 Der Caminho completo da DLL de tradução.  
  
 *cbPathMax*  
 Entrada Comprimento máximo do buffer *lpszPath* .  
  
 *pcbPathOut*  
 Der Número total de bytes (excluindo o byte de terminação nula) retornado em *lpszPath*. Se o número de bytes disponíveis para retornar for maior ou igual a *cbPathMax*, o caminho da DLL de tradução em *lpszPath* será truncado para *cbPathMax* menos o caractere de terminação nula. O argumento *pcbPathOut* pode ser um ponteiro nulo.  
  
 *pvOption*  
 [Saída] opção de conversão de 32 bits.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar ou se o usuário cancelar a caixa de diálogo.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLGetTranslator** retorna false, um valor * \* pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \* pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O argumento *cbNameMax* ou *cbPathMax* era menor ou igual a 0.|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O argumento *hwndParent* era inválido ou nulo.|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou tradutor inválido|O argumento *lpszName* era inválido. Ele não foi encontrado no registro.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de instalação do driver ou do Tradutor|Não foi possível carregar a biblioteca de tradutores.|  
|ODBC_ERROR_INVALID_OPTION|Opção de transação inválida|O argumento *pvOption* continha um valor inválido.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Se *hwndParent* for nulo ou se *lpszName*, *lpszPath*ou *pvOption* for um ponteiro nulo, **SQLGetTranslator** retornará false. Caso contrário, ele exibirá a lista de tradutores instalados na caixa de diálogo a seguir.  
  
 ![Caixa de diálogo Selecionar Conversor](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 Se *lpszName* contiver um nome de Tradutor válido, ele será selecionado. Caso contrário, \<No Translator> é selecionado.  
  
 Se o usuário escolher \<No Translator> , o conteúdo de *lpszName*, *lpszPath*e *pvOption* não será tocado. **SQLGetTranslator** define *pcbNameOut* e *PCBPATHOUT* como 0 e retorna true.  
  
 Se o usuário escolher um tradutor, **SQLGetTranslator** chamará **ConfigTranslator** na DLL de instalação do tradutor. Se **ConfigTranslator** retornar false, **SQLGetTranslator** retornará para sua caixa de diálogo. Se **ConfigTranslator** retornar true, **SQLGetTranslator** retornará true, junto com o nome do tradutor, o caminho e a opção de conversão selecionados.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Configurando um tradutor|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Obtendo um atributo de tradução|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Configurando um atributo de tradução|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
