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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b572a861af3479e1543be9fda9598cc7e25d36c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290205"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**Conformidade**  
 Versão introduzida: ODBC 2.0  
  
 **Resumo**  
 **SQLManageDataSources** exibe uma caixa de diálogo com a qual os usuários podem configurar, adicionar e excluir fontes de dados nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hwnd*  
 [Entrada] Alça da janela dos pais.  
  
## <a name="returns"></a>Retornos  
 **SQLManageDataSources** retorna FALSE se *hwnd* não for uma alça de janela válida. Caso contrário, ele retorna VERDADEIRO.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **sqlManageDataSources** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_REQUEST_FAILED|*Falha na solicitação*|A chamada para **configDSN** falhou.|  
|ODBC_ERROR_INVALID__HWND|Alça de janela inválida|O argumento *hwnd* era inválido ou NULO.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="managing-data-sources"></a>Gerenciar fontes de dados  
 **SQLManageDataSources** exibe inicialmente a caixa de diálogo **Administrador de Origem de Dados ODBC,** como mostrado na ilustração a seguir.  
  
 ![Caixa de diálogo Administrador da Fonte de Dados ODBC](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 A caixa de diálogo exibe as fontes de dados listadas nas informações do sistema em três guias: **DSN do usuário,** **Sistema DSN**e **Arquivo DSN**. Se o usuário clicar duas vezes em uma fonte de dados ou selecionar uma fonte de dados e clicar **em Configurar,** **SQLManageDataSources** chama **ConfigDSN** na configuração DLL com a opção ODBC_CONFIG_DSN.  
  
 Se o usuário clicar **em Adicionar**, **SQLManageDataSources** exibirá a caixa de diálogo **Criar nova fonte de dados,** mostrada na ilustração a seguir.  
  
 ![Caixa de diálogo Criar Nova Fonte de Dados](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 A caixa de diálogo exibe uma lista de drivers instalados. Se o usuário clicar duas vezes em um driver ou selecionar um driver e clicar em **OK,** **SQLManageDataSources** chama **ConfigDSN** na configuração DLL e passa-o a opção ODBC_ADD_DSN.  
  
 Se o usuário selecionar uma fonte de dados e clicar em **Remover,** **SQLManageDataSources** pergunta se o usuário deseja excluir a fonte de dados. Se o usuário clicar **em Sim,** **SQLManageDataSources** **chamará ConfigDSN** na configuração DLL com a opção ODBC_REMOVE_DSN.  
  
 A caixa de diálogo **Criar nova fonte de dados** é usada para adicionar ou excluir uma fonte de dados do usuário, uma fonte de dados do sistema ou uma fonte de dados de arquivo.  
  
## <a name="user-dsns"></a>Usuário DSNs  
 As DSNs criadas para usuários individuais serão chamadas dSNs de usuário, para distingui-las das DSNs do sistema. As DSNs do usuário são registradas da seguinte forma nas informações do sistema:  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>Sistema DSNs  
 A caixa de diálogo **Criar nova fonte de dados** permite adicionar uma fonte de dados do sistema ao seu computador local ou excluir uma, ou definir a configuração para uma fonte de dados do sistema.  
  
 Uma fonte de dados configurada com um nome de fonte de dados do sistema (DSN) pode ser usada por mais de um usuário na mesma máquina. Ele também pode ser usado por um serviço de todo o sistema, que pode então obter acesso à fonte de dados, mesmo se nenhum usuário estiver conectado à máquina.  
  
 Um Sistema DSN é registrado no HKEY_LOCAL_MACHINE entrada nas informações do sistema e não na entrada HKEY_CURRENT_USER. Ele não está vinculado a um usuário que faz logon com seu nome de usuário e senha particulares, mas pode ser usado por qualquer usuário dessa máquina ou por um serviço automático em todo o sistema. O sistema DSN está, no entanto, ligado a uma máquina. Ele não suporta a capacidade de usar DSNs remotas entre máquinas. Os DSNs do sistema são registrados da seguinte forma nas informações do sistema:  
  
 HKEY_LOCAL_MACHINE SOFTWARE ODBC Odbc.ini  
  
## <a name="file-dsns"></a>DSNs de arquivo  
 Uma fonte de dados de arquivo não tem um nome de origem de dados, assim como uma fonte de dados da máquina, e não está registrada em nenhum usuário ou máquina. As informações de conexão dessa fonte de dados estão contidas em um arquivo .dsn que pode ser copiado para qualquer máquina. Uma fonte de dados de arquivo pode ser compartilhada, nesse caso o arquivo .dsn reside em uma rede e pode ser usado simultaneamente por vários usuários na rede, desde que o usuário tenha o driver apropriado instalado. Uma fonte de dados de arquivo também pode ser incompartilhável, nesse caso, ele pode ser usado apenas em uma única máquina.  
  
 Para obter mais informações sobre as fontes de dados do arquivo, consulte [Conectar-se usando fontes de dados de arquivo](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)ou consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="managing-drivers"></a>Gerenciamento de drivers  
 Se o usuário clicar na guia **Drivers** na caixa de diálogo **Administrador de Origem de Dados oDBC,** o **SQLManageDataSources** exibirá uma lista de drivers ODBC instalados no sistema, bem como informações sobre os drivers. A data exibida é a data de criação do driver, conforme mostrado na ilustração a seguir.  
  
 ![Guia Drivers de Administrador da Fonte de Dados ODBC](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>Opções de Rastreamento  
 Se o usuário clicar na guia **Rastreamento** na caixa de diálogo **Administrador de Origem de Dados ODBC,** o **SQLManageDataSources** exibirá opções de rastreamento, conforme mostrado na ilustração a seguir.  
  
 ![Guia Rastreamento do Administrador da Fonte de Dados ODBC](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 Se o usuário clicar em **Iniciar rastreamento agora** e, em seguida, clicar em **OK,** **SQLManageDataSources** habilita o rastreamento manual mente para todos os aplicativos atualmente em execução na máquina.  
  
 Se o usuário especificar o nome de um arquivo de rastreamento na caixa de texto **Caminho do arquivo Log** e, em seguida, clicar em **OK,** **SQLManageDataSources** definirá a palavra-chave **TraceFile** na seção [ODBC] das informações do sistema para o nome especificado.  
  
> [!IMPORTANT]  
>  O suporte para Visual Studio Analyzer foi removido a partir do Windows 8 (visual Studio Analyzer foi incluído apenas em versões mais antigas do Visual Studio.). Para um mecanismo alternativo de solução de problemas, use o rastreamento BID.  
  
 Se o usuário clicar em **Iniciar o Analisador de Estúdio Visual** e, em seguida, clicar em **OK,** o Visual Studio Analyzer será ativado. Ele permanece ativado até que **o Stop Visual Studio Analyzer** seja clicado.  
  
 Para obter mais informações sobre rastreamento, consulte [Rastreamento](../../../odbc/reference/develop-app/tracing.md). Para obter mais informações sobre as palavras-chave **Trace** e **TraceFile,** consulte [Subchave ODBC](../../../odbc/reference/install/odbc-subkey.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Criando fontes de dados|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
