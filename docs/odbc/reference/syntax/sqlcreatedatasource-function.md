---
title: Função SQLCreateDataSource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLCreateDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCreateDataSource
helpviewer_keywords:
- SQLCreateDataSource function [ODBC]
ms.assetid: 76ee851a-dca9-40cc-8e9e-eb3f74e560ee
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b6e3b90f9634abd1e22b923f12b8b8854c7427d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcreatedatasource-function"></a>Função SQLCreateDataSource
**Conformidade**  
 Versão introduzidas: ODBC 2.0  
  
 **Resumo**  
 **SQLCreateDataSource** exibe uma caixa de diálogo com a qual o usuário pode adicionar uma fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HWND*  
 [Entrada] Identificador da janela pai.  
  
 *lpszDS*  
 [Entrada] Nome da fonte de dados. *lpszDS* pode ser um ponteiro nulo ou uma cadeia de caracteres vazia.  
  
## <a name="returns"></a>Retorna  
 **SQLCreateDataSource** retorna TRUE se a fonte de dados é criada. Caso contrário, retornará FALSE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLCreateDataSource** retorna FALSE, um tipo de  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O *hwnd* argumento era nulo ou inválido.|  
|ODBC_ERROR_INVALID_DSN|DSN inválido|O *lpszDS* argumento continha uma cadeia de caracteres que era inválida para um DSN.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* falha|A chamada para **ConfigDSN** com a opção ODBC_ADD_DSN falhou.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de instalação de driver ou conversor|Não foi possível carregar a biblioteca de instalação do driver.|  
|ODBC_ERROR_USER_CANCELED|Operação cancelada pelo usuário|O usuário cancelou a criação de uma nova fonte de dados.|  
|ODBC_ERROR_CREATE_DSN_FAILED|Não foi possível criar o DSN solicitado|Não foi possível conectar ao banco de dados; a chamada para **SQLDriverConnect** para um DSN de arquivo não retornou uma conexão bem-sucedida.<br /><br /> Não foi possível gravar no arquivo.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido a uma falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Se *hwnd* for nulo, **SQLCreateDataSource** retorna FALSE. Caso contrário, exibe o **criar nova fonte de dados** caixa de diálogo com uma página do Assistente para escolher o tipo de fonte de dados a ser configurado, conforme mostrado na ilustração a seguir.  
  
 ![Criar caixa de diálogo Nova fonte de dados: Selecionar tipo de](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 A opção padrão é **fonte de dados do arquivo**. Quando uma fonte de dados foi escolhida e **próximo** clicado, a seguinte página do assistente que contém uma lista de drivers instalados é exibida.  
  
 ![Criar caixa de diálogo Nova fonte de dados: Selecionar driver](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 Se **Cancelar** é clicado, a caixa de diálogo caixa desaparecerá e **SQLCreateDataSource** retorna FALSE com o código de erro de ODBC_ERROR_USER_CANCELED. Se o **fonte de dados de usuário** ou **fonte de dados do sistema** opção foi selecionada, o **avançado** botão não estiver disponível.  
  
 Quando o **próximo** botão é clicado, o seguinte ocorrerá, dependendo do tipo de dados de origem foi selecionada:  
  
-   Se **fonte de dados de arquivo** foi selecionada, a página do assistente é exibida para o usuário insira um nome de arquivo.  
  
-   Se qualquer um dos **fonte de dados de usuário** ou **fonte de dados do sistema** foi selecionada, é exibida uma página de Assistente para exibir o tipo de fonte de dados e o driver para revisão e quando **concluir** é clicado, a fonte de dados é configurada.  
  
 Se **avançado** é clicado na página do Assistente para criar nova fonte de dados, uma página de assistente é exibida para o usuário insira informações específicas do driver. Na caixa de texto dessa caixa de diálogo, digite o driver e palavras-chave separadas por retorna, conforme mostrado na ilustração a seguir.  
  
 ![Caixa de diálogo de configurações de criação de DSN de arquivo antecipada](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 Palavras-chave específicas do driver de adicionais podem ser encontradas na descrição do **SQLDriverConnect**. Tudo, exceto **DSN** são permitidos.  
  
 O padrão para o **verificar esta Conexão** opção for TRUE. Esse padrão se aplica a esta página do assistente está ativada ou não. Se **Okey** é clicado, a cadeia de caracteres especificada na caixa de texto e o **verificar esta Conexão** valor de opção são armazenados em cache. (Se o **fechar** botão ou **Cancelar** é clicado, qualquer recentemente inseridas informações específicas de driver for perdidas porque a cadeia de caracteres especificada na caixa de texto e o **verificar esta Conexão** não estão em cache o valor da opção.)  
  
 Se **fonte de dados de arquivo** tiver sido selecionada na primeira página do assistente, em seguida, depois que um driver foi selecionado e os valores de palavra-chave foram inseridos na página do Assistente avançado, o usuário é solicitado a inserir um nome de arquivo. Clique em **procurar** para procurar um nome de arquivo, caso em que o diretório padrão no **procurar** caixa é especificada por uma combinação do caminho especificado por CommonFileDir em HKEY_LOCAL_MACHINE\SOFTWARE\ Microsoft\Windows\CurrentVersion e "ODBC\DataSources". (Se CommonFileDir "C:\Program Files\Common Files", o diretório padrão seria "C:\Program programas\Arquivos Comuns\odbc\fontes".)  
  
 Quando um nome de arquivo foi inserido e **próximo** é clicado, o arquivo nome inserido é verificado para validade nas regras de nomenclatura de arquivo padrão do sistema operacional. Se o nome do arquivo for inválido, uma caixa de mensagem de erro informa ao usuário se um nome de arquivo inválido foi inserido. Depois que o usuário confirma a caixa de mensagem, o foco é retornado para a página do assistente em que o nome do arquivo é inserido. Se o nome do arquivo é válido, uma página do assistente que mostra os pares de palavra-chave-valor selecionado é exibida para revisão, conforme mostrado na ilustração a seguir.  
  
 ![Criar caixa de diálogo Nova fonte de dados: analise](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 Se **concluir** é clicado e **fonte de dados de arquivo** foi selecionado como o tipo de fonte de dados e se o **verificar esta conexão** opção for TRUE,  **SQLDriverConnect** é chamado com o **SAVEFILE** e **DRIVER** palavras-chave. O *DriverCompletion* argumento é definido como SQL_DRIVER_COMPLETE. O nome do arquivo para o **SAVEFILE** palavra-chave é o nome que foi inserido ou escolhido e o nome do driver para o **DRIVER** palavra-chave é o nome que foi escolhido. Se uma cadeia de caracteres de conexão específicos de driver foi especificada na página do Assistente avançado, essa cadeia de caracteres é anexada após o **DRIVER** palavra-chave.  
  
 Se **SQLDriverConnect** retorna SQL_SUCCESS, o Gerenciador de Driver criou o DSN de arquivo. **SQLCreateDataSource** retorna TRUE. Se **SQLDriverConnect** não retorna SQL_SUCCESS, uma mensagem de aviso caixa indica que não foi possível estabelecer uma conexão à fonte de dados. Um DSN com informações de conexão mínima ainda pode ser criado. Esta caixa de mensagem permite que o usuário cancelar ou continuar com a criação de DSN de arquivo.  
  
 Se o usuário optar por continuar criando o DSN, esse processo continuará como se o **verificar esta conexão** opção foi definida como FALSE. Se o usuário optar por cancelar, FALSE será retornado para **SQLCreateDataSource** com um código de erro de ODBC_ERROR_CREATE_DSN_FAILED.  
  
 Se **fonte de dados de arquivo** foi selecionado como o tipo de fonte de dados e o **verificar esta conexão** opção é FALSE, um DSN de arquivo é criado com o **DRIVER** palavra-chave e especificado pelo usuário cadeia de conexão (se houver) da página de assistente avançado. Se a criação do arquivo foi bem-sucedida, será retornado verdadeiro para **SQLCreateDataSource**. Se a criação do arquivo não foi bem-sucedida, uma caixa de mensagem de erro notifica o usuário com o erro foi retornado do sistema operacional. É retornado falso para **SQLCreateDataSource** com um código de erro de ODBC_ERROR_CREATE_DSN_FAILED. Para obter mais informações sobre fontes de dados de arquivo, consulte [conectar fontes de dados de arquivo usando](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), ou consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Se **usuário** ou **fonte de dados do sistema** foi selecionado como o tipo de fonte de dados, **ConfigDSN** na configuração do driver biblioteca é chamada com o ODBC_ADD_DSN  *Frequentes*. Para obter mais informações, consulte [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Gerenciar fontes de dados|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
