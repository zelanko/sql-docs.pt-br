---
title: "Função SQLInstallDriverManager | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLInstallDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverManager
helpviewer_keywords:
- SQLInstallDriverManager function [ODBC]
ms.assetid: aebc439b-fffd-4d98-907a-0163f79aee8d
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6bc56b9045ae3f9a53b410ef0546d539e3c25ee8
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlinstalldrivermanager-function"></a>Função SQLInstallDriverManager
**Conformidade**  
 Versão apresentado: ODBC 1.0: preteridos no Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 e sistemas operacionais posteriores  
  
 **Resumo**  
 **SQLInstallDriverManager** retorna o caminho do diretório de destino para a instalação dos componentes centrais do ODBC. O programa de chamada, na verdade, deve copiar arquivos do Gerenciador de Driver para o diretório de destino.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszPath*  
 [Saída] Caminho do diretório de destino da instalação.  
  
 *cbPathMax*  
 [Entrada] Comprimento de *lpszPath*. Isso deve ser pelo menos bytes de MAX_PATH.  
  
 *pcbPathOut*  
 [Saída] Número total de bytes (excluindo o byte nulo de terminação) retornado em *lpszPath*. Se o número de bytes disponíveis para retornar é maior que ou igual a *cbPathMax*, o caminho no *lpszPath* será truncado para *cbPathMax* menos o encerramento nulo caractere. O *pcbPathOut* argumento pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLInstallDriverManager** retorna FALSE, um tipo de * \*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o * \*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O *lpszPath* argumento não era grande o suficiente para conter o caminho de saída. O buffer contém o caminho truncado.<br /><br /> O *cbPathMax* argumento era menor que MAX_PATH.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de uso do componente|Falha do instalador usado incrementar a contagem de uso de componente de núcleo do ODBC.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido a uma falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLInstallDriverManager** é chamado para retornar o caminho para os componentes principais do ODBC e o uso do componente de incremento contagem nas informações do sistema. Se já existe uma versão do Gerenciador de Driver, mas a contagem de uso do componente para o driver não existir, o novo valor de contagem de uso do componente é definido como 2.  
  
 O programa de instalação do aplicativo é responsável pela cópia fisicamente os arquivos de componente principal e contagens de manter o uso de arquivo. Se um arquivo de componente principal não tiver sido instalado anteriormente, o programa de instalação do aplicativo deve copiá-lo e criar a contagem de uso de arquivos. Se o arquivo tiver sido instalado anteriormente, o programa de instalação simplesmente incrementa a contagem de uso de arquivos.  
  
 Se uma versão mais antiga do Gerenciador de Driver foi instalada anteriormente pelo programa de instalação do aplicativo, os principais componentes devem ser desinstalados e reinstalados, para que a contagem de uso do componente principal é válida. **No SQLRemoveDriverManager** deve ser chamada primeiro para decrementar a contagem de uso do componente. **SQLInstallDriverManager** , em seguida, deve ser chamado para incrementar a contagem de uso do componente. O programa de instalação do aplicativo deve substituir os arquivos de componente principal antigo com os novos arquivos. As contagens de uso de arquivo permanece o mesmo, e outros aplicativos que são usados os arquivos de componente principal versão mais antigos usará os arquivos da versão mais recentes.  
  
 Em uma instalação nova de tradutores, os drivers e os componentes principais ODBC, o programa de instalação do aplicativo deve chamar as funções a seguir na sequência: **SQLInstallDriverManager**, **SQLInstallDriverEx**, **No SQLConfigDriver** (com um *frequentes* de ODBC_INSTALL_DRIVER) e, em seguida, **SQLInstallTranslatorEx**. Na desinstalação dos componentes principais, drivers e tradutores, o programa de instalação do aplicativo deve chamar as funções a seguir na sequência: **no SQLRemoveTranslator**, **no SQLRemoveDriver**e, em seguida, **No SQLRemoveDriverManager**. Essas funções devem ser chamadas nessa sequência. Em uma atualização de todos os componentes, todas as funções de desinstalação devem ser chamadas em sequência e, em seguida, todas as funções de instalação devem ser chamadas em sequência.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionar, modificar ou remover um driver|[No SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Instalar um driver|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|Instalando um conversor|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|Remoção de um driver|[No SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|Removendo o Gerenciador de Driver|[No SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|Removendo um conversor|[No SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
