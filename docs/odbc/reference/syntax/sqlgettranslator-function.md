---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1f1c5bbfd2e2fbf91fd9e91acafe0bc72d006d3f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63132762"
---
# <a name="sqlgettranslator-function"></a>Função SQLGetTranslator
**Conformidade com**  
 Versão introduzida: ODBC 2.0  
  
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
 [Entrada] Identificador de janela pai.  
  
 *lpszName*  
 [Entrada/saída] Nome do tradutor de informações do sistema.  
  
 *cbNameMax*  
 [Entrada] Comprimento máximo do *lpszName* buffer.  
  
 *pcbNameOut*  
 [Entrada/saída] Número total de bytes (excluindo o byte nulo de terminação) passado ou retornado em *lpszName*. Se o número de bytes disponíveis para retornar for maior que ou igual a *cbNameMax*, o nome do tradutor na *lpszName* será truncado com *cbNameMax* menos o caractere de finalização null. O *pcbNameOut* argumento pode ser um ponteiro nulo.  
  
 *lpszPath*  
 [Saída] Caminho completo da DLL de tradução.  
  
 *cbPathMax*  
 [Entrada] Comprimento máximo do *lpszPath* buffer.  
  
 *pcbPathOut*  
 [Saída] Número total de bytes (excluindo o byte nulo de terminação) retornado em *lpszPath*. Se o número de bytes disponíveis para retornar for maior que ou igual a *cbPathMax*, o caminho DLL de conversão na *lpszPath* será truncado com *cbPathMax* menos o caractere de finalização null. O *pcbPathOut* argumento pode ser um ponteiro nulo.  
  
 *pvOption*  
 Opção de conversão de 32 bits do [saída].  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedido e FALSO se ele falhar ou se o usuário cancelar a caixa de diálogo.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLGetTranslator** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O *cbNameMax* ou *cbPathMax* argumento era menor que ou igual a 0.|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O *hwndParent* argumento era inválido ou nulo.|  
|ODBC_ERROR_INVALID_NAME|Nome inválido de driver ou conversor|O *lpszName* argumento era inválido. Ele não pôde ser encontrado no registro.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de instalação do driver ou conversor|Não foi possível carregar a biblioteca de tradução.|  
|ODBC_ERROR_INVALID_OPTION|Opção de transação inválido|O *pvOption* argumento continha um valor inválido.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Se *hwndParent* é nulo ou se *lpszName*, *lpszPath*, ou *pvOption* é um ponteiro nulo, **SQLGetTranslator** retorna FALSE. Caso contrário, ele exibe a lista de conversores instalados na caixa de diálogo a seguir.  
  
 ![Marque a caixa de diálogo tradução](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 Se *lpszName* contém um nome válido de tradução, ele é selecionado. Caso contrário, \<tradutor não > está selecionada.  
  
 Se o usuário escolhe \<tradutor não >, o conteúdo de *lpszName*, *lpszPath*, e *pvOption* não são tocadas. **SQLGetTranslator** define *pcbNameOut* e *pcbPathOut* como 0 e retornará TRUE.  
  
 Se o usuário escolhe um tradutor **SQLGetTranslator** chamadas **ConfigTranslator** na DLL de instalação do tradutor. Se **ConfigTranslator** retorna FALSE, o **SQLGetTranslator** retorna à sua caixa de diálogo. Se **ConfigTranslator** retorna TRUE, **SQLGetTranslator** retorna TRUE, junto com a opção de tradução, o caminho e nome do tradutor selecionado.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Configurando um tradutor|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Obtendo um atributo de tradução|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definir um atributo de tradução|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
