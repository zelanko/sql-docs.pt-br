---
title: Função SQLInstallDriverManager | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f1e3ac7f0a76c607fa07d6eb92d069d99ef5e0a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076207"
---
# <a name="sqlinstalldrivermanager-function"></a>Função SQLInstallDriverManager
**Conformidade**  
 Versão introduzida: ODBC 1,0: preterido no Windows XP Service Pack 2, no Windows Server 2003 Service Pack 1 e em sistemas operacionais posteriores  
  
 **Resumo**  
 **SQLInstallDriverManager** retorna o caminho do diretório de destino para a instalação dos componentes principais do ODBC. O programa de chamada deve realmente copiar os arquivos do Gerenciador de driver para o diretório de destino.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszPath*  
 Der Caminho do diretório de destino da instalação.  
  
 *cbPathMax*  
 Entrada Comprimento de *lpszPath*. Deve ter pelo menos _MAX_PATH bytes.  
  
 *pcbPathOut*  
 Der Número total de bytes (excluindo o byte de terminação nula) retornado em *lpszPath*. Se o número de bytes disponíveis para retornar for maior ou igual a *cbPathMax*, o caminho em *lpszPath* será truncado para *cbPathMax* menos o caractere de terminação nula. O argumento *pcbPathOut* pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLInstallDriverManager** retorna false, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|DESCRIÇÃO|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O argumento *lpszPath* não era grande o suficiente para conter o caminho de saída. O buffer contém o caminho truncado.<br /><br /> O argumento *cbPathMax* era menor que _MAX_PATH.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de uso do componente|O instalador não pôde incrementar a contagem de uso do componente principal ODBC.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLInstallDriverManager** é chamado para retornar o caminho para componentes principais do ODBC e incrementar a contagem de uso do componente nas informações do sistema. Se já existir uma versão do Gerenciador de driver, mas a contagem de uso de componentes para o driver não existir, o novo valor de contagem de uso do componente será definido como 2.  
  
 O programa de instalação do aplicativo é responsável por copiar fisicamente os arquivos do componente principal e manter as contagens de uso do arquivo. Se um arquivo de componente principal não tiver sido instalado anteriormente, o programa de instalação do aplicativo deverá copiar o arquivo e criar a contagem de uso do arquivo. Se o arquivo tiver sido instalado anteriormente, o programa de instalação simplesmente incrementará a contagem de uso do arquivo.  
  
 Se uma versão mais antiga do Gerenciador de driver foi instalada anteriormente pelo programa de instalação do aplicativo, os componentes principais devem ser desinstalados e reinstalados, para que a contagem de uso do componente principal seja válida. **SQLRemoveDriverManager** deve primeiro ser chamado para decrementar a contagem de uso do componente. **SQLInstallDriverManager** deve ser chamado para incrementar a contagem de uso do componente. O programa de instalação do aplicativo deve substituir os arquivos do componente principal antigo pelos novos arquivos. As contagens de uso do arquivo permanecerão as mesmas, e outros aplicativos que usaram os arquivos do componente principal da versão mais antiga agora usarão os arquivos de versão mais recentes.  
  
 Em uma nova instalação dos componentes, drivers e tradutores do ODBC Core, o programa de instalação do aplicativo deve chamar as seguintes funções em Sequence: **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLConfigDriver** (com um *fRequest* de ODBC_INSTALL_DRIVER) e, em seguida, **SQLInstallTranslatorEx**. Em uma desinstalação dos componentes principais, dos drivers e dos tradutores, o programa de instalação do aplicativo deve chamar as seguintes funções em sequência: **SQLRemoveTranslator**, **SQLRemoveDriver**e, em seguida, **SQLRemoveDriverManager**. Essas funções devem ser chamadas nesta sequência. Em uma atualização de todos os componentes do, todas as funções de desinstalação devem ser chamadas em sequência e, em seguida, todas as funções de instalação devem ser chamadas em sequência.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo um driver|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Instalando um driver|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|Instalando um tradutor|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|Removendo um driver|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|Removendo o Gerenciador de driver|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|Removendo um tradutor|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
