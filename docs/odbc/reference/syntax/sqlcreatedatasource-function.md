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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301196"
---
# <a name="sqlcreatedatasource-function"></a>Função SQLCreateDataSource
**Conformidade**  
 Versão introduzida: ODBC 2.0  
  
 **Resumo**  
 **SQLCreateDataSource** exibe uma caixa de diálogo com a qual o usuário pode adicionar uma fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hwnd*  
 [Entrada] Alça da janela dos pais.  
  
 *lpszDS*  
 [Entrada] Nome da fonte dos dados. *lpszDS* pode ser um ponteiro nulo ou uma seqüência vazia.  
  
## <a name="returns"></a>Retornos  
 **SQLCreateDataSource** retorna TRUE se a fonte de dados for criada. Caso contrário, ele retorna FALSO.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **sQLCreateDataSource** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_INVALID_HWND|Alça de janela inválida|O argumento *hwnd* era inválido ou NULO.|  
|ODBC_ERROR_INVALID_DSN|DSN inválido|O argumento *lpszDS* continha uma string que era inválida para um DSN.|  
|ODBC_ERROR_REQUEST_FAILED|*Falha na solicitação*|A chamada para **ConfigDSN** com a opção ODBC_ADD_DSN falhou.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de configuração do driver ou tradutor|A biblioteca de configuração do driver não pôde ser carregada.|  
|ODBC_ERROR_USER_CANCELED|Operação cancelada pelo usuário|O usuário cancelou a criação de uma nova fonte de dados.|  
|ODBC_ERROR_CREATE_DSN_FAILED|Não foi possível criar o DSN solicitado|Não foi possível conectar-se ao banco de dados; a chamada para **SQLDriverConnect** para um DSN de arquivo não retornou uma conexão bem sucedida.<br /><br /> Não foi possível escrever para o arquivo.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Se *hwnd* for nulo, **SQLCreateDataSource** retorna FALSO. Caso contrário, ele exibe a caixa de diálogo **Criar nova fonte de dados** com uma página de assistente para escolher o tipo de fonte de dados a ser configurado, conforme mostrado na ilustração a seguir.  
  
 ![Caixa de diálogo Criar Nova Fonte de Dados: selecionar tipo](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 A opção padrão é **File Data Data Source**. Quando uma fonte de dados foi escolhida e o **Next** clicou, a seguinte página de assistente que contém uma lista de drivers instalados é exibida.  
  
 ![Caixa de diálogo Criar Nova Fonte de Dados: selecionar driver](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 Se **Cancelar** for clicado, a caixa de diálogo desaparecerá e **SQLCreateDataSource** retorna FALSA com o código de erro de ODBC_ERROR_USER_CANCELED. Se a opção **Fonte de Dados** do Usuário ou Fonte de Dados do **Sistema** foi selecionada, o botão **Avançado** não está disponível.  
  
 Quando o botão **Next** for clicado, um dos seguintes ocorrerá, dependendo de qual tipo de fonte de dados foi selecionada:  
  
-   Se **a Fonte de Dados do Arquivo** foi selecionada, uma página de assistente será exibida para que o usuário digite um nome de arquivo.  
  
-   Se a Fonte de **Dados do Usuário** ou a Fonte de Dados do **Sistema** forselecionada, uma página do assistente exibindo o tipo de origem de dados e o driver será exibido para revisão e, quando **o Acabamento** for clicado, a fonte de dados será configurada.  
  
 Se **o Advanced** for clicado na página 'Criar nova fonte de dados', uma página do assistente será exibida para que o usuário digite informações específicas do driver. Na caixa de texto desta caixa de diálogo, digite o driver e as palavras-chave separadas por devoluções, conforme mostrado na ilustração a seguir.  
  
 ![Caixa de diálogo Configurações Avançadas de Criação de DSN de Arquivo](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 Palavras-chave específicas do driver podem ser encontradas sob a descrição do **SQLDriverConnect**. Todos, exceto **DSN,** são permitidos.  
  
 O padrão para verificar esta opção **'Verificar esta conexão'** é TRUE. Este padrão se aplica se esta página de assistente está ativada ou não. Se **OK** for clicado, a seqüência especificada na caixa de texto e o valor da opção **Verificar essa conexão** serão armazenados em cache. (Se o botão **Fechar** ou **cancelar** for clicado, qualquer informação específica do driver recém-inserida será perdida porque a seqüência especificada na caixa de texto e o valor da opção **Verificar essa conexão** não são armazenados em cache.)  
  
 Se a **Fonte de Dados de Arquivo** foi selecionada na primeira página do assistente, depois que um driver foi selecionado e os valores das palavras-chave foram inseridos na página do assistente Avançado, o usuário é solicitado a inserir um nome de arquivo. Clique **em Procurar** para procurar um nome de arquivo, nesse caso, o diretório padrão na caixa **Procurar** é especificado por uma combinação do caminho especificado pelo CommonFileDir em HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion e "ODBC\DataSources". (Se o CommonFileDir fosse "C:\Program Files\Common Files", o diretório padrão seria "C:\Program Files\Common Files\ODBC\Data Sources".)  
  
 Quando um nome de arquivo foi inserido e o **Next** é clicado, o nome do arquivo inserido é verificado para validade em relação às regras padrão de nomeação de arquivos do sistema operacional. Se o nome do arquivo for inválido, uma caixa de mensagem de erro notificará o usuário de que um nome de arquivo inválido foi inserido. Depois que o usuário reconhece a caixa de mensagens, o foco é retornado para a página de assistente na qual o nome do arquivo é inserido. Se o nome do arquivo for válido, uma página de assistente que mostra os pares de valor de palavra-chave selecionados será exibida para revisão, conforme mostrado na ilustração a seguir.  
  
 ![Caixa de diálogo Criar Nova Fonte de Dados: revisão](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 Se **o Concluir for** clicado e a Fonte de Dados do **Arquivo** for selecionada como o tipo de fonte de dados e se a opção Verificar **essa conexão** for TRUE, o **SQLDriverConnect** será chamado com as palavras-chave **SAVEFILE** e **DRIVER.** O *argumento DriverComplet* está definido como SQL_DRIVER_COMPLETE. O nome do arquivo para a palavra-chave **SAVEFILE** é o nome que foi inserido ou escolhido, e o nome do driver para a palavra-chave **DRIVER** é o nome escolhido. Se uma seqüência de conexão específica do driver foi especificada na página do assistente Avançado, essa seqüência será anexada após a palavra-chave **DRIVER.**  
  
 Se **o SQLDriverConnect** retornar SQL_SUCCESS, o Gerenciador de drivers criou o DSN de arquivo. **SQLCreateDataSource** retorna TRUE. Se **o SQLDriverConnect** não retornar SQL_SUCCESS, uma caixa de mensagem de aviso indica que uma conexão não poderia ser feita à fonte de dados. Um DSN com informações mínimas de conexão ainda pode ser criado. Esta caixa de mensagem permite que o usuário cancele ou continue com a criação do Arquivo DSN.  
  
 Se o usuário optar por continuar criando o DSN, esse processo continuará como se a opção **Verificar essa conexão** fosse definida como FALSE. Se o usuário optar por cancelar, FALSE será devolvido para **SQLCreateDataSource** com um código de erro de ODBC_ERROR_CREATE_DSN_FAILED.  
  
 Se **a Fonte de Dados de Arquivo** foi selecionada como o tipo de origem de dados e a opção Verificar essa **conexão** é FALSA, um DSN de arquivo será criado com a palavra-chave **DRIVER** e a seqüência de conexão especificada pelo usuário (se houver) da página assistente Avançada. Se a criação do arquivo foi bem sucedida, TRUE será devolvido para **SQLCreateDataSource**. Se a criação do arquivo não foi bem sucedida, uma caixa de mensagem de erro notifica o usuário com qualquer erro que tenha sido devolvido do sistema operacional. FALSE é devolvido para **SQLCreateDataSource** com um código de erro de ODBC_ERROR_CREATE_DSN_FAILED. Para obter mais informações sobre fontes de dados de arquivos, consulte [Conectar-se usando fontes de dados de arquivo](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)ou consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Se a **fonte de dados** do **usuário** ou do sistema foi selecionada como o tipo de origem dos dados, o **ConfigDSN** na biblioteca de configuração do driver será chamado com o ODBC_ADD_DSN *fRequest*. Para obter mais informações, consulte [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Gerenciar fontes de dados|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
