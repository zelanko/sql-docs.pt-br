---
title: Função SQLRemoveTranslator | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveTranslator
helpviewer_keywords:
- SQLRemoveTranslator function [ODBC]
ms.assetid: c6feda49-0359-4224-8de9-77125cf2397b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a577a868f7b56a6677da3cb12cfb29057ea66f6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68024526"
---
# <a name="sqlremovetranslator-function"></a>Função SQLRemoveTranslator
**Conformidade**  
 Versão introduzida: ODBC 3,0  
  
 **Resumo**  
 **SQLRemoveTranslator** remove informações sobre um tradutor da seção Odbcinst. ini das informações do sistema e decrementa a contagem de uso de componentes do tradutor em 1.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszTranslator*  
 Entrada O nome do tradutor, conforme registrado na chave Odbcinst. ini das informações do sistema.  
  
 *lpdwUsageCount*  
 Der A contagem de uso do tradutor depois que essa função foi chamada.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar. Se não existir nenhuma entrada nas informações do sistema quando essa função for chamada, a função retornará FALSE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLRemoveTranslator** retorna false, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|DESCRIÇÃO|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente não encontrado no registro|O instalador não pôde remover as informações do tradutor porque ele não existia no registro ou não pôde ser encontrado no registro.|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou tradutor inválido|O argumento *lpszTranslator* era inválido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de uso do componente|O instalador não pôde decrementar a contagem de uso do driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLRemoveTranslator** complementa a função [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) e atualiza a contagem de uso do componente nas informações do sistema. Essa função deve ser chamada somente de um aplicativo de instalação.  
  
 **SQLRemoveTranslator** reduzirá a contagem de uso do componente em 1. Se a contagem de uso do componente for para 0, a entrada do tradutor nas informações do sistema será removida. A entrada do tradutor está no seguinte local nas informações do sistema, sob o nome do Tradutor:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 Na verdade, o **SQLRemoveTranslator** não remove nenhum arquivo. O programa de chamada é responsável por excluir arquivos e manter a contagem de uso do arquivo. Somente após a contagem de uso do componente e a contagem de uso do arquivo ter atingido zero é um arquivo excluído fisicamente. Alguns arquivos em um componente podem ser excluídos e outros não excluídos, dependendo se os arquivos são usados por outros aplicativos que incrementaram a contagem de uso do arquivo.  
  
 **SQLRemoveTranslator** também é chamado como parte de um processo de atualização. Se um aplicativo detectar que deve executar uma atualização e tiver instalado anteriormente o driver, o driver deverá ser removido e reinstalado. **SQLRemoveTranslator** deve ser chamado primeiro para decrementar a contagem de uso do componente e, em seguida, **SQLInstallTranslatorEx** deve ser chamado para incrementar a contagem de uso do componente. O programa de instalação do aplicativo deve substituir fisicamente os arquivos antigos pelos novos arquivos. A contagem de uso do arquivo permanecerá a mesma, e outros aplicativos que usam os arquivos de versão mais antigos agora usarão a versão mais recente.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Instalando um tradutor|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
