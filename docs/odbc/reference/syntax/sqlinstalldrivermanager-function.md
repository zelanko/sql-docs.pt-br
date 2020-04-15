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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0788de0493439a360c0446733b31606a02e12422
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302107"
---
# <a name="sqlinstalldrivermanager-function"></a>Função SQLInstallDriverManager
**Conformidade**  
 Versão introduzida: ODBC 1.0: Preterido no Windows XP Service Pack 2, No Windows Server 2003 Service Pack 1 e posteriormente nos sistemas operacionais  
  
 **Resumo**  
 **SQLInstallDriverManager** retorna o caminho do diretório de destino para a instalação dos componentes principais do ODBC. O programa de chamada deve, na verdade, copiar os arquivos do Driver Manager para o diretório de destino.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszPath*  
 [Saída] Caminho do diretório de destino da instalação.  
  
 *cbPathMax*  
 [Entrada] Comprimento de *lpszPath*. Isso deve ser pelo menos _MAX_PATH bytes.  
  
 *pcbpathOut*  
 [Saída] Número total de bytes (excluindo o byte de rescisão nula) retornado em *lpszPath*. Se o número de bytes disponíveis para retornar for maior ou igual ao *cbPathMax,* o caminho no *lpszPath* será truncado para *cbPathMax* menos o caractere de rescisão nula. O *argumento pcbPathOut* pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLInstallDriverManager** retorna FALSO, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O argumento *lpszPath* não era grande o suficiente para conter o caminho de saída. O buffer contém o caminho truncado.<br /><br /> O *argumento cbPathMax* foi menos de _MAX_PATH.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou diminuir a contagem de uso de componentes|O instalador não conseguiu incrementar a contagem de uso do componente principal ODBC.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **O SQLInstallDriverManager** é chamado para retornar o caminho para os componentes principais do ODBC e incrementar a contagem de uso de componentes nas informações do sistema. Se uma versão do Driver Manager já existir, mas a contagem de uso do componente para o driver não existir, o novo valor de contagem de uso do componente será definido como 2.  
  
 O programa de configuração do aplicativo é responsável por copiar fisicamente os arquivos do componente principal e manter as contagens de uso do arquivo. Se um arquivo de componente principal não tiver sido instalado anteriormente, o programa de configuração do aplicativo deve copiar o arquivo e criar a contagem de uso do arquivo. Se o arquivo tiver sido instalado anteriormente, o programa de configuração apenas incrementa a contagem de uso do arquivo.  
  
 Se uma versão mais antiga do Driver Manager foi previamente instalada pelo programa de configuração do aplicativo, os componentes principais devem ser desinstalados e depois reinstalados, de modo que a contagem de uso do componente principal seja válida. **SQLRemoveDriverManager** deve ser chamado primeiro para diminuir a contagem de uso do componente. **SQLInstallDriverManager** deve então ser chamado para incrementar a contagem de uso do componente. O programa de configuração do aplicativo deve substituir os arquivos de componentes antigos por novos arquivos. As contagens de uso de arquivos permanecerão as mesmas, e outros aplicativos que usaram os arquivos de componentes da versão mais antiga agora usarão os arquivos de versão mais recente.  
  
 Em uma nova instalação dos componentes principais do ODBC, drivers e tradutores, o programa de configuração do aplicativo deve chamar as seguintes funções em seqüência: **SQLInstallDriverManager,** **SQLInstallDriverEx,** **SQLConfigDriver** (com um *fRequest* of ODBC_INSTALL_DRIVER) e, em seguida, **SQLInstallTranslatorEx**. Em uma desinstalação dos componentes principais, drivers e tradutores, o programa de configuração do aplicativo deve chamar as seguintes funções em seqüência: **SQLRemoveTranslator,** **SQLRemoveDriver**e, em seguida, **SQLRemoveDriverManager**. Essas funções devem ser chamadas nesta seqüência. Em uma atualização de todos os componentes, todas as funções de desinstalação devem ser chamadas em seqüência e, em seguida, todas as funções de instalação devem ser chamadas em seqüência.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo um driver|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Instalando um driver|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|Instalando um tradutor|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|Removendo um driver|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|Removendo o Driver Manager|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|Removendo um tradutor|[SQLRemoveTradutor](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
