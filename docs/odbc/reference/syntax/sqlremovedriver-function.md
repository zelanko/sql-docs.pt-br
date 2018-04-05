---
title: Função no SQLRemoveDriver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5c910c862bd24a29ace17a2ec92352917d41699e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlremovedriver-function"></a>Função no SQLRemoveDriver
**Conformidade**  
 Versão introduzidas: ODBC 3.0  
  
 **Resumo**  
 **No SQLRemoveDriver** altera ou remove informações sobre o driver da entrada Odbcinst.ini nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDriver*  
 [Entrada] O nome do driver como registrado na chave Odbcinst.ini as informações do sistema.  
  
 *fRemoveDSN*  
 [Entrada] Os valores válidos são:  
  
 TRUE: Remover DSNs associados com o driver especificado na *lpszDriver*. FALSE: Não remova os DSNs associados com o driver especificado na *lpszDriver*.  
  
 *lpdwUsageCount*  
 [Saída] A contagem de uso do driver depois que essa função foi chamada.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar. Se não houver nenhuma entrada nas informações do sistema quando esta função é chamada, a função retornará FALSE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **no SQLRemoveDriver** retorna FALSE, um tipo de  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente não encontrado no registro|O instalador não foi possível remover as informações do driver porque ele não existe no registro ou não pôde ser encontrado no registro.|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou conversor inválido|O *lpszDriver* argumento era inválido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de uso do componente|Falha do instalador diminuir a contagem de uso do driver.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|O *fRemoveDSN* argumento era TRUE; no entanto, um ou mais DSNs não podem ser removidos. A chamada para **no SQLConfigDriver** com a solicitação ODBC_REMOVE_DRIVER falhou.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido a uma falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **No SQLRemoveDriver** complementa o [SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md) função e atualizações o uso do componente contagem nas informações do sistema. Essa função deve ser chamada apenas de um aplicativo de instalação.  
  
 **No SQLRemoveDriver** irá diminuir o valor de contagem de uso do componente por 1. Se a contagem de uso do componente chegar a 0, ocorrerá o seguinte:  
  
1.  O **no SQLConfigDriver** função com a opção ODBC_REMOVE_DRIVER será chamada. Se o *fRemoveDSN* opção é definida como TRUE, o **ConfigDSN** chamadas de função **SQLRemoveDSNFromIni** para remover todas as fontes de dados associadas com o driver especificado em *lpszDriver.* Se o *fRemoveDSN* opção é definida como FALSE, as fontes de dados não serão excluídas.  
  
2.  A entrada de driver nas informações do sistema será removida. A entrada de driver está no seguinte sistema informações local, sob o nome do driver:  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **No SQLRemoveDriver** , na verdade, não remova os arquivos. O programa de chamada é responsável por excluir arquivos e manter a contagem de uso de arquivos. Somente quando a contagem de uso do componente e a contagem de uso do arquivo atingido zero é um arquivo excluído fisicamente. Alguns arquivos em um componente podem ser excluídos e outros não excluído, dependendo se os arquivos são usados por outros aplicativos que têm incrementado a contagem de uso de arquivos.  
  
 **No SQLRemoveDriver** também é chamado como parte de um processo de atualização. Se um aplicativo detectar que ele tem que executar uma atualização e tiver instalado anteriormente o driver, o driver deve ser removido e reinstalado. **No SQLRemoveDriver** primeiro deve ser chamado para diminuir a contagem de uso do componente e, em seguida, **SQLInstallDriverEx** deve ser chamado para incrementar a contagem de uso do componente. O programa de instalação do aplicativo deve substituir os arquivos antigos com os novos arquivos. A contagem de uso de arquivo permanece o mesmo, e outros aplicativos que usam os arquivos da versão mais antigos agora usará a versão mais recente.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionar, modificar ou remover um driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) (na configuração de DLL)|  
|Adicionar, modificar ou remover um driver|[No SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Instalar um driver|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
