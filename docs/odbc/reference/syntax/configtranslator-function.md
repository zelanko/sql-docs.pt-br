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
ms.openlocfilehash: 18bf7e3f66140ef92b520ea7c86b616ea7067b16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68016704"
---
# <a name="configtranslator-function"></a>Função ConfigTranslator
**Conformidade**  
 Versão introduzida: ODBC 2,0  
  
 **Resumo**  
 **ConfigTranslator** retorna uma opção de conversão padrão para um tradutor. Ele pode estar na DLL do tradutor ou em uma DLL de instalação separada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hwndParent*  
 Entrada Identificador de janela pai. A função não exibirá nenhuma caixa de diálogo se o identificador for nulo.  
  
 *pvOption*  
 Der Uma opção de conversão de 32 bits.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **ConfigTranslator** retorna false, um valor de * \*pfErrorCode* associado é Postado no buffer de erros do instalador por uma chamada para **SQLPostInstallerError** e pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|DESCRIÇÃO|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O argumento *hwndParent* era inválido ou nulo.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Erro específico do driver ou do Tradutor|Um erro específico de driver para o qual não há erro de instalador ODBC definido. O argumento *SzError* em uma chamada para a função **SQLPostInstallerError** deve conter a mensagem de erro específica do driver.|  
|ODBC_ERROR_INVALID_OPTION|Opção de conversão inválida|O argumento *pvOption* continha um valor inválido.|  
  
## <a name="comments"></a>Comentários  
 Se o tradutor der suporte apenas a uma única opção de conversão, **ConfigTranslator** retornará true e definirá *pvOption* como a opção de 32 bits. Caso contrário, ele determina a opção de tradução padrão a ser usada. **ConfigTranslator** pode exibir uma caixa de diálogo com a qual um usuário seleciona uma opção de conversão padrão.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtendo uma opção de conversão|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Selecionando um tradutor|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Configurando uma opção de conversão|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
