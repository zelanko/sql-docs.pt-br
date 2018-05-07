---
title: Função no SQLRemoveDriverManager | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad7508ef6825bda50adee02fe92665e4d3445ee5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlremovedrivermanager-function"></a>Função no SQLRemoveDriverManager
**Conformidade**  
 Versão apresentado: ODBC 3.0: preteridos no Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 e sistemas operacionais posteriores.  
  
 **Resumo**  
 **No SQLRemoveDriverManager** altera ou remove informações sobre os principais componentes ODBC da entrada Odbcinst.ini nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pdwUsageCount*  
 [Saída] A contagem de uso do Gerenciador de Driver depois que essa função foi chamada.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar. Se não houver nenhuma entrada nas informações do sistema quando esta função é chamada, a função retornará FALSE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **no SQLRemoveDriverManager** retorna FALSE, um tipo de  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente não encontrado no registro|O instalador não foi possível remover as informações do Gerenciador de Driver porque ele não existe no registro ou não pôde ser encontrado no registro.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de uso do componente|Falha do instalador diminuir a contagem de uso do Gerenciador de Driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido a uma falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **No SQLRemoveDriverManager** complementa o **SQLInstallDriverManager** função e o uso do componente contagem nas informações do sistema de atualizações. Essa função deve ser chamada apenas de um aplicativo de instalação.  
  
 **No SQLRemoveDriverManager** irá diminuir a contagem de uso do componente principal por 1. Se a contagem de uso do componente chegar a 0, as informações do sistema de entrada serão removidas. A entrada de componente principal está no seguinte local nas informações do sistema, sob o título "Núcleo de ODBC":  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  Um aplicativo não deve fisicamente remover arquivos do Gerenciador de Driver quando a contagem de uso do componente e a contagem de uso de arquivo chegarem a zero.  
  
 **No SQLRemoveDriverManager** , na verdade, não remova os arquivos. O programa de chamada é responsável por excluir arquivos e contagens de manter o uso de arquivo. Arquivos do Gerenciador de driver não deve, no entanto, ser removido quando a contagem de uso do componente e a contagem de uso do arquivo atingiu zero, porque esses arquivos podem ser usados por outros aplicativos que não têm incrementado a contagem de uso de arquivos.  
  
 **No SQLRemoveDriverManager** é chamado como parte do processo de desinstalação. Componentes principais do ODBC (que incluem o Gerenciador de Driver, biblioteca de cursores, instalador, biblioteca de idioma, administrador, conversão de arquivos e assim por diante) são desinstalados como um todo. Os seguintes arquivos não são removidos quando **no SQLRemoveDriverManager** é chamado como parte do processo de desinstalação:  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32. DLL|  
|ODBCCR32. DLL|ODBC16GT. DLL|  
|ODBCCU32. DLL|ODBC32GT. DLL|  
|ODBCINT. DLL|DS16GT. DLL|  
|ODBCTRAC. DLL|DS32GT. DLL|  
|MSVCRT40. DLL|ODBCAD32. EXE|  
|ODBCCP32. PAINEL DE CONTROLE||  
  
 **No SQLRemoveDriverManager** também é chamado como parte de um processo de atualização. Se um aplicativo detectar que ele tem que executar uma atualização e tiver instalado anteriormente o driver, o driver deve ser removido e reinstalado.  
  
 **No SQLRemoveDriverManager** deve ser chamada primeiro para decrementar a contagem de uso do componente. **SQLInstallDriverEx** , em seguida, deve ser chamado para incrementar a contagem de uso do componente. O programa de instalação do aplicativo deve substituir os arquivos de componente principal antigo com os novos arquivos. As contagens de uso de arquivo permanece o mesmo, e outros aplicativos que usam os arquivos de componente principal versão mais antigos usará os arquivos da versão mais recentes.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Instalando o Gerenciador de Driver|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
