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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94dc0d6d6f3b5bc96ae41aecda5b46f119cff85c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301196"
---
# <a name="sqlcreatedatasource-function"></a>Função SQLCreateDataSource
**Conformidade**  
 Versão introduzida: ODBC 2,0  
  
 **Resumo**  
 **SQLCreateDataSource** exibe uma caixa de diálogo com a qual o usuário pode adicionar uma fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HWND*  
 Entrada Identificador de janela pai.  
  
 *lpszDS*  
 Entrada Nome da fonte de dados. *lpszDS* pode ser um ponteiro nulo ou uma cadeia de caracteres vazia.  
  
## <a name="returns"></a>Retornos  
 **SQLCreateDataSource** retornará true se a fonte de dados for criada. Caso contrário, retornará FALSE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLCreateDataSource** retorna false, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O argumento *HWND* era inválido ou nulo.|  
|ODBC_ERROR_INVALID_DSN|DSN inválido|O argumento *lpszDS* continha uma cadeia de caracteres que era inválida para um DSN.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na *solicitação*|Falha na chamada para **ConfigDSN** com a opção ODBC_ADD_DSN.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de instalação do driver ou do Tradutor|Não foi possível carregar a biblioteca de instalação do driver.|  
|ODBC_ERROR_USER_CANCELED|Operação cancelada pelo usuário|O usuário cancelou a criação de uma nova fonte de dados.|  
|ODBC_ERROR_CREATE_DSN_FAILED|Não foi possível criar o DSN solicitado|Não foi possível conectar ao banco de dados; a chamada para **SQLDriverConnect** para um DSN de arquivo não retornou uma conexão bem-sucedida.<br /><br /> Não foi possível gravar no arquivo.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Se *HWND* for NULL, **SQLCreateDataSource** retornará false. Caso contrário, ele exibe a caixa de diálogo **criar nova fonte de dados** com uma página de assistente para escolher o tipo de fonte de dados a ser configurado, conforme mostrado na ilustração a seguir.  
  
 ![Caixa de diálogo Criar Nova Fonte de Dados: selecionar tipo](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 A opção padrão é **fonte de dados de arquivo**. Quando uma fonte de dados tiver sido escolhida e, **em seguida** , clicada, a página do assistente a seguir que contém uma lista de drivers instalados será exibida.  
  
 ![Caixa de diálogo Criar Nova Fonte de Dados: selecionar driver](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 Se **Cancel** for clicado, a caixa de diálogo desaparecerá e **SQLCreateDataSource** retornará false com o código de erro ODBC_ERROR_USER_CANCELED. Se a opção fonte de **dados do usuário** ou fonte de **dados do sistema** tiver sido selecionada, o botão **avançado** não estará disponível.  
  
 Quando o botão **Avançar** for clicado, ocorrerá uma das seguintes opções, dependendo de qual tipo de fonte de dados foi selecionado:  
  
-   Se a **fonte de dados de arquivo** tiver sido selecionada, uma página de assistente será exibida para que o usuário insira um nome de arquivo.  
  
-   Se a **fonte** de dados do usuário ou a **fonte de dados do sistema** tiver sido selecionada, uma página do assistente exibindo o tipo de fonte de dados e o driver será exibida para revisão e quando a opção **concluir** for clicada, a fonte de dados será configurada.  
  
 Se **avançado** for clicado na página Criar novo assistente de fonte de dados, será exibida uma página de assistente para que o usuário insira informações específicas do driver. Na caixa de texto dessa caixa de diálogo, digite o driver e as palavras-chave separadas por Devoluções, conforme mostrado na ilustração a seguir.  
  
 ![Caixa de diálogo Configurações Avançadas de Criação de DSN de Arquivo](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 Palavras-chave adicionais específicas do driver podem ser encontradas na descrição de **SQLDriverConnect**. Todos, exceto **DSN** , são permitidos.  
  
 O padrão para a opção **verificar esta conexão** é true. Esse padrão se aplica se esta página do assistente está ativada ou não. Se **OK** for clicado, a cadeia de caracteres especificada na caixa de texto e o valor da opção **verificar esta conexão** serão armazenados em cache. (Se o botão **fechar** ou **Cancelar** for clicado, todas as informações específicas do driver inseridas recentemente serão perdidas porque a cadeia de caracteres especificada na caixa de texto e o valor da opção **verificar esta conexão** não serão armazenados em cache.)  
  
 Se a **fonte de dados de arquivo** tiver sido selecionada na primeira página do assistente, depois que um driver tiver sido selecionado e os valores de palavra-chave tiverem sido inseridos na página avançado do assistente, será solicitado que o usuário insira um nome de arquivo. Clique em **procurar** para procurar um nome de arquivo; nesse caso, o diretório padrão na caixa de **procura** é especificado por uma combinação do caminho especificado por CommonFileDir em HKEY_LOCAL_MACHINE \Software\Microsoft\Windows\CurrentVersion e "ODBC\DataSources". (Se CommonFileDir fosse "C:\Program Files\Common Files", o diretório padrão seria "C:\Program Files\Common Files\ODBC\Data sources".)  
  
 Quando um nome de arquivo é inserido e o **próximo** é clicado, o nome de arquivo inserido é verificado quanto à validade em relação às regras de nomenclatura de arquivo padrão do sistema operacional. Se o nome do arquivo for inválido, uma caixa de mensagem de erro notificará o usuário de que um nome de arquivo inválido foi inserido. Depois que o usuário reconhece a caixa de mensagem, o foco é retornado para a página do assistente na qual o nome do arquivo é inserido. Se o nome do arquivo for válido, uma página do assistente que mostra os pares de palavras-chave selecionados será exibida para revisão, conforme mostrado na ilustração a seguir.  
  
 ![Caixa de diálogo Criar Nova Fonte de Dados: revisão](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 Se o botão **concluir** for clicado e a **fonte de dados de arquivo** tiver sido selecionada como o tipo de fonte de dados, e se a opção **verificar esta conexão** for verdadeira, **SQLDriverConnect** será chamado com as palavras-chave **SaveFile** e **Driver** . O argumento *DriverCompletion* é definido como SQL_DRIVER_COMPLETE. O nome do arquivo para a palavra-chave **SaveFile** é o nome que foi inserido ou escolhido e o nome do driver para a palavra-chave do **Driver** é o nome que foi escolhido. Se uma cadeia de conexão específica do driver tiver sido especificada na página do assistente avançado, essa cadeia de caracteres será anexada após a palavra-chave do **Driver** .  
  
 Se **SQLDriverConnect** retornar SQL_SUCCESS, o Gerenciador de driver criou o DSN do arquivo. **SQLCreateDataSource** retorna true. Se **SQLDriverConnect** não retornar SQL_SUCCESS, uma caixa de mensagem de aviso indicará que não foi possível estabelecer uma conexão com a fonte de dados. Um DSN com informações de conexão mínima ainda pode ser criado. Essa caixa de mensagem permite que o usuário cancele ou continue com a criação do DSN de arquivo.  
  
 Se o usuário optar por continuar criando o DSN, esse processo continuará como se a opção **verificar esta conexão** estivesse definida como false. Se o usuário optar por cancelar, FALSE será retornado para **SQLCreateDataSource** com um código de erro de ODBC_ERROR_CREATE_DSN_FAILED.  
  
 Se a **fonte de dados de arquivo** tiver sido selecionada como o tipo de fonte de dados e a opção **verificar esta conexão** for falsa, um DSN de arquivo será criado com a palavra-chave do **Driver** e a cadeia de conexão especificada pelo usuário (se houver) na página avançado do assistente. Se a criação do arquivo tiver sido bem-sucedida, TRUE será retornado para **SQLCreateDataSource**. Se a criação do arquivo não tiver sido bem-sucedida, uma caixa de mensagem de erro notificará o usuário com qualquer erro retornado do sistema operacional. FALSE é retornado para **SQLCreateDataSource** com um código de erro de ODBC_ERROR_CREATE_DSN_FAILED. Para obter mais informações sobre fontes de dados de arquivo, consulte [conectando-se usando fontes de dados de arquivo](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)ou consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Se a **fonte de dados** do **usuário** ou do sistema tiver sido selecionada como o tipo de fonte de dados, **ConfigDSN** na biblioteca de instalação do driver será chamada com o ODBC_ADD_DSN *fRequest*. Para obter mais informações, consulte [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Gerenciar fontes de dados|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
