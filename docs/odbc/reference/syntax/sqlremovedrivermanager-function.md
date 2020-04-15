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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301807"
---
# <a name="sqlremovedrivermanager-function"></a>Função SQLRemoveDriverManager
**Conformidade**  
 Versão introduzida: ODBC 3.0: Depreciado no Windows XP Service Pack 2, No Windows Server 2003 Service Pack 1 e posteriormente nos sistemas operacionais.  
  
 **Resumo**  
 **SQLRemoveDriverManager** altera ou remove informações sobre os componentes principais do ODBC da entrada Odbcinst.ini nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pdwUsageCount*  
 [Saída] A contagem de uso do Driver Manager após esta função foi chamada.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar. Se não houver entrada nas informações do sistema quando essa função for chamada, a função retorna FALSA.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLRemoveDriverManager** retorna FALSO, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente não encontrado no registro|O instalador não pôde remover as informações do Driver Manager porque ou ela não existia no registro ou não podia ser encontrada no registro.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou diminuir a contagem de uso de componentes|O instalador não conseguiu diminuir a contagem de uso do Driver Manager.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **O SQLRemoveDriverManager** complementa a função **SQLInstallDriverManager** e atualiza a contagem de uso de componentes nas informações do sistema. Esta função deve ser chamada apenas a partir de um aplicativo de configuração.  
  
 **SQLRemoveDriverManager** diminuirá a contagem de uso do componente principal em 1. Se a contagem de uso do componente for para 0, as informações do sistema de entrada serão removidas. A entrada do componente principal está no seguinte local nas informações do sistema, sob o título "Núcleo ODBC":  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  Um aplicativo não deve remover fisicamente arquivos do Driver Manager quando a contagem de uso do componente e a contagem de uso do arquivo atingirem zero.  
  
 **SQLRemoveDriverManager** não remove nenhum arquivo. O programa de chamada é responsável por excluir arquivos e manter as contagens de uso de arquivos. Os arquivos do Driver Manager não devem, no entanto, ser removidos quando a contagem de uso do componente e a contagem de uso do arquivo atingirem zero, porque esses arquivos podem ser usados por outros aplicativos que não tenham incrementado a contagem de uso do arquivo.  
  
 **SQLRemoveDriverManager** é chamado como parte do processo Desinstalar. Os componentes principais do ODBC (que incluem o Driver Manager, A Biblioteca do Cursor, instalador, biblioteca de idiomas, administrador, arquivos de thunking e assim por diante) são desinstalados como um todo. Os seguintes arquivos não são removidos quando **o SQLRemoveDriverManager** é chamado como parte do processo Desinstalar:  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32. Dll|  
|ODBCCR32. Dll|ODBC16GT. Dll|  
|ODBCCU32. Dll|ODBC32GT. Dll|  
|ODBCINT. Dll|DS16GT. Dll|  
|ODBCTRAC. Dll|DS32GT. Dll|  
|MSVCRT40. Dll|ODBCAD32. Exe|  
|ODBCCP32. Cpl||  
  
 **SQLRemoveDriverManager** também é chamado como parte de um processo de atualização. Se um aplicativo detectar que tem que realizar uma atualização e já instalou o driver, o driver deve ser removido e, em seguida, reinstalado.  
  
 **SQLRemoveDriverManager** deve ser chamado primeiro para diminuir a contagem de uso do componente. **SQLInstallDriverEx** deve então ser chamado para incrementar a contagem de uso do componente. O programa de configuração do aplicativo deve substituir os arquivos de componentes antigos por novos arquivos. As contagens de uso de arquivos permanecerão as mesmas, e outros aplicativos que usam os arquivos de componentes da versão mais antiga agora usarão os arquivos de versão mais recente.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Instalando um driver manager|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
