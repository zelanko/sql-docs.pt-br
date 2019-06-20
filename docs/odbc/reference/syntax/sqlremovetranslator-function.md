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
manager: craigg
ms.openlocfilehash: 42513e6dcf32e21030e56fd3b386800b7525f534
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537146"
---
# <a name="sqlremovetranslator-function"></a>Função SQLRemoveTranslator
**Conformidade com**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLRemoveTranslator** remove informações sobre um tradutor da seção Odbcinst. ini do informações do sistema e diminui a contagem de utilização de componente do tradutor em 1.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszTranslator*  
 [Entrada] O nome do tradutor como registrado na chave do Odbcinst. ini, as informações do sistema.  
  
 *lpdwUsageCount*  
 [Saída] A contagem de utilização do tradutor depois que essa função foi chamada.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar. Se não houver nenhuma entrada nas informações do sistema quando essa função é chamada, a função retorna FALSE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLRemoveTranslator** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Não foi encontrado no registro do componente|O instalador não foi possível remover as informações de tradução, porque não existia no registro ou não pôde ser encontrado no registro.|  
|ODBC_ERROR_INVALID_NAME|Nome inválido de driver ou conversor|O *lpszTranslator* argumento era inválido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de utilização de componente|O instalador não conseguiu reduzir a contagem de uso do driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLRemoveTranslator** complementa os [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) função e as atualizações o uso do componente contagem nas informações do sistema. Essa função deve ser chamada apenas de um aplicativo de instalação.  
  
 **SQLRemoveTranslator** diminuirá a contagem de uso do componente em 1. Se a contagem de uso do componente chegar a 0, será possível remover a entrada de tradução nas informações do sistema. A entrada do tradutor está no seguinte local nas informações do sistema, sob o nome do tradutor:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator** não remover todos os arquivos. O programa de chamada é responsável pela exclusão de arquivos e manter a contagem de uso de arquivos. Somente depois que a contagem de uso do componente e a contagem de uso de arquivos atingiu o zero é um arquivo excluído fisicamente. Alguns arquivos em um componente podem ser excluídos, e outras pessoas não excluído, dependendo se os arquivos são usados por outros aplicativos que têm aumentado a contagem de uso de arquivos.  
  
 **SQLRemoveTranslator** também é chamado como parte de um processo de atualização. Se um aplicativo detectar que ele deve realizar uma atualização e ele foi instalado anteriormente o driver, o driver deve ser removido e reinstalado. **SQLRemoveTranslator** deve ser chamada primeiro para diminuir a contagem de uso do componente e então **SQLInstallTranslatorEx** deve ser chamado para incrementar a contagem de uso do componente. O programa de instalação do aplicativo fisicamente deve substituir os arquivos antigos com os novos arquivos. A contagem de uso de arquivos permanecerão os mesmos e outros aplicativos que usam os arquivos da versão mais antigos agora usará a versão mais recente.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Instalando um tradutor|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
