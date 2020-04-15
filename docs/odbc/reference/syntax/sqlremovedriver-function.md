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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303927"
---
# <a name="sqlremovedriver-function"></a>Função SQLRemoveDriver
**Conformidade**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLRemoveDriver** altera ou remove informações sobre o driver a partir da entrada Odbcinst.ini nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Lpszdriver*  
 [Entrada] O nome do motorista registrado na chave Odbcinst.ini das informações do sistema.  
  
 *fRemoveDSN*  
 [Entrada] Os valores válidos são:  
  
 TRUE: Remova DSNs associados ao driver especificado no *lpszDriver*. FALSO: Não remova DSNs associados ao driver especificado no *lpszDriver*.  
  
 *lpdwUsagecount*  
 [Saída] A contagem de uso do driver após esta função foi chamada.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar. Se não houver entrada nas informações do sistema quando essa função for chamada, a função retorna FALSA.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **sQLRemoveDriver** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente não encontrado no registro|O instalador não pôde remover as informações do driver porque ou não existia no registro ou não podia ser encontrado no registro.|  
|ODBC_ERROR_INVALID_NAME|Nome de motorista ou tradutor inválido|O argumento *lpszDriver* era inválido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou diminuir a contagem de uso de componentes|O instalador não conseguiu diminuir a contagem de uso do driver.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|O argumento *fRemoveDSN* era VERDADEIRO; no entanto, um ou mais DSNs não puderam ser removidos. A chamada para **SQLConfigDriver** com a solicitação ODBC_REMOVE_DRIVER falhou.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLRemoveDriver** complementa a função [SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md) e atualiza a contagem de uso de componentes nas informações do sistema. Esta função deve ser chamada apenas a partir de um aplicativo de configuração.  
  
 **SQLRemoveDriver** diminuirá o valor da contagem de uso do componente em 1. Se a contagem de uso do componente for para 0, ocorrerão as seguintes:  
  
1.  A função **SQLConfigDriver** com a opção ODBC_REMOVE_DRIVER será chamada. Se a opção *fRemoveDSN* estiver definida como TRUE, a função **ConfigDSN** chamará **SQLRemoveDSNFromIni** para remover todas as fontes de dados associadas ao driver especificado no *lpszDriver.* Se a opção *fRemoveDSN* estiver definida como FALSE, as fontes de dados não serão excluídas.  
  
2.  A entrada do driver nas informações do sistema será removida. A entrada do driver está no seguinte local de informações do sistema, sob o nome do driver:  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver** não remove nenhum arquivo. O programa de chamada é responsável por excluir arquivos e manter a contagem de uso do arquivo. Somente depois que a contagem de uso do componente e a contagem de uso do arquivo atingirem zero é que um arquivo fisicamente excluído. Alguns arquivos em um componente podem ser excluídos, e outros não excluídos, dependendo se os arquivos são usados por outros aplicativos que aumentaram a contagem de uso do arquivo.  
  
 **SQLRemoveDriver** também é chamado como parte de um processo de atualização. Se um aplicativo detectar que tem que realizar uma atualização e já instalou o driver, o driver deve ser removido e, em seguida, reinstalado. **SQLRemoveDriver** deve primeiro ser chamado para diminuir a contagem de uso do componente e, em seguida, **sQLInstallDriverEx** deve ser chamado para incrementar a contagem de uso do componente. O programa de configuração do aplicativo deve substituir os arquivos antigos pelos novos arquivos. A contagem de uso do arquivo permanecerá a mesma, e outros aplicativos que usam os arquivos de versão mais antigo agora usarão a versão mais recente.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo um driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) (na DLL de configuração)|  
|Adicionando, modificando ou removendo um driver|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Instalando um driver|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
