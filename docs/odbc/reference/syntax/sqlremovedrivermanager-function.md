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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5cd31a45ed891a8dc95f4f23981d4b626a6095b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024543"
---
# <a name="sqlremovedrivermanager-function"></a>Função SQLRemoveDriverManager
**Conformidade com**  
 Versão introduzida: ODBC 3.0: Preterido no Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 e sistemas operacionais posteriores.  
  
 **Resumo**  
 **SQLRemoveDriverManager** altera ou remove informações sobre os principais componentes ODBC da entrada Odbcinst. ini nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pdwUsageCount*  
 [Saída] A contagem de utilização do Gerenciador de Driver depois que essa função foi chamada.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar. Se não houver nenhuma entrada nas informações do sistema quando essa função é chamada, a função retorna FALSE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLRemoveDriverManager** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Não foi encontrado no registro do componente|O instalador não foi possível remover as informações do Gerenciador de Driver porque ele não existe no registro ou não pôde ser encontrado no registro.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de utilização de componente|O instalador não conseguiu reduzir a contagem de uso do Gerenciador de Driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLRemoveDriverManager** complementa os **SQLInstallDriverManager** função e o uso do componente contagem nas informações do sistema de atualizações. Essa função deve ser chamada apenas de um aplicativo de instalação.  
  
 **SQLRemoveDriverManager** diminuirá a contagem de uso do componente core 1. Se a contagem de uso do componente chegar a 0, as informações do sistema de entrada serão removidas. A entrada de componente principal está no seguinte local nas informações do sistema, sob o título "Principal" ODBC":  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  Um aplicativo não deve fisicamente remover arquivos do Gerenciador de Driver quando a contagem de uso do componente e a contagem de utilização do arquivo atingir zero.  
  
 **SQLRemoveDriverManager** não remover todos os arquivos. O programa de chamada é responsável pela exclusão de arquivos e contagens de manter o uso de arquivos. Arquivos do Gerenciador de driver não deveria, no entanto, ser removido quando a contagem de uso do componente e a contagem de uso de arquivos têm chegou a zero, porque esses arquivos podem ser usados por outros aplicativos que não têm aumentado a contagem de uso de arquivos.  
  
 **SQLRemoveDriverManager** é chamado como parte do processo de desinstalação. Principais componentes ODBC (que incluem o Gerenciador de Driver, biblioteca de cursores, instalador, biblioteca de linguagem, administrador, conversão de arquivos e assim por diante) são desinstalados como um todo. Os seguintes arquivos não são removidos quando **SQLRemoveDriverManager** é chamado como parte do processo de desinstalação:  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32.DLL|  
|ODBCCR32.DLL|ODBC16GT.DLL|  
|ODBCCU32.DLL|ODBC32GT.DLL|  
|ODBCINT. DLL|DS16GT.DLL|  
|ODBCTRAC. DLL|DS32GT.DLL|  
|MSVCRT40.DLL|ODBCAD32.EXE|  
|ODBCCP32.CPL||  
  
 **SQLRemoveDriverManager** também é chamado como parte de um processo de atualização. Se um aplicativo detectar que ele deve realizar uma atualização e ele foi instalado anteriormente o driver, o driver deve ser removido e reinstalado.  
  
 **SQLRemoveDriverManager** primeiro deve ser chamado para diminuir a contagem de uso do componente. **SQLInstallDriverEx** , em seguida, deve ser chamado para incrementar a contagem de uso do componente. O programa de instalação do aplicativo deve substituir os arquivos de componente principal antigo com os novos arquivos. As contagens de uso de arquivos permanecerão os mesmos e outros aplicativos que usam os arquivos de componente de núcleo de versão mais antigos agora usará os arquivos da versão mais recentes.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Instalando um Gerenciador de Driver|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
