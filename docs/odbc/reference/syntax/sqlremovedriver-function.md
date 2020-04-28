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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 205c5b46e5f6cea195094f7a50e81d7509927d1a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303927"
---
# <a name="sqlremovedriver-function"></a>Função SQLRemoveDriver
**Conformidade**  
 Versão introduzida: ODBC 3,0  
  
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
 Entrada O nome do driver, conforme registrado na chave Odbcinst. ini das informações do sistema.  
  
 *fRemoveDSN*  
 Entrada Os valores válidos são:  
  
 TRUE: Remova os DSNs associados ao driver especificado em *lpszDriver*. FALSE: não remova os DSNs associados ao driver especificado em *lpszDriver*.  
  
 *lpdwUsageCount*  
 Der A contagem de uso do driver depois que essa função foi chamada.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar. Se não existir nenhuma entrada nas informações do sistema quando essa função for chamada, a função retornará FALSE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLRemoveDriver** retorna false, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente não encontrado no registro|O instalador não pôde remover as informações do driver porque ele não existia no registro ou não foi encontrado no registro.|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou tradutor inválido|O argumento *lpszDriver* era inválido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de uso do componente|O instalador não pôde decrementar a contagem de uso do driver.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|O argumento *fRemoveDSN* era true; no entanto, um ou mais DSNs não puderam ser removidos. Falha na chamada para **SQLConfigDriver** com a solicitação de ODBC_REMOVE_DRIVER.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLRemoveDriver** complementa a função [SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md) e atualiza a contagem de uso do componente nas informações do sistema. Essa função deve ser chamada somente de um aplicativo de instalação.  
  
 **SQLRemoveDriver** reduzirá o valor de contagem de uso do componente em 1. Se a contagem de uso do componente for para 0, ocorrerá o seguinte:  
  
1.  A função **SQLConfigDriver** com a opção ODBC_REMOVE_DRIVER será chamada. Se a opção *fRemoveDSN* for definida como true, a função **ConfigDSN** chamará **SQLRemoveDSNFromIni** para remover todas as fontes de dados associadas ao driver especificado em *lpszDriver.* Se a opção *fRemoveDSN* for definida como false, as fontes de dados não serão excluídas.  
  
2.  A entrada de driver nas informações do sistema será removida. A entrada do driver está no seguinte local de informações do sistema, sob o nome do driver:  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 Na verdade, o **SQLRemoveDriver** não remove nenhum arquivo. O programa de chamada é responsável por excluir arquivos e manter a contagem de uso do arquivo. Somente após a contagem de uso do componente e a contagem de uso do arquivo ter atingido zero é um arquivo excluído fisicamente. Alguns arquivos em um componente podem ser excluídos e outros não excluídos, dependendo se os arquivos são usados por outros aplicativos que incrementaram a contagem de uso do arquivo.  
  
 **SQLRemoveDriver** também é chamado como parte de um processo de atualização. Se um aplicativo detectar que deve executar uma atualização e tiver instalado anteriormente o driver, o driver deverá ser removido e reinstalado. **SQLRemoveDriver** deve ser chamado primeiro para decrementar a contagem de uso do componente e, em seguida, **SQLInstallDriverEx** deve ser chamado para incrementar a contagem de uso do componente. O programa de instalação do aplicativo deve substituir os arquivos antigos pelos novos arquivos. A contagem de uso do arquivo permanecerá a mesma, e outros aplicativos que usam os arquivos de versão mais antigos agora usarão a versão mais recente.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo um driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) (na DLL de instalação)|  
|Adicionando, modificando ou removendo um driver|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Instalando um driver|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
