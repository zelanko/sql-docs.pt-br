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
manager: craigg
ms.openlocfilehash: 47069f1003b9b3f9bddb1e8601b3b4284372ae7e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63132688"
---
# <a name="sqlinstalldrivermanager-function"></a>Função SQLInstallDriverManager
**Conformidade com**  
 Versão introduzida: ODBC 1.0: Preterido no Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 e sistemas operacionais posteriores  
  
 **Resumo**  
 **SQLInstallDriverManager** retorna o caminho do diretório de destino para a instalação dos componentes principais ODBC. O programa de chamada, na verdade, deve copiar arquivos do Gerenciador de Driver para o diretório de destino.  
  
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
 [Entrada] Comprimento da *lpszPath*. Isso deve ser pelo menos bytes MAX_PATH.  
  
 *pcbPathOut*  
 [Saída] Número total de bytes (excluindo o byte nulo de terminação) retornado em *lpszPath*. Se o número de bytes disponíveis para retornar for maior que ou igual a *cbPathMax*, o caminho na *lpszPath* será truncado com *cbPathMax* menos a terminação null caractere. O *pcbPathOut* argumento pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLInstallDriverManager** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O *lpszPath* argumento não era grande o suficiente para conter o caminho de saída. O buffer contém o caminho truncado.<br /><br /> O *cbPathMax* argumento era menor que MAX_PATH.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de utilização de componente|O instalador não conseguiu incrementar a contagem de utilização de componente de núcleo ODBC.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLInstallDriverManager** é chamado para retornar o caminho para os principais componentes ODBC e o uso do componente de incremento são contadas nas informações do sistema. Se já houver uma versão do Gerenciador de Driver, mas a contagem de utilização de componente para o driver não existir, o novo valor de contagem de uso do componente é definido como 2.  
  
 O programa de instalação do aplicativo é responsável pela cópia fisicamente os arquivos de componente principais e contagens de manter o uso de arquivos. Se um arquivo de componente de núcleo não tiver sido instalado anteriormente, o programa de instalação do aplicativo deve copiar o arquivo e crie a contagem de uso de arquivos. Se o arquivo tiver sido instalado anteriormente, o programa de instalação simplesmente incrementa a contagem de uso de arquivos.  
  
 Se uma versão mais antiga do Gerenciador de Driver já foi instalada pelo programa de instalação do aplicativo, os principais componentes devem ser desinstalados e reinstalados, para que a contagem de utilização de componente principal é válida. **SQLRemoveDriverManager** primeiro deve ser chamado para diminuir a contagem de uso do componente. **SQLInstallDriverManager** , em seguida, deve ser chamado para incrementar a contagem de uso do componente. O programa de instalação do aplicativo deve substituir os arquivos de componente principal antigo com os novos arquivos. As contagens de uso de arquivos permanecerão os mesmos e outros aplicativos que usavam os arquivos de componente de núcleo de versão mais antigos agora usará os arquivos da versão mais recentes.  
  
 Em uma nova instalação de componentes principais, drivers e conversores de ODBC, o programa de instalação do aplicativo deve chamar as funções a seguir na sequência: **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLConfigDriver** (com um *frequentes* de ODBC_INSTALL_DRIVER) e, em seguida,  **SQLInstallTranslatorEx**. Em uma desinstalação dos componentes principais, drivers e conversores, o programa de instalação do aplicativo deve chamar as funções a seguir na sequência: **SQLRemoveTranslator**, **SQLRemoveDriver**e então **SQLRemoveDriverManager**. Essas funções devem ser chamadas nessa sequência. Em uma atualização de todos os componentes, todas as funções de desinstalação devem ser chamadas na sequência e, em seguida, todas as funções de instalação devem ser chamadas na sequência.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionar, modificar ou remover um driver|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Instalar um driver|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|Instalando um tradutor|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|Remoção de um driver|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|Removendo o Gerenciador de Driver|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|Removendo um tradutor|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
