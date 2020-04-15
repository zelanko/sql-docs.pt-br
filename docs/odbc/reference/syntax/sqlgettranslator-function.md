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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bcd5aeebab8539b8b94db56ff30892f4a7dbbac1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303267"
---
# <a name="sqlgettranslator-function"></a>Função SQLGetTranslator
**Conformidade**  
 Versão introduzida: ODBC 2.0  
  
 **Resumo**  
 **SQLGetTranslator** exibe uma caixa de diálogo a partir da qual um usuário pode selecionar um tradutor.  
  
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
 *Hwndparent*  
 [Entrada] Alça da janela dos pais.  
  
 *lpszName*  
 [Entrada/saída] Nome do tradutor das informações do sistema.  
  
 *cbNameMax*  
 [Entrada] Comprimento máximo do buffer *lpszName.*  
  
 *pcbNameOut*  
 [Entrada/saída] Número total de bytes (excluindo o byte de rescisão nula) passado ou devolvido em *lpszName*. Se o número de bytes disponíveis para retornar for maior ou igual ao *cbNameMax,* o nome do tradutor em *lpszName* será truncado para *cbNameMax* menos o caractere de rescisão nula. O *argumento pcbNameOut* pode ser um ponteiro nulo.  
  
 *lpszPath*  
 [Saída] Caminho completo da tradução DLL.  
  
 *cbPathMax*  
 [Entrada] Comprimento máximo do buffer *lpszPath.*  
  
 *pcbpathOut*  
 [Saída] Número total de bytes (excluindo o byte de rescisão nula) retornado em *lpszPath*. Se o número de bytes disponíveis para retornar for maior ou igual ao *cbPathMax,* o caminho dll de tradução no *lpszPath* é truncado para *cbPathMax* menos o caractere de rescisão nula. O *argumento pcbPathOut* pode ser um ponteiro nulo.  
  
 *pvOption*  
 Opção de tradução de 32 bits.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar ou se o usuário cancelar a caixa de diálogo.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLGetTranslator** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O argumento *cbNameMax* ou *cbPathMax* era menor ou igual a 0.|  
|ODBC_ERROR_INVALID_HWND|Alça de janela inválida|O argumento *hwndParent* era inválido ou NULO.|  
|ODBC_ERROR_INVALID_NAME|Nome de motorista ou tradutor inválido|O argumento *lpszName* era inválido. Não foi possível encontrar no registro.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de configuração do driver ou tradutor|A biblioteca de tradutores não pôde ser carregada.|  
|ODBC_ERROR_INVALID_OPTION|Opção de transação inválida|O *argumento pvOption* continha um valor inválido.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Se *hwndParent* for nulo ou se *lpszName,* *lpszPath*ou *pvOption* for um ponteiro nulo, **o SQLGetTranslator** retorna FALSO. Caso contrário, ele exibe a lista de tradutores instalados na caixa de diálogo a seguir.  
  
 ![Caixa de diálogo Selecionar Conversor](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 Se *lpszName* contiver um nome de tradutor válido, ele será selecionado. Caso contrário, \<nenhum tradutor> é selecionado.  
  
 Se o usuário \<escolher Não Tradutor>, o conteúdo de *lpszName,* *lpszPath*e *pvOption* não será tocado. **SQLGetTranslator** define *pcbNameOut* e *pcbPathOut* para 0 e retorna TRUE.  
  
 Se o usuário escolher um tradutor, **o SQLGetTranslator** chamará O Tradutor de **Config** na Configuração DLL do tradutor. Se **ConfigTranslator** retornar FALSE, **SQLGetTranslator** retorna à sua caixa de diálogo. Se **ConfigTranslator** retornar TRUE, **SQLGetTranslator** retorna TRUE, juntamente com a opção de nome, caminho e tradução do tradutor selecionado.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Configurando um tradutor|[Tradutor de config](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Obtendo um atributo de tradução|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definindo um atributo de tradução|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
