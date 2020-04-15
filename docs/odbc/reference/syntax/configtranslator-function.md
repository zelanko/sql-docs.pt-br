---
title: Função ConfigTranslator | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigTranslator
helpviewer_keywords:
- ConfigTranslator [ODBC]
ms.assetid: 7c22f07e-36de-425b-aa67-e32a84afae92
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb2f26f87854d74a217885010014633963472787
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306027"
---
# <a name="configtranslator-function"></a>Função ConfigTranslator
**Conformidade**  
 Versão introduzida: ODBC 2.0  
  
 **Resumo**  
 **ConfigTranslator** retorna uma opção de tradução padrão para um tradutor. Pode estar no DLL tradutor ou em uma configuração separada DLL.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hwndparent*  
 [Entrada] Alça da janela dos pais. A função não exibirá nenhuma caixa de diálogo se a alça estiver nula.  
  
 *pvOption*  
 [Saída] Uma opção de tradução de 32 bits.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o ConfigTranslator** retorna FALSE, um valor * \*pfErrorCode* associado é postado no buffer de erro do instalador por uma chamada para **SQLPostInstallerError** e pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Alça de janela inválida|O argumento *hwndParent* era inválido ou NULO.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Erro específico do driver ou tradutor|Um erro específico do driver para o qual não há um erro de instalador ODBC definido. O argumento *SzError* em uma chamada para a função **SQLPostInstallerError** deve conter a mensagem de erro específica do driver.|  
|ODBC_ERROR_INVALID_OPTION|Opção de tradução inválida|O *argumento pvOption* continha um valor inválido.|  
  
## <a name="comments"></a>Comentários  
 Se o tradutor suportar apenas uma única opção de tradução, **o ConfigTranslator** retorna TRUE e define *pvOption* para a opção de 32 bits. Caso contrário, ele determina a opção de tradução padrão a ser usada. **ConfigTranslator** pode exibir uma caixa de diálogo com a qual um usuário seleciona uma opção de tradução padrão.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtendo uma opção de tradução|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Selecionando um tradutor|[SqlGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Definindo uma opção de tradução|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
