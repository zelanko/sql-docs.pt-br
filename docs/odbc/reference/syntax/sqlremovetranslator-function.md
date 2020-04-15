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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 348d2c5da0731ba88ccd4dd6406d3754890f7906
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301783"
---
# <a name="sqlremovetranslator-function"></a>Função SQLRemoveTranslator
**Conformidade**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLRemoveTranslator** remove informações sobre um tradutor da seção Odbcinst.ini das informações do sistema e diminui a contagem de uso de componentes do tradutor por 1.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszTradutor*  
 [Entrada] O nome do tradutor registrado na chave Odbcinst.ini das informações do sistema.  
  
 *lpdwUsagecount*  
 [Saída] A contagem de uso do tradutor após esta função foi chamada.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar. Se não houver entrada nas informações do sistema quando essa função for chamada, a função retorna FALSA.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **sqlRemoveTranslator** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente não encontrado no registro|O instalador não pôde remover as informações do tradutor porque ou ela não existia no registro ou não podia ser encontrada no registro.|  
|ODBC_ERROR_INVALID_NAME|Nome de motorista ou tradutor inválido|O *argumento lpszTranslator* era inválido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou diminuir a contagem de uso de componentes|O instalador não conseguiu diminuir a contagem de uso do driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLRemoveTranslator** complementa a função [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) e atualiza a contagem de uso de componentes nas informações do sistema. Esta função deve ser chamada apenas a partir de um aplicativo de configuração.  
  
 **SQLRemoveTranslator** diminuirá a contagem de uso do componente em 1. Se a contagem de uso do componente for para 0, a entrada do tradutor nas informações do sistema será removida. A entrada do tradutor está no seguinte local nas informações do sistema, sob o nome do tradutor:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator** não remove nenhum arquivo. O programa de chamada é responsável por excluir arquivos e manter a contagem de uso de arquivos. Somente depois que a contagem de uso do componente e a contagem de uso do arquivo atingirem zero é que um arquivo fisicamente excluído. Alguns arquivos em um componente podem ser excluídos, e outros não excluídos, dependendo se os arquivos são usados por outros aplicativos que aumentaram a contagem de uso do arquivo.  
  
 **SQLRemoveTranslator** também é chamado como parte de um processo de atualização. Se um aplicativo detectar que tem que realizar uma atualização e já instalou o driver, o driver deve ser removido e, em seguida, reinstalado. **SQLRemoveTranslator** deve primeiro ser chamado para diminuir a contagem de uso do componente e, em seguida, **sQLInstallTranslatorEx** deve ser chamado para incrementar a contagem de uso do componente. O programa de configuração do aplicativo deve substituir fisicamente os arquivos antigos pelos novos arquivos. A contagem de uso do arquivo permanecerá a mesma, e outros aplicativos que usam os arquivos de versão mais antigo agora usarão a versão mais recente.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Instalando um tradutor|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
