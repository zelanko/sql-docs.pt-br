---
title: Função SQLRemoveDriverManager | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriverManager
helpviewer_keywords:
- SQLRemoveDriverManager function function [ODBC]
ms.assetid: 3a41511f-6603-4b81-a815-7883874023c4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 27b32c1c4e0f3f4d5359af287ba07d40b033af00
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301807"
---
# <a name="sqlremovedrivermanager-function"></a>Função SQLRemoveDriverManager
**Conformidade**  
 Versão introduzida: ODBC 3,0: preterido no Windows XP Service Pack 2, no Windows Server 2003 Service Pack 1 e em sistemas operacionais posteriores.  
  
 **Resumo**  
 **SQLRemoveDriverManager** altera ou remove informações sobre os componentes principais do ODBC da entrada Odbcinst. ini nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pdwUsageCount*  
 Der A contagem de uso do Gerenciador de driver depois que essa função foi chamada.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar. Se não existir nenhuma entrada nas informações do sistema quando essa função for chamada, a função retornará FALSE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLRemoveDriverManager** retorna false, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente não encontrado no registro|O instalador não pôde remover as informações do Gerenciador de driver porque ele não existia no registro ou não foi encontrado no registro.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de uso do componente|O instalador não pôde decrementar a contagem de uso do Gerenciador de driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 O **SQLRemoveDriverManager** complementa a função **SQLInstallDriverManager** e atualiza a contagem de uso do componente nas informações do sistema. Essa função deve ser chamada somente de um aplicativo de instalação.  
  
 **SQLRemoveDriverManager** reduzirá a contagem de uso do componente principal em 1. Se a contagem de uso do componente for para 0, as informações do sistema de entrada serão removidas. A entrada do componente principal está no seguinte local nas informações do sistema, sob o título "ODBC Core":  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  Um aplicativo não deve remover fisicamente os arquivos do Gerenciador de driver quando a contagem de uso do componente e a contagem de uso do arquivo atingem zero.  
  
 Na verdade, o **SQLRemoveDriverManager** não remove nenhum arquivo. O programa de chamada é responsável por excluir arquivos e manter as contagens de uso do arquivo. No entanto, os arquivos do Gerenciador de driver não devem ser removidos quando a contagem de uso do componente e a contagem de uso do arquivo tiverem atingido zero, pois esses arquivos podem ser usados por outros aplicativos que não incrementaram a contagem de uso do arquivo.  
  
 **SQLRemoveDriverManager** é chamado como parte do processo de desinstalação. Os componentes principais do ODBC (que incluem o Gerenciador de driver, a biblioteca de cursores, o instalador, a biblioteca de idiomas, o administrador, os arquivos de conversão e assim por diante) são desinstalados como um todo. Os seguintes arquivos não são removidos quando **SQLRemoveDriverManager** é chamado como parte do processo de desinstalação:  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32. DLL|  
|ODBCCR32. DLL|ODBC16GT. DLL|  
|ODBCCU32. DLL|ODBC32GT. DLL|  
|ODBCINT. DLL|DS16GT. DLL|  
|ODBCTRAC. DLL|DS32GT. DLL|  
|MSVCRT40. DLL|ODBCAD32. EXE|  
|ODBCCP32. PAINEL||  
  
 **SQLRemoveDriverManager** também é chamado como parte de um processo de atualização. Se um aplicativo detectar que deve executar uma atualização e tiver instalado anteriormente o driver, o driver deverá ser removido e reinstalado.  
  
 **SQLRemoveDriverManager** deve primeiro ser chamado para decrementar a contagem de uso do componente. **SQLInstallDriverEx** deve ser chamado para incrementar a contagem de uso do componente. O programa de instalação do aplicativo deve substituir os arquivos do componente principal antigo pelos novos arquivos. As contagens de uso de arquivo permanecerão as mesmas, e outros aplicativos que usam os arquivos de componentes principais de versão mais antiga agora usarão os arquivos de versão mais recentes.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Instalando um Gerenciador de driver|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
