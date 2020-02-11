---
title: SQLManageDataSources | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLManageDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLManageDataSources
helpviewer_keywords:
- SQLManageDataSources [ODBC]
ms.assetid: ac6d186f-b394-406c-94c4-c6331d1ca468
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 819856a584c6133e28e222a704b720337f99cd9c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68018958"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**Conformidade**  
 Versão introduzida: ODBC 2,0  
  
 **Resumo**  
 **SQLManageDataSources** exibe uma caixa de diálogo com a qual os usuários podem configurar, adicionar e excluir fontes de dados nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HWND*  
 Entrada Identificador de janela pai.  
  
## <a name="returns"></a>Retornos  
 **SQLManageDataSources** retornará false se *HWND* não for um identificador de janela válido. Caso contrário, ele retorna VERDADEIRO.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLManageDataSources** retorna false, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|DESCRIÇÃO|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na *solicitação*|Falha na chamada para **ConfigDSN** .|  
|ODBC_ERROR_INVALID__HWND|Identificador de janela inválido|O argumento *HWND* era inválido ou nulo.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="managing-data-sources"></a>Gerenciar fontes de dados  
 O **SQLManageDataSources** inicialmente exibe a caixa de diálogo **administrador de fonte de dados ODBC** , conforme mostrado na ilustração a seguir.  
  
 ![Caixa de diálogo Administrador da Fonte de Dados ODBC](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 A caixa de diálogo exibe as fontes de dados listadas nas informações do sistema em três guias: **DSN do usuário**, **DSN do sistema**e DSN do **arquivo**. Se o usuário clicar duas vezes em uma fonte de dados ou selecionar uma fonte de dados e clicar em **Configurar**, **SQLManageDataSources** CHAMARá **ConfigDSN** na DLL de instalação com a opção ODBC_CONFIG_DSN.  
  
 Se o usuário clicar em **Adicionar**, o **SQLManageDataSources** exibirá a caixa de diálogo **criar nova fonte de dados** , mostrada na ilustração a seguir.  
  
 ![Caixa de diálogo Criar Nova Fonte de Dados](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 A caixa de diálogo exibe uma lista de drivers instalados. Se o usuário clicar duas vezes em um driver ou selecionar um driver e clicar em **OK**, **SQLManageDataSources** CHAMARá **ConfigDSN** na DLL de instalação e passará a opção ODBC_ADD_DSN.  
  
 Se o usuário selecionar uma fonte de dados e clicar em **remover**, **SQLManageDataSources** perguntará se o usuário deseja excluir a fonte de dados. Se o usuário clicar em **Sim**, **SQLManageDataSources** CHAMARá **ConfigDSN** na DLL de instalação com a opção ODBC_REMOVE_DSN.  
  
 A caixa de diálogo **criar nova fonte de dados** é usada para adicionar ou excluir uma fonte de dados de usuário, uma fonte de dados do sistema ou uma fonte de dados de arquivo.  
  
## <a name="user-dsns"></a>DSNs do usuário  
 Os DSNs criados para usuários individuais serão chamados de DSNs de usuário para distingui-los de DSNs do sistema. Os DSNs de usuário são registrados da seguinte maneira nas informações do sistema:  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>DSNs do sistema  
 A caixa de diálogo **criar nova fonte de dados** permite que você adicione uma fonte de dados do sistema ao computador local ou exclua uma, ou defina a configuração de uma fonte de dados do sistema.  
  
 Uma fonte de dados configurada com um nome de fonte de dados do sistema (DSN) pode ser usada por mais de um usuário no mesmo computador. Ele também pode ser usado por um serviço de todo o usuário, que pode, então, obter acesso à fonte de dados, mesmo que não haja usuários conectados à máquina.  
  
 Um DSN de sistema é registrado na entrada de HKEY_LOCAL_MACHINE nas informações do sistema, e não na entrada de HKEY_CURRENT_USER. Ele não está vinculado a um usuário que faz logon com seu nome de usuário e senha específicos, mas pode ser usado por qualquer usuário desse computador ou por um serviço de todo o uso automático. No entanto, o DSN do sistema está vinculado a uma máquina. Ele não dá suporte à capacidade de usar DSNs remotos entre computadores. Os DSNs do sistema são registrados da seguinte maneira nas informações do sistema:  
  
 ODBC ODBC. ini de SOFTWARE HKEY_LOCAL_MACHINE  
  
## <a name="file-dsns"></a>DSNs de arquivo  
 Uma fonte de dados de arquivo não tem um nome de fonte de dados, assim como uma fonte de dados de computador e não está registrada em nenhum usuário ou máquina. As informações de conexão para essa fonte de dados estão contidas em um arquivo. DSN que pode ser copiado para qualquer computador. Uma fonte de dados de arquivo pode ser compartilhável; nesse caso, o arquivo. DSN reside em uma rede e pode ser usado simultaneamente por vários usuários na rede, contanto que o usuário tenha o driver apropriado instalado. Uma fonte de dados de arquivo também pode ser descompartilhável; nesse caso, ela pode ser usada somente em um único computador.  
  
 Para obter mais informações sobre fontes de dados de arquivo, consulte [conectando-se usando fontes de dados de arquivo](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)ou consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="managing-drivers"></a>Gerenciando drivers  
 Se o usuário clicar na guia **drivers** na caixa de diálogo **administrador de fonte de dados ODBC** , o **SQLManageDataSources** exibirá uma lista de drivers ODBC instalados no sistema, bem como informações sobre os drivers. A data exibida é a data de criação do driver, conforme mostrado na ilustração a seguir.  
  
 ![Guia Drivers de Administrador da Fonte de Dados ODBC](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>Opções de Rastreamento  
 Se o usuário clicar na guia **rastreamento** na caixa de diálogo **administrador de fonte de dados ODBC** , o **SQLManageDataSources** exibirá opções de rastreamento, conforme mostrado na ilustração a seguir.  
  
 ![Guia Rastreamento do Administrador da Fonte de Dados ODBC](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 Se o usuário clicar em **Iniciar rastreamento agora** e clicar em **OK**, o **SQLManageDataSources** habilitará o rastreamento manualmente para todos os aplicativos atualmente em execução no computador.  
  
 Se o usuário especificar o nome de um arquivo de rastreamento na caixa de texto **caminho do arquivo de log** e clicar em **OK**, **SQLManageDataSources** definirá a palavra-chave **TraceFile** na seção [ODBC] das informações do sistema para o nome especificado.  
  
> [!IMPORTANT]  
>  O suporte para Visual Studio Analyzer foi removido a partir do Windows 8 (Visual Studio Analyzer foi incluído apenas em versões anteriores do Visual Studio.). Para obter um mecanismo de solução de problemas alternativo, use o rastreamento de LICITAção.  
  
 Se o usuário clicar em **iniciar Visual Studio Analyzer** e clicar em **OK**, Visual Studio Analyzer será habilitado. Ela permanece habilitada até que o botão **parar Visual Studio Analyzer** seja clicado.  
  
 Para obter mais informações sobre o rastreamento, consulte [Tracing](../../../odbc/reference/develop-app/tracing.md). Para obter mais informações sobre as palavras-chave **trace** e **TraceFile** , consulte a [subchave ODBC](../../../odbc/reference/install/odbc-subkey.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Criando fontes de dados|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
