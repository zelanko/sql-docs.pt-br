---
title: Função SQLRemoveDriver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriver
helpviewer_keywords:
- SQLRemoveDriver function [ODBC]
ms.assetid: 9a3b4f8b-982b-44b9-ade6-754ff026dc90
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 274451cdd2d1c3d811e4105a6d646044537999f1
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537370"
---
# <a name="sqlremovedriver-function"></a>Função SQLRemoveDriver
**Conformidade com**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLRemoveDriver** altera ou remove informações sobre o driver da entrada Odbcinst. ini nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDriver*  
 [Entrada] O nome do driver como registrado na chave do Odbcinst. ini, as informações do sistema.  
  
 *fRemoveDSN*  
 [Entrada] Os valores válidos são:  
  
 TRUE: Remover DSNs associados com o driver especificado na *lpszDriver*. FALSE: Não remova os DSNs associados com o driver especificado na *lpszDriver*.  
  
 *lpdwUsageCount*  
 [Saída] A contagem de utilização do driver depois que essa função foi chamada.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar. Se não houver nenhuma entrada nas informações do sistema quando essa função é chamada, a função retorna FALSE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLRemoveDriver** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Não foi encontrado no registro do componente|O instalador não foi possível remover as informações do driver porque ele não existe no registro ou não pôde ser encontrado no registro.|  
|ODBC_ERROR_INVALID_NAME|Nome inválido de driver ou conversor|O *lpszDriver* argumento era inválido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de utilização de componente|O instalador não conseguiu reduzir a contagem de uso do driver.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|O *fRemoveDSN* argumento era TRUE; no entanto, os DSNs de um ou mais não pôde ser removidos. A chamada para **SQLConfigDriver** com a solicitação ODBC_REMOVE_DRIVER falhou.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLRemoveDriver** complementa os [SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md) função e as atualizações o uso do componente contagem nas informações do sistema. Essa função deve ser chamada apenas de um aplicativo de instalação.  
  
 **SQLRemoveDriver** diminuirá o valor de contagem de uso do componente em 1. Se a contagem de uso do componente chegar a 0, ocorrerá o seguinte:  
  
1.  O **SQLConfigDriver** função com a opção ODBC_REMOVE_DRIVER será chamada. Se o *fRemoveDSN* opção for definida como TRUE, o **ConfigDSN** chamadas de função **SQLRemoveDSNFromIni** para remover todas as fontes de dados associadas com o driver especificado em *lpszDriver.* Se o *fRemoveDSN* opção é definida como FALSE, as fontes de dados não serão excluídas.  
  
2.  A entrada de driver nas informações do sistema será removida. A entrada driver é no seguinte sistema informações local, sob o nome do driver:  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver** não remover todos os arquivos. O programa de chamada é responsável pela exclusão de arquivos e manter a contagem de uso de arquivos. Somente depois que a contagem de uso do componente e a contagem de uso de arquivos atingiu o zero é um arquivo excluído fisicamente. Alguns arquivos em um componente podem ser excluídos, e outras pessoas não excluído, dependendo se os arquivos são usados por outros aplicativos que têm aumentado a contagem de uso de arquivos.  
  
 **SQLRemoveDriver** também é chamado como parte de um processo de atualização. Se um aplicativo detectar que ele deve realizar uma atualização e ele foi instalado anteriormente o driver, o driver deve ser removido e reinstalado. **SQLRemoveDriver** deve ser chamada primeiro para diminuir a contagem de uso do componente e então **SQLInstallDriverEx** deve ser chamado para incrementar a contagem de uso do componente. O programa de instalação do aplicativo deve substituir os arquivos antigos com os novos arquivos. A contagem de uso de arquivos permanecerão os mesmos e outros aplicativos que usam os arquivos da versão mais antigos agora usará a versão mais recente.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionar, modificar ou remover um driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) (na configuração de DLL)|  
|Adicionar, modificar ou remover um driver|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Instalar um driver|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
