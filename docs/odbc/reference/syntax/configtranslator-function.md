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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: edcffe36c0185276fae89f800e1bbcfc5bc33b33
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232018"
---
# <a name="configtranslator-function"></a>Função ConfigTranslator
**Conformidade com**  
 Versão introduzida: ODBC 2.0  
  
 **Resumo**  
 **ConfigTranslator** retorna uma opção de conversão padrão para um tradutor. Ele pode estar no tradutor de DLL ou uma DLL de instalação separado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hwndParent*  
 [Entrada] Identificador de janela pai. A função não exibirá nenhuma caixa de diálogo se o identificador for nulo.  
  
 *pvOption*  
 [Saída] Uma opção de conversão de 32 bits.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **ConfigTranslator** retornar FALSE, um associado  *\*pfErrorCode* valor é postado no buffer de erro do instalador por uma chamada para **SQLPostInstallerError**e pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O *hwndParent* argumento era inválido ou nulo.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Erro específico do driver ou do tradutor|Um erro específico do driver para o qual não há nenhum erro de instalador ODBC definido. O *SzError* argumento em uma chamada para o **SQLPostInstallerError** função deve conter a mensagem de erro específico do driver.|  
|ODBC_ERROR_INVALID_OPTION|Opção de conversão inválido|O *pvOption* argumento continha um valor inválido.|  
  
## <a name="comments"></a>Comentários  
 Se o conversor dá suporte a apenas uma opção de tradução única **ConfigTranslator** retornará TRUE e definirá *pvOption* para a opção de 32 bits. Caso contrário, ele determina que a opção de conversão padrão de uso. **ConfigTranslator** pode exibir uma caixa de diálogo com a qual um usuário seleciona uma opção de conversão padrão.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtendo uma opção de tradução|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Selecionando um tradutor|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Definir uma opção de tradução|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
