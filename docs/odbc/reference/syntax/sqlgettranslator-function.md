---
title: "Função SQLGetTranslator | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLGetTranslator
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetTranslator
helpviewer_keywords: SQLGetTranslator function [ODBC]
ms.assetid: 33879db3-5ef9-4585-9be5-69376157e017
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5d8b0f18e683facc1316fd5a58ac1a2983acea63
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgettranslator-function"></a>Função SQLGetTranslator
**Conformidade**  
 Versão introduzidas: ODBC 2.0  
  
 **Resumo**  
 **SQLGetTranslator** exibe uma caixa de diálogo na qual um usuário pode selecionar um conversor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Identificador da janela pai.  
  
 *lpszName*  
 [Entrada/saída] Nome do tradutor das informações do sistema.  
  
 *cbNameMax*  
 [Entrada] Comprimento máximo do *lpszName* buffer.  
  
 *pcbNameOut*  
 [Entrada/saída] Número total de bytes (excluindo o byte nulo de terminação) passado ou retornado em *lpszName*. Se o número de bytes disponíveis para retornar é maior que ou igual a *cbNameMax*, o nome do conversor no *lpszName* será truncado para *cbNameMax* menos de caractere de terminação nula. O *pcbNameOut* argumento pode ser um ponteiro nulo.  
  
 *lpszPath*  
 [Saída] Caminho completo da DLL de tradução.  
  
 *cbPathMax*  
 [Entrada] Comprimento máximo do *lpszPath* buffer.  
  
 *pcbPathOut*  
 [Saída] Número total de bytes (excluindo o byte nulo de terminação) retornado em *lpszPath*. Se o número de bytes disponíveis para retornar é maior que ou igual a *cbPathMax*, o caminho de DLL de conversão em *lpszPath* será truncado para *cbPathMax* menos de caractere de terminação nula. O *pcbPathOut* argumento pode ser um ponteiro nulo.  
  
 *pvOption*  
 Opção de conversão de 32 bits [saída].  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedido e FALSO se ele falhar ou se o usuário cancelar a caixa de diálogo.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLGetTranslator** retorna FALSE, um tipo de  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O *cbNameMax* ou *cbPathMax* argumento era menor ou igual a 0.|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O *hwndParent* argumento era nulo ou inválido.|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou conversor inválido|O *lpszName* argumento era inválido. Ele não pôde ser encontrado no registro.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de instalação de driver ou conversor|Não foi possível carregar a biblioteca de conversor.|  
|ODBC_ERROR_INVALID_OPTION|Opção de transação inválido|O *pvOption* argumento continha um valor inválido.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido a uma falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Se *hwndParent* é nulo ou se *lpszName*, *lpszPath*, ou *pvOption* é um ponteiro nulo, **SQLGetTranslator** retorna FALSE. Caso contrário, ele exibe a lista de conversores instalados na caixa de diálogo a seguir.  
  
 ![Marque a caixa de diálogo conversor](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 Se *lpszName* contém um nome de conversor válido está selecionado. Caso contrário, \<nenhum conversor > está selecionada.  
  
 Se o usuário escolhe \<nenhum conversor >, o conteúdo de *lpszName*, *lpszPath*, e *pvOption* não são tocadas. **SQLGetTranslator** define *pcbNameOut* e *pcbPathOut* como 0 e retorna TRUE.  
  
 Se o usuário escolhe um conversor, **SQLGetTranslator** chamadas **ConfigTranslator** na instalação do tradutor DLL. Se **ConfigTranslator** retorna FALSE, **SQLGetTranslator** retorna para a caixa de diálogo. Se **ConfigTranslator** retorna TRUE, **SQLGetTranslator** retorna TRUE, junto com a opção de conversão, o caminho e o nome do conversor selecionado.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Configurando um conversor|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Obtendo um atributo de tradução|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definir um atributo de tradução|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
