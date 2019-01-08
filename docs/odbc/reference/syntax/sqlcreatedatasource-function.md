---
title: Função SQLCreateDataSource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba02c28f3243b623695e3e087490ef3f73c60385
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204335"
---
# <a name="sqlcreatedatasource-function"></a>Função SQLCreateDataSource
**Conformidade com**  
 Versão introduzida: ODBC 2.0  
  
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
 [Entrada] Identificador de janela pai.  
  
 *lpszDS*  
 [Entrada] Nome da fonte de dados. *lpszDS* pode ser um ponteiro nulo ou uma cadeia de caracteres vazia.  
  
## <a name="returns"></a>Retorna  
 **SQLCreateDataSource** retorna TRUE se a fonte de dados é criada. Caso contrário, retornará FALSE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLCreateDataSource** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O *hwnd* argumento era inválido ou nulo.|  
|ODBC_ERROR_INVALID_DSN|DSN inválido|O *lpszDS* argumento continha uma cadeia de caracteres que era inválida para um DSN.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* falhou|A chamada para **ConfigDSN** com a opção ODBC_ADD_DSN falhou.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de instalação do driver ou conversor|Não foi possível carregar a biblioteca de instalação do driver.|  
|ODBC_ERROR_USER_CANCELED|Operação cancelada pelo usuário|O usuário cancelou a criação de uma nova fonte de dados.|  
|ODBC_ERROR_CREATE_DSN_FAILED|Não foi possível criar o DSN solicitado|Não foi possível conectar ao banco de dados; a chamada para **SQLDriverConnect** para um DSN de arquivo não retornou uma conexão bem-sucedida.<br /><br /> Não foi possível gravar no arquivo.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Se *hwnd* for nulo, **SQLCreateDataSource** retorna FALSE. Caso contrário, ele exibe a **criar nova fonte de dados** caixa de diálogo com uma página do Assistente para escolher o tipo de fonte de dados a ser definido, conforme mostrado na ilustração a seguir.  
  
 ![Criar caixa de diálogo Nova fonte de dados: selecione o tipo](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 A opção padrão é **fonte de dados do arquivo**. Quando uma fonte de dados foi escolhida e **próxima** clicado, a seguinte página de assistente que contém uma lista dos drivers instalados é exibida.  
  
 ![Criar caixa de diálogo Nova fonte de dados: Selecionar driver](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 Se **cancele** é clicado, a caixa de diálogo caixa desaparece e **SQLCreateDataSource** retorna falso com o código de erro de ODBC_ERROR_USER_CANCELED. Se o **fonte de dados de usuário** ou **fonte de dados do sistema** opção foi selecionada, o **avançado** botão não estiver disponível.  
  
 Quando o **próxima** botão é clicado, o seguinte ocorrerá, dependendo de qual tipo de dados de origem foi selecionada:  
  
-   Se **fonte de dados de arquivo** foi selecionado, uma página do assistente é exibida para o usuário insira um nome de arquivo.  
  
-   Se qualquer um dos **fonte de dados de usuário** ou **fonte de dados do sistema** foi selecionado, uma página de assistente exibe o tipo de fonte de dados e o driver será exibida para revisão e quando **concluir** é clicado, a fonte de dados está configurada.  
  
 Se **avançado** é clicado na página do assistente Criar nova fonte de dados, uma página do assistente é exibida para o usuário insira informações específicas de driver. Na caixa de texto dessa caixa de diálogo, digite o driver e palavras-chave separadas por retorna, conforme mostrado na ilustração a seguir.  
  
 ![Caixa de diálogo de configurações de criação de DSN de arquivo de avanço](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 Palavras-chave específicas do driver de adicionais podem ser encontradas na descrição do **SQLDriverConnect**. Todos, exceto **DSN** são permitidos.  
  
 O padrão para o **verificar esta Conexão** opção for TRUE. Esse padrão se aplica a esta página do assistente está ativada ou não. Se **Okey** é clicado, a cadeia de caracteres especificada na caixa de texto e o **verificar esta Conexão** valor de opção são armazenados em cache. (Se o **feche** botão ou **Cancelar** é clicado, qualquer recentemente inserido informações específicas de driver serão perdidas, pois a cadeia de caracteres especificada na caixa de texto e o **verificar esta Conexão** não estão em cache o valor da opção.)  
  
 Se **fonte de dados de arquivo** tiver sido selecionada na primeira página do assistente, em seguida, depois que um driver foi selecionado e os valores de palavra-chave tenham sido inseridos na página de assistente avançado, o usuário é solicitado a inserir um nome de arquivo. Clique em **navegue** para procurar um nome de arquivo, caso em que o diretório padrão no **procurar** caixa é especificada por uma combinação do caminho especificado por CommonFileDir em HKEY_LOCAL_MACHINE\SOFTWARE\ Microsoft\Windows\CurrentVersion e "ODBC\DataSources". (Se CommonFileDir era "C:\Program Files\Common Files", o diretório padrão seria "C:\Program programas\Arquivos Comuns\odbc\fontes".)  
  
 Quando um nome de arquivo foi inserido e **próxima** é clicado, o arquivo de nome inserido é verificado quanto à validade contra as regras de nomenclatura de arquivo padrão do sistema operacional. Se o nome do arquivo for inválido, uma caixa de mensagem de erro notifica o usuário se um nome de arquivo inválido foi inserido. Depois que o usuário confirma a caixa de mensagem, o foco é retornado para a página do assistente em que o nome do arquivo é inserido. Se o nome do arquivo for válido, uma página de assistente que mostra os pares de palavra-chave-valor selecionado é exibida para revisão, conforme mostrado na ilustração a seguir.  
  
 ![Criar caixa de diálogo Nova fonte de dados: revisar](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 Se **terminar** é clicado e **fonte de dados de arquivo** foi selecionado como o tipo de fonte de dados e se o **verificar esta conexão** opção for TRUE,  **SQLDriverConnect** é chamado com o **SAVEFILE** e **DRIVER** palavras-chave. O *DriverCompletion* argumento é definido como SQL_DRIVER_COMPLETE. O nome do arquivo para o **SAVEFILE** palavra-chave é o nome que foi inserido ou escolhido e o nome do driver para o **DRIVER** palavra-chave é o nome que foi escolhido. Se uma cadeia de caracteres de conexão específicos de driver foi especificada na página de assistente avançado, essa cadeia de caracteres é acrescentada após o **DRIVER** palavra-chave.  
  
 Se **SQLDriverConnect** retorna SQL_SUCCESS, o Gerenciador de Driver tiver criado o DSN de arquivo. **SQLCreateDataSource** retorna TRUE. Se **SQLDriverConnect** não retorna SQL_SUCCESS, uma mensagem de aviso caixa indica que não foi possível estabelecer uma conexão à fonte de dados. Um DSN com informações de conexão mínima ainda pode ser criado. Essa caixa de mensagem permite que o usuário cancelar ou continuar com a criação de DSN de arquivo.  
  
 Se o usuário optar por continuar criando o DSN, esse processo continua como se o **Verifique se essa conexão** opção foi definida como FALSE. Se o usuário optar por cancelar, FALSO será retornado para **SQLCreateDataSource** com um código de erro de ODBC_ERROR_CREATE_DSN_FAILED.  
  
 Se **fonte de dados de arquivo** foi selecionado como o tipo de fonte de dados e o **verificar esta conexão** opção for FALSE, um DSN de arquivo é criado com o **DRIVER** palavra-chave e especificado pelo usuário cadeia de conexão (se houver) da página de assistente avançado. Se a criação do arquivo tiver sido bem-sucedida, será retornado verdadeiro para **SQLCreateDataSource**. Se a criação do arquivo não foi bem-sucedida, uma caixa de mensagem de erro notifica o usuário com o erro que foi retornado do sistema operacional. É retornado falso para **SQLCreateDataSource** com um código de erro de ODBC_ERROR_CREATE_DSN_FAILED. Para obter mais informações sobre fontes de dados de arquivo, consulte [conectar fontes de dados de arquivo usando](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), ou consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Se **usuário** ou **fonte de dados do sistema** foi selecionado como o tipo de fonte de dados **ConfigDSN** na configuração do driver biblioteca é chamada com o ODBC_ADD_DSN  *Frequentes*. Para obter mais informações, consulte [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Gerenciar fontes de dados|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
