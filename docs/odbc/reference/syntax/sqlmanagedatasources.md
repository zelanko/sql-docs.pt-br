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
manager: craigg
ms.openlocfilehash: f22fc952f0394f9e59ca8d67c76d0b00594b0759
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62465980"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**Conformidade com**  
 Versão introduzida: ODBC 2.0  
  
 **Resumo**  
 **SQLManageDataSources** exibe uma caixa de diálogo com a qual os usuários podem configurar, adicionar e excluir fontes de dados nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hwnd*  
 [Entrada] Identificador de janela pai.  
  
## <a name="returns"></a>Retorna  
 **SQLManageDataSources** retornará FALSE se *hwnd* não é um identificador de janela válido. Caso contrário, ele retorna TRUE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLManageDataSources** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* falhou|A chamada para **ConfigDSN** falhou.|  
|ODBC_ERROR_INVALID__HWND|Identificador de janela inválido|O *hwnd* argumento era inválido ou nulo.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
  
## <a name="managing-data-sources"></a>Gerenciar fontes de dados  
 **SQLManageDataSources** exibe inicialmente o **administrador de fonte de dados ODBC** caixa de diálogo, conforme mostrado na ilustração a seguir.  
  
 ![Caixa de diálogo Administrador de fonte de dados ODBC](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 A caixa de diálogo exibe as fontes de dados listadas nas informações do sistema em três guias: **DSN de usuário**, **DSN de sistema**, e **DSN de arquivo**. Se o usuário clica duas vezes em uma fonte de dados ou seleciona uma fonte de dados e clica **configurar**, **SQLManageDataSources** chamadas **ConfigDSN** na configuração da DLL com o ODBC_CONFIG_ Opção de DSN.  
  
 Se o usuário clica **Add**, **SQLManageDataSources** exibe o **criar nova fonte de dados** caixa de diálogo, mostrada na ilustração a seguir.  
  
 ![Criar caixa de diálogo Nova fonte de dados](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 A caixa de diálogo exibe uma lista dos drivers instalados. Se o usuário clica duas vezes em um driver ou seleciona um driver e clica **Okey**, **SQLManageDataSources** chamadas **ConfigDSN** na configuração da DLL e a passa a opção ODBC_ADD_DSN.  
  
 Se o usuário seleciona uma fonte de dados e clicar **remova**, **SQLManageDataSources** pergunta se o usuário deseja excluir a fonte de dados. Se o usuário clica **Yes**, **SQLManageDataSources** chamadas **ConfigDSN** na configuração da DLL com a opção ODBC_REMOVE_DSN.  
  
 O **criar nova fonte de dados** caixa de diálogo é usada para adicionar ou excluir uma fonte de dados do usuário, uma fonte de dados do sistema ou uma fonte de dados de arquivo.  
  
## <a name="user-dsns"></a>DSNs do usuário  
 DSNs do usuário, para diferenciá-los de DSNs de sistema serão chamados DSNs criados para usuários individuais. DSNs do usuário são registrados desta forma nas informações do sistema:  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>DSNs de sistema  
 O **criar nova fonte de dados** caixa de diálogo permite que você adicionar uma fonte de dados do sistema em seu computador local ou exclua uma ou para definir a configuração para uma fonte de dados do sistema.  
  
 Uma fonte de dados configurado com um nome de fonte de dados do sistema (DSN) pode ser usada por mais de um usuário no mesmo computador. Ele também pode ser usado por um serviço de todo o sistema, que pode então obter acesso à fonte de dados, mesmo se nenhum usuário está conectado à máquina.  
  
 Um DSN de sistema está registrado na entrada HKEY_LOCAL_MACHINE nas informações do sistema, em vez de na entrada de HKEY_CURRENT_USER. Ele não está ligado a um usuário que fizer logon com o determinado nome de usuário e senha, mas pode ser usado por qualquer usuário dessa máquina ou por um serviço automático em todo o sistema. O DSN do sistema é, no entanto, vinculado a uma máquina. Ele não oferece suporte a capacidade de usar DSNs remotas entre computadores. DSNs de sistema são registrados desta forma nas informações do sistema:  
  
 HKEY_LOCAL_MACHINE    SOFTWARE       ODBC          Odbc.ini  
  
## <a name="file-dsns"></a>DSNs de arquivos  
 Uma fonte de dados de arquivo não tem um nome de fonte de dados, como faz uma fonte de dados de máquina e não está registrado para qualquer um usuário ou computador. As informações de conexão para essa fonte de dados estão contidas em um arquivo. DSN que pode ser copiado para qualquer máquina. Uma fonte de dados de arquivo pode ser compartilhável, caso em que o arquivo. DSN reside em uma rede e pode ser usada simultaneamente por vários usuários na rede desde que o usuário tem o driver apropriado instalado. Uma fonte de dados de arquivo também pode ser não compartilhável, caso em que ele pode ser usado apenas em um único computador.  
  
 Para obter mais informações sobre fontes de dados de arquivo, consulte [conectar fontes de dados de arquivo usando](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), ou consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="managing-drivers"></a>Gerenciamento de Drivers  
 Se o usuário clica o **Drivers** guia o **administrador de fonte de dados ODBC** caixa de diálogo **SQLManageDataSources** exibe uma lista de drivers ODBC instalados no sistema, bem como informações sobre os drivers. A data exibida é a data de criação do driver, conforme mostrado na ilustração a seguir.  
  
 ![Guia do administrador de fonte de dados ODBC Drivers](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>Opções de Rastreamento  
 Se o usuário clica o **rastreamento** guia o **administrador de fonte de dados ODBC** caixa de diálogo **SQLManageDataSources** exibe as opções de rastreamento, conforme mostrado no seguinte ilustração.  
  
 ![Guia rastreamento do administrador de fonte de dados ODBC](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 Se o usuário clica **Iniciar rastreamento agora** e, em seguida, clica em **Okey**, **SQLManageDataSources** habilita o rastreamento manualmente para todos os aplicativos em execução no momento no computador.  
  
 Se o usuário Especifica o nome de um arquivo de rastreamento na **caminho do arquivo de Log** caixa de texto e, em seguida, clica **Okey**, **SQLManageDataSources** define o **TraceFile** palavra-chave na seção [ODBC] as informações do sistema para o nome especificado.  
  
> [!IMPORTANT]  
>  Suporte para o analisador do Visual Studio foi removido a partir do Windows 8 (Visual Studio Analyzer foi incluído apenas em versões mais antigas do Visual Studio.). Para obter uma alternativa de mecanismo de solução de problemas, use o rastreamento da oferta.  
  
 Se o usuário clica **iniciar o Visual Studio Analyzer** e, em seguida, clica em **Okey**, Visual Studio Analyzer está habilitado. Ele permanecerá habilitado até que **parar o Visual Studio Analyzer** é clicado.  
  
 Para obter mais informações sobre rastreamento, consulte [rastreamento](../../../odbc/reference/develop-app/tracing.md). Para obter mais informações sobre o **rastreamento** e **TraceFile** palavras-chave, consulte [subchave ODBC](../../../odbc/reference/install/odbc-subkey.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Criando fontes de dados|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
