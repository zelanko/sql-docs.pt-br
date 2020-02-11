---
title: Função SQLDriverConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDriverConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverConnect
helpviewer_keywords:
- SQLDriverConnect function [ODBC]
ms.assetid: e299be1d-5c74-4ede-b6a3-430eb189134f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9528280514be2eb2424b15a39ded3206aaca112f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104701"
---
# <a name="sqldriverconnect-function"></a>Função SQLDriverConnect
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ODBC  
  
 **Resumo**  
 **SQLDriverConnect** é uma alternativa ao **SQLConnect**. Ele dá suporte a fontes de dados que exigem mais informações de conexão do que os três argumentos em **SQLConnect**, caixas de diálogo para solicitar ao usuário todas as informações de conexão e fontes de dados que não estão definidas nas informações do sistema.  
  
 O **SQLDriverConnect** fornece os seguintes atributos de conexão:  
  
-   Estabeleça uma conexão usando uma cadeia de conexão que contenha o nome da fonte de dados, uma ou mais IDs de usuário, uma ou mais senhas e outras informações exigidas pela fonte de dados.  
  
-   Estabelecer uma conexão usando uma cadeia de conexão parcial ou nenhuma informação adicional; Nesse caso, o Gerenciador de driver e o driver podem solicitar informações de conexão ao usuário.  
  
-   Estabeleça uma conexão com uma fonte de dados que não esteja definida nas informações do sistema. Se o aplicativo fornecer uma cadeia de conexão parcial, o driver poderá solicitar informações de conexão ao usuário.  
  
-   Estabeleça uma conexão com uma fonte de dados usando uma cadeia de conexão construída com as informações em um arquivo. DSN.  
  
 Depois que uma conexão é estabelecida, **SQLDriverConnect** retorna a cadeia de conexão concluída. O aplicativo pode usar essa cadeia de caracteres para solicitações de conexão subsequentes. Para obter mais informações, consulte [conectando-se com SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLDriverConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLHWND         WindowHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr,  
     SQLUSMALLINT    DriverCompletion);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexão.  
  
 *WindowHandle*  
 Entrada Identificador de janela. O aplicativo pode passar o identificador da janela pai, se aplicável, ou um ponteiro nulo se o identificador de janela não for aplicável ou **SQLDriverConnect** não apresentará nenhuma caixa de diálogo.  
  
 *Inconnectionstring*  
 Entrada Uma cadeia de conexão completa (consulte a sintaxe em "Comentários"), uma cadeia de conexão parcial ou uma cadeia de caracteres vazia.  
  
 *StringLength1*  
 Entrada Comprimento de **Inconnectionstring*, em caracteres, se a cadeia de caracteres for Unicode, ou bytes se a cadeia de caracteres for ANSI ou DBCS.  
  
 *Outconnectstring*  
 Der Ponteiro para um buffer para a cadeia de conexão concluída. Após a conexão bem-sucedida com a fonte de dados de destino, esse buffer contém a cadeia de conexão concluída. Os aplicativos devem alocar pelo menos 1.024 caracteres para esse buffer.  
  
 Se *Outconnectionstring* for NULL, *StringLength2Ptr* ainda retornará o número total de caracteres (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *outconnectionstring*.  
  
 *BufferLength*  
 Entrada Comprimento do buffer **Outconnectstring* , em caracteres.  
  
 *StringLength2Ptr*  
 Der Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo o caractere de terminação nula) disponível para retornar \*em *outconnectionstring*. Se o número de caracteres disponíveis para retornar for maior ou igual a *BufferLength*, a cadeia de conexão concluída em \* *outconnectionstring* será truncada para *BufferLength* menos o comprimento de um caractere de terminação nula.  
  
 *DriverCompletion*  
 Entrada Sinalizador que indica se o driver ou o Gerenciador de driver deve solicitar mais informações de conexão:  
  
 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED ou SQL_DRIVER_NOPROMPT.  
  
 (Para obter informações adicionais, consulte "Comentários".)  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLDriverConnect** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *FHandleType* de SQL_HANDLE_DBC e um *hHandle* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLDriverConnect** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|O buffer \* *outconnectstring* não era grande o suficiente para retornar a cadeia de conexão inteira, portanto, a cadeia de conexão foi truncada. O comprimento da cadeia de conexão não truncada é retornado em **StringLength2Ptr*. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S00|Atributo de cadeia de conexão inválido|Uma palavra-chave de atributo inválida foi especificada na cadeia de conexão (*Inconnectionstring*), mas o driver foi capaz de se conectar à fonte de dados mesmo assim. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor da opção alterado|O driver não oferecia suporte ao valor especificado apontado pelo argumento *ValuePtr* em **SQLSetConnectAttr** e substituído um valor semelhante. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S08|Erro ao salvar o DSN do arquivo|A cadeia de caracteres em * \*inconnectionstring* continha uma palavra-chave **FILEDSN** , mas o arquivo. DSN não foi salvo. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S09|Palavra-chave inválida|(DM) a cadeia de caracteres em * \*inconnectionstring* continha uma palavra-chave **SaveFile** , mas não um **Driver** ou uma palavra-chave **FILEDSN** . (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08001|Cliente incapaz de estabelecer conexão|O driver não pôde estabelecer uma conexão com a fonte de dados.|  
|08002|Nome da conexão em uso|(DM) o *ConnectionHandle* especificado já foi usado para estabelecer uma conexão com uma fonte de dados e a conexão ainda estava aberta.|  
|08004|O servidor rejeitou a conexão|A fonte de dados rejeitou o estabelecimento da conexão para motivos definidos pela implementação.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver estava tentando se conectar falhou antes de a função **SQLDriverConnect** ter concluído o processamento.|  
|28000|Especificação de autorização inválida|O identificador de usuário ou a cadeia de caracteres de autorização, ou ambos, conforme especificado na cadeia de conexão (*Inconnectionstring*), violadas as restrições definidas pela fonte de dados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*szMessageText* descreve o erro e sua causa.|  
|HY000|Erro geral: DSN de arquivo inválido|(DM) a cadeia de caracteres em **Inconnectionstring* continha uma palavra-chave FILEDSN, mas o nome do arquivo. DSN não foi encontrado.|  
|HY000|Erro geral: não é possível criar o buffer de arquivo|(DM) a cadeia de caracteres em **Inconnectionstring* continha uma palavra-chave FILEDSN, mas o arquivo. DSN estava ilegível.|  
|HY001|Erro de alocação de memória|O Gerenciador de driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função **SQLDriverConnect** .<br /><br /> O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *ConnectionHandle*. A função foi chamada e, antes de concluir a execução, a [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamada em *ConnectionHandle*e, em seguida, a função **SQLDriverConnect** foi chamada novamente no *ConnectionHandle*.<br /><br /> Ou, a função **SQLDriverConnect** foi chamada e, antes de concluir a execução, **SQLCancelHandle** foi chamado no *ConnectionHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) outra função de execução assíncrona (não **SQLDriverConnect**) foi chamada para o *ConnectionHandle* e ainda estava em execução quando a função **SQLDriverConnect** foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função **SQLDriverConnect** não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor especificado para o argumento *StringLength1* era menor que 0 e não era igual a SQL_NTS.<br /><br /> (DM) o valor especificado para o argumento *BufferLength* era menor que 0.|  
|HY092|Identificador de atributo/opção inválido|(DM) o argumento *DriverCompletion* foi SQL_DRIVER_PROMPT e o argumento *WindowHandle* era um ponteiro nulo.|  
|HY110|Conclusão de driver inválida|(DM) o valor especificado para o argumento *DriverCompletion* não era igual a SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED ou SQL_DRIVER_NOPROMPT.<br /><br /> (DM) o pool de conexões foi habilitado e o valor especificado para o argumento *DriverCompletion* não era igual a SQL_DRIVER_NOPROMPT.|  
|HYC00|Recurso opcional não implementado|O driver não oferece suporte à versão do comportamento de ODBC que o aplicativo solicitou.|  
|HYT00|Tempo limite esgotado|O período de tempo limite de logon expirou antes da conclusão da conexão com a fonte de dados. O período de tempo limite é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver correspondente ao nome da fonte de dados especificado não oferece suporte à função.|  
|IM002|Fonte de dados não encontrada e nenhum driver padrão especificado|(DM) o nome da fonte de dados especificado na cadeia de conexão (*Inconnectionstring*) não foi encontrado nas informações do sistema e não havia nenhuma especificação de driver padrão.<br /><br /> (DM) a fonte de dados ODBC e as informações de driver padrão não foram encontradas nas informações do sistema.|  
|IM003|Não foi possível carregar o driver especificado|(DM) o driver listado na especificação de fonte de dados nas informações do sistema ou especificado pela palavra-chave do **Driver** não foi encontrado ou não pôde ser carregado por algum outro motivo.|  
|IM004|Falha no **SQLAllocHandle** do Driver em SQL_HANDLE_ENV|(DM) durante **SQLDriverConnect**, o Gerenciador de driver chamou a função **SQLAllocHandle** do driver com um *fHandleType* de SQL_HANDLE_ENV e o driver retornou um erro.|  
|IM005|Falha no **SQLAllocHandle** do Driver em SQL_HANDLE_DBC.|(DM) durante **SQLDriverConnect**, o Gerenciador de driver chamou a função **SQLAllocHandle** do driver com um *fHandleType* de SQL_HANDLE_DBC e o driver retornou um erro.|  
|IM006|Falha no **SQLSetConnectAttr** do driver|(DM) durante **SQLDriverConnect**, o Gerenciador de driver chamou a função **SQLSetConnectAttr** do driver e o driver retornou um erro.|  
|IM007|Nenhuma fonte de dados ou driver especificado; caixa de diálogo proibida|Nenhum nome de fonte de dados ou driver foi especificado na cadeia de conexão e *DriverCompletion* foi SQL_DRIVER_NOPROMPT.|  
|IM008|Falha na caixa de diálogo|O driver tentou exibir sua caixa de diálogo de logon e falhou.<br /><br /> *WindowHandle* era um ponteiro nulo e *DriverCompletion* não foi SQL_DRIVER_NO_PROMPT.|  
|IM009|Não é possível carregar a DLL de tradução|O driver não pôde carregar a DLL de tradução que foi especificada para a fonte de dados ou para a conexão.|  
|IM010|O nome da fonte de dados é muito longo|(DM) o valor do atributo para a palavra-chave DSN foi maior do que SQL_MAX_DSN_LENGTH caracteres.|  
|IM011|Nome de driver muito longo|(DM) o valor do atributo para a palavra-chave do **Driver** tinha mais de 255 caracteres.|  
|IM012|Erro de sintaxe de palavra-chave do DRIVER|(DM) o par de palavra-chave-valor da palavra-chave do **Driver** continha um erro de sintaxe.<br /><br /> (DM) a cadeia de caracteres em * \*inconnectionstring* continha uma palavra-chave **FILEDSN** , mas o arquivo. DSN não continha uma palavra-chave de **Driver** ou uma palavra-chave **DSN** .|  
|IM014|O DSN especificado contém uma incompatibilidade de arquitetura entre o driver e o aplicativo|(DM) 32-o aplicativo de bits usa um DSN que se conecta a um driver de 64 bits; ou vice-versa.|  
|IM015|Falha no SQLDriverConnect do driver em SQL_HANDLE_DBC_INFO_HANDLE|Se um driver retornar SQL_ERROR, o Gerenciador de driver retornará SQL_ERROR ao aplicativo e a conexão falhará.<br /><br /> Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desenvolvendo o reconhecimento do pool de conexões em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
|S1118|O driver não oferece suporte à notificação assíncrona|Quando o driver não dá suporte à notificação assíncrona, não é possível definir SQL_ATTR_ASYNC_DBC_EVENT ou SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>Comentários  
 Uma cadeia de conexão tem a seguinte sintaxe:  
  
 *Connection-String* :: = *Empty-String*[; *] &#124; atributo*[;] &#124; *atributo*; *cadeia de conexão*  
  
 *Empty-String* :: =*atributo* :: = *atributo-palavra-chave*=*atributo-valor* &#124; driver = [{]*atributo-valor*[}]  
  
 *atributo-palavra-chave* :: = DSN &#124; UID &#124; pwd &#124; *Driver-defined-atributo-palavra-chave*  
  
 *atributo-valor* :: = *cadeia de caracteres de caractere*  
  
 *Driver-definido-atributo-palavra-chave* :: = *identificador*  
  
 em que *cadeia de caracteres de caractere* tem zero ou mais caracteres; o *identificador* tem um ou mais caracteres; *atributo-a palavra-chave* não diferencia maiúsculas de minúsculas; *atributo-valor* pode diferenciar maiúsculas de minúsculas; e o valor da palavra-chave **DSN** não consiste exclusivamente em espaços em branco.  
  
 Devido à cadeia de conexão e à gramática de arquivos de inicialização, às palavras-chave e aos valores de atributo que contêm os caracteres **[]{}(),;? = \*! @** não incluído entre chaves deve ser evitado. O valor da palavra-chave **DSN** não pode consistir apenas em espaços em branco e não deve conter espaços em branco à esquerda. Devido à gramática das informações do sistema, as palavras-chave e os nomes das fontes de dados não podem conter\\o caractere de barra invertida ().  
  
 Os aplicativos não precisam adicionar chaves ao valor do atributo após a palavra-chave do **Driver** , a menos que o atributo contenha um ponto-e-vírgula (;); nesse caso, as chaves são necessárias. Se o valor do atributo que o driver recebe inclui chaves, o driver não deve removê-los, mas eles devem fazer parte da cadeia de conexão retornada.  
  
 Um DSN ou um valor de cadeia de conexão entre chaves{}() contendo qualquer um dos caracteres **[{}] (),;? = \*! @** é passado intacto para o driver. No entanto, ao usar esses caracteres em uma palavra-chave, o Gerenciador de driver retorna um erro ao trabalhar com DSNs de arquivo, mas passa a cadeia de conexão para o driver para cadeias de conexão regulares. Evite usar chaves inseridas em um valor de palavra-chave.  
  
 A cadeia de conexão pode incluir qualquer número de palavras-chave definidas pelo driver. Como a palavra-chave do **Driver** não usa informações das informações do sistema, o driver deve definir palavras-chaves suficientes para que um driver possa se conectar a uma fonte de dados usando apenas as informações na cadeia de conexão. (Para obter mais informações, consulte "diretrizes de driver", mais adiante nesta seção.) O driver define quais palavras-chave são necessárias para se conectar à fonte de dados.  
  
 A tabela a seguir descreve os valores de atributo das palavras-chave **DSN**, **FILEDSN**, **Driver**, **UID**, **pwd**e **SaveFile** .  
  
|Palavra-chave|Descrição do valor do atributo|  
|-------------|---------------------------------|  
|**DSN**|Nome de uma fonte de dados como retornado por **SQLDataSources** ou a caixa de diálogo fontes de dados de **SQLDriverConnect**.|  
|**FILEDSN**|Nome de um arquivo. DSN do qual uma cadeia de conexão será criada para a fonte de dados. Essas fontes de dados são chamadas de fontes de dados de arquivo.|  
|**DRIVER**|Descrição do driver conforme retornado pela função **Sqldrives** . Por exemplo, RDB ou SQL Server.|  
|**UID**|Uma ID de usuário.|  
|**PWD**|A senha correspondente à ID de usuário ou uma cadeia de caracteres vazia se não houver senha para a ID de usuário (PWD =;).|  
|**SAVEFILE**|O nome de arquivo de um arquivo. DSN no qual os valores de atributo das palavras-chave usadas para fazer a conexão atual e bem-sucedida devem ser salvos.|  
  
 Para obter informações sobre como um aplicativo escolhe uma fonte de dados ou driver, consulte [escolhendo uma fonte de dados ou um driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Se qualquer palavra-chave for repetida na cadeia de conexão, o driver usará o valor associado à primeira ocorrência da palavra-chave. Se as palavras-chave **DSN** e **Driver** estiverem incluídas na mesma cadeia de conexão, o Gerenciador de driver e o driver usarão a palavra-chave que aparece primeiro.  
  
 As palavras-chave **FILEDSN** e **DSN** são mutuamente exclusivas: a palavra-chave exibida primeiro é usada e aquela que aparece segundo é ignorada. As palavras-chave **FILEDSN** e **Driver** , por outro lado, não são mutuamente exclusivas. Se qualquer palavra-chave aparecer em uma cadeia de conexão com **FILEDSN**, o valor do atributo da palavra-chave na cadeia de conexão será usado em vez do valor do atributo da mesma palavra-chave no arquivo. DSN.  
  
 Se a palavra-chave **FILEDSN** for usada, as palavras-chave especificadas em um arquivo. DSN serão usadas para criar uma cadeia de conexão. (Para obter mais informações, consulte "fontes de dados de arquivo", mais adiante nesta seção.) A palavra-chave **UID** é opcional; um arquivo. DSN pode ser criado apenas com a palavra-chave **Driver** . A palavra-chave **pwd** não é armazenada em um arquivo. DSN. O diretório padrão para salvar e carregar um arquivo. DSN será uma combinação do caminho especificado por **CommonFileDir** em HKEY_LOCAL_MACHINE \Software\Microsoft\ Windows\CurrentVersion e "ODBC\DataSources". (Se CommonFileDir fosse "C:\Program Files\Common Files", o diretório padrão seria "C:\Program Files\Common Files\ODBC\Data sources".)  
  
> [!NOTE]  
>  Um arquivo. DSN pode ser manipulado diretamente chamando as funções [SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md) e [SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md) na DLL do instalador.  
  
 Se a palavra-chave **SaveFile** for usada, os valores de atributo das palavras-chave usadas para fazer a conexão atual serão salvas como um arquivo. DSN com o nome do valor do atributo da palavra-chave **SaveFile** . A palavra-chave **SaveFile** deve ser usada em conjunto com a palavra-chave **Driver** , a palavra-chave **FILEDSN** ou ambas, ou a função retorna SQL_SUCCESS_WITH_INFO com SQLSTATE 01S09 (palavra-chave inválida). A palavra-chave **SaveFile** deve aparecer antes da palavra-chave do **Driver** na cadeia de conexão ou os resultados serão indefinidos.  
  
## <a name="driver-manager-guidelines"></a>Diretrizes do Gerenciador de driver  
 O Gerenciador de driver constrói uma cadeia de conexão para passar para o driver no argumento *Inconnectionstring* da função **SQLDriverConnect** do driver. O Gerenciador de driver não modifica o argumento *Inconnectionstring* passado para ele pelo aplicativo.  
  
 A ação do Gerenciador de driver é baseada no valor do argumento *DriverCompletion* :  
  
-   SQL_DRIVER_PROMPT: se a cadeia de conexão não contiver o **Driver**, o **DSN**ou a palavra-chave **FILEDSN** , o Gerenciador de driver exibirá a caixa de diálogo fontes de dados. Ele constrói uma cadeia de conexão do nome da fonte de dados retornada pela caixa de diálogo e quaisquer outras palavras-chave passadas para ele pelo aplicativo. Se o nome da fonte de dados retornado pela caixa de diálogo estiver vazio, o Gerenciador de driver especificará o DSN de par de valor de palavra-chave = padrão. (Essa caixa de diálogo não exibirá uma fonte de dados com o nome "padrão".)  
  
-   SQL_DRIVER_COMPLETE ou SQL_DRIVER_COMPLETE_REQUIRED: se a cadeia de conexão especificada pelo aplicativo incluir a palavra-chave **DSN** , o Gerenciador de driver copiará a cadeia de conexão especificada pelo aplicativo. Caso contrário, ele usa as mesmas ações que faz quando *DriverCompletion* é SQL_DRIVER_PROMPT.  
  
-   SQL_DRIVER_NOPROMPT: o Gerenciador de driver copia a cadeia de conexão especificada pelo aplicativo.  
  
 Se a cadeia de conexão especificada pelo aplicativo contiver a palavra-chave **Driver** , o Gerenciador de driver copiará a cadeia de conexão especificada pelo aplicativo.  
  
 Usando a cadeia de conexão construída, o Gerenciador de driver determina qual driver usar, conecta-se a esse driver e passa a cadeia de conexão que ele construiu para o driver; para obter mais informações sobre a interação do Gerenciador de driver e o driver, consulte a seção "Comentários" na [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). Se a cadeia de conexão não contiver a palavra-chave **Driver** , o Gerenciador de driver determinará qual driver usar da seguinte maneira:  
  
1.  Se a cadeia de conexão contiver a palavra-chave **DSN** , o Gerenciador de driver recuperará o driver associado à fonte de dados das informações do sistema.  
  
2.  Se a cadeia de conexão não contiver a palavra-chave **DSN** ou se a fonte de dados não for encontrada, o Gerenciador de driver recuperará o driver associado à fonte de dados padrão das informações do sistema. (Para obter mais informações, consulte [subchave padrão](../../../odbc/reference/install/default-subkey.md).) O Gerenciador de driver altera o valor da palavra-chave **DSN** na cadeia de conexão para "padrão".  
  
3.  Se a palavra-chave **DSN** na cadeia de conexão for definida como "padrão", o Gerenciador de driver recuperará o driver associado à fonte de dados padrão das informações do sistema.  
  
4.  Se a fonte de dados não for encontrada e a fonte de dados padrão não for encontrada, o Gerenciador de driver retornará SQL_ERROR com SQLSTATE IM002 (fonte de dados não encontrada e nenhum driver padrão especificado).  
  
## <a name="file-data-sources"></a>Fontes de dados do arquivo  
 Se a cadeia de conexão especificada pelo aplicativo na chamada para **SQLDriverConnect** contiver a palavra-chave **FILEDSN** e essa palavra-chave não for substituída pela palavra-chave **DSN** ou **Driver** , o Gerenciador de driver criará uma cadeia de conexão usando as informações no arquivo. DSN e no argumento *inconnectionstring* . O Gerenciador de driver procede da seguinte maneira:  
  
1.  Verifica se o nome de arquivo do arquivo. DSN é válido. Caso contrário, ele retornará SQL_ERROR com SQLSTATE IM014 (nome inválido de DSN de arquivo). Se o nome do arquivo for uma cadeia de caracteres vazia ("") e SQL_DRIVER_NOPROMPT não for especificado, a caixa de diálogo **arquivo-abrir** será exibida. Se o nome do arquivo contiver um caminho válido, mas nenhum nome de arquivo ou nome de arquivo inválido, e SQL_DRIVER_NOPROMPT não for especificado, a caixa de diálogo **arquivo-abrir** será exibida com o diretório atual definido como aquele especificado no nome do arquivo. Se o nome do arquivo for uma cadeia de caracteres vazia ("") ou o nome do arquivo contiver um caminho válido, mas nenhum nome de arquivo ou um nome de arquivo inválido, e SQL_DRIVER_NOPROMPT for especificado, SQL_ERROR será retornado com SQLSTATE IM014 (nome inválido de DSN de arquivo).  
  
2.  Lê todas as palavras-chave na seção [ODBC] do arquivo. DSN. Se a palavra-chave do **Driver** não estiver presente, ela retornará SQL_ERROR com SQLSTATE IM012 (erro de sintaxe de palavra-chave do driver), exceto onde o arquivo. DSN não é compartilhável e, portanto, contém apenas a palavra-chave **DSN** .  
  
     Se a fonte de dados de arquivo não puder ser compartilhada, o Gerenciador de driver lerá o valor da palavra-chave **DSN** e se conectará conforme necessário para a fonte de dados do usuário ou do sistema apontada pela fonte de dados de arquivo não compartilhável. As etapas 3 a 5 não são executadas.  
  
3.  Constrói uma cadeia de conexão para o driver. A cadeia de conexão do driver é a União das palavras-chave especificadas no arquivo. DSN e as especificadas na cadeia de conexão do aplicativo original. Regras para a construção da cadeia de conexão do driver em que as palavras-chave se sobrepõem são as seguintes:  
  
    -   Se a palavra-chave do **Driver** existir na cadeia de conexão do aplicativo e os drivers especificados pelas palavras-chave do **Driver** não forem iguais no arquivo. DSN e na cadeia de conexão do aplicativo, as informações do driver no arquivo. DSN serão ignoradas e as informações do driver na cadeia de conexão do aplicativo serão usadas. Se os drivers especificados pela palavra-chave do **Driver** forem os mesmos no arquivo. DSN e na cadeia de conexão do aplicativo, em que todas as palavras-chaves se sobrepõem, as especificadas na cadeia de conexão do aplicativo terão precedência sobre aquelas especificadas no arquivo. DSN.  
  
    -   Na nova cadeia de conexão, a palavra-chave **FILEDSN** é eliminada.  
  
4.  Carrega o driver examinando a entrada do registro HKEY_LOCAL_MACHINE \SOFTWARE\ODBC\ODBCINST. INI\\<nome\>do driver \Driver \<em que o nome do driver> é especificado pela palavra-chave do **Driver** .  
  
5.  Passa o driver para a nova cadeia de conexão.  
  
 Para obter exemplos de arquivos. DSN, consulte [conectar-se usando fontes de dados de arquivo](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md).  
  
## <a name="savefile-keyword"></a>Palavra-chave SAVEFILE  
 Se a cadeia de conexão especificada pelo aplicativo contiver a palavra-chave **SaveFile** , o Gerenciador de driver salvará a cadeia de conexão em um arquivo. DSN. O Gerenciador de driver procede da seguinte maneira:  
  
1.  Verifica se o nome do arquivo. DSN incluído como o valor do atributo da palavra-chave **SaveFile** é válido. Caso contrário, ele retornará SQL_ERROR com SQLSTATE IM014 (nome inválido de DSN de arquivo). A validade do nome do arquivo é determinada pelas regras de nomenclatura padrão do sistema. Se o nome do arquivo for uma cadeia de caracteres vazia ("") e o argumento *DriverCompletion* não for SQL_DRIVER_NOPROMPT, o nome do arquivo será válido. Se o nome do arquivo já existir, se *DriverCompletion* for SQL_DRIVER_NOPROMPT, o arquivo será substituído. Se *DriverCompletion* for SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE ou SQL_DRIVER_COMPLETE_REQUIRED, uma caixa de diálogo solicitará que o usuário especifique se o arquivo deve ser substituído. Se não for inserido, a caixa de diálogo **arquivo-salvar** será exibida.  
  
2.  Se o driver retornar SQL_SUCCESS e o nome do arquivo não for uma cadeia de caracteres vazia, o Gerenciador de driver gravará as informações de conexão retornadas no argumento *Outconnectionstring* para o arquivo especificado com o formato especificado na seção "cadeias de conexão" anteriormente nesta seção.  
  
3.  Se o driver retornar SQL_SUCCESS e o nome do arquivo era uma cadeia de caracteres vazia (""), o Gerenciador de driver chamará a caixa de diálogo comum de **salvar arquivo** com o *HWND* especificado e gravará as informações de conexão retornadas em *outconnectstring* para o arquivo especificado na caixa de diálogo comum de salvar arquivo com o formato especificado na seção "cadeias de conexão" anteriormente nesta seção  
  
4.  Se o driver retornar SQL_SUCCESS, ele retornará o argumento *Outconnectionstring* que contém a cadeia de conexão para o aplicativo.  
  
5.  Se o driver retornar SQL_SUCCESS_WITH_INFO ou SQL_ERROR, o Gerenciador de driver retornará o SQLSTATE ao aplicativo.  
  
## <a name="driver-guidelines"></a>Diretrizes de driver  
 O driver verifica se a cadeia de conexão passada para ele pelo Gerenciador de driver contém a palavra-chave **DSN** ou **Driver** . Se a cadeia de conexão contiver a palavra-chave **Driver** , o driver não poderá recuperar informações sobre a fonte de dados das informações do sistema. Se a cadeia de conexão contiver a palavra-chave **DSN** ou não contiver o **DSN** ou a palavra-chave **Driver** , o driver poderá recuperar informações sobre a fonte de dados das informações do sistema da seguinte maneira:  
  
1.  Se a cadeia de conexão contiver a palavra-chave **DSN** , o driver recuperará as informações da fonte de dados especificada.  
  
2.  Se a cadeia de conexão não contiver a palavra-chave **DSN** , a fonte de dados especificada não for encontrada ou a palavra-chave **DSN** for definida como "padrão", o driver recuperará as informações da fonte de dados padrão.  
  
 O driver usa todas as informações recuperadas das informações do sistema para aumentar as informações passadas para ele na cadeia de conexão. Se as informações nas informações do sistema duplicarem informações na cadeia de conexão, o driver usará as informações na cadeia de conexão.  
  
 Com base no valor de *DriverCompletion*, o driver solicita informações de conexão ao usuário, como a ID de usuário e a senha, e se conecta à fonte de dados:  
  
-   SQL_DRIVER_PROMPT: o driver exibe uma caixa de diálogo, usando os valores da cadeia de conexão e as informações do sistema (se houver) como valores iniciais. Quando o usuário sai da caixa de diálogo, o driver se conecta à fonte de dados. Ele também constrói uma cadeia de conexão do valor da palavra-chave **DSN** ou **Driver** em \* *inconnectionstring* e as informações retornadas na caixa de diálogo. Ele coloca essa cadeia de conexão no buffer **Outconnectstring* .  
  
-   SQL_DRIVER_COMPLETE ou SQL_DRIVER_COMPLETE_REQUIRED: se a cadeia de conexão contiver informações suficientes e essas informações estiverem corretas, o driver se conectará à fonte \*de dados e copiará *inconnectionstring* para \* *outconnectstring*. Se alguma informação estiver ausente ou incorreta, o driver usará as mesmas ações que faz quando *DriverCompletion* for SQL_DRIVER_PROMPT, exceto que se *DriverCompletion* for SQL_DRIVER_COMPLETE_REQUIRED, o driver desabilitará os controles de todas as informações não necessárias para se conectar à fonte de dados.  
  
-   SQL_DRIVER_NOPROMPT: se a cadeia de conexão contiver informações suficientes, o driver se conectará à fonte \*de dados e copiará *inconnectionstring* para \* *outconnectstring*. Caso contrário, o driver retornará SQL_ERROR para **SQLDriverConnect**.  
  
 Na conexão bem-sucedida com a fonte de dados, o driver também \*define *StringLength2Ptr* com o comprimento da cadeia de conexão de saída que está disponível para retornar em **outconnectionstring*.  
  
 Se o usuário cancelar uma caixa de diálogo apresentada pelo Gerenciador de driver ou pelo driver, **SQLDriverConnect** retornará SQL_NO_DATA.  
  
 Para obter informações sobre como o Gerenciador de driver e o driver interagem durante o processo de conexão, consulte [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Se um driver oferecer suporte a **SQLDriverConnect**, a seção de palavra-chave do driver das informações do sistema para o driver deverá conter a palavra-chave **ConnectFunctions** com o segundo conjunto de caracteres como "Y".  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>Conectando quando o pool de conexões está habilitado  
 O pooling de conexões permite que um aplicativo reutilize uma conexão que já foi criada. Quando **SQLDriverConnect** é chamado, o Gerenciador de driver tenta fazer a conexão usando uma conexão que faz parte de um pool de conexões em um ambiente designado para o pool de conexões. Para obter mais informações sobre o pool de conexões, consulte [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Um aplicativo pode definir SQL_ATTR_RESET_CONNECTION antes de chamar SQLDisconnect em uma conexão em que o pooling está habilitado. Para obter mais informações, consulte [função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 As seguintes restrições se aplicam quando um aplicativo chama **SQLDriverConnect** para se conectar a uma conexão em pool:  
  
-   Nenhum processamento de pooling de conexão é executado quando a palavra-chave **SaveFile** é especificada na cadeia de conexão.  
  
-   Se o pool de conexões estiver habilitado, **SQLDriverConnect** poderá ser chamado somente com um argumento *DriverCompletion* de SQL_DRIVER_NOPROMPT; Se **SQLDriverConnect** for chamado com qualquer outro *DRIVERCOMPLETION*, SQLSTATE HY110 (conclusão de driver inválida) será retornada.  
  
## <a name="connection-attributes"></a>Atributos de conexão  
 O atributo de conexão SQL_ATTR_LOGIN_TIMEOUT, definido usando **SQLSetConnectAttr**, define o número de segundos para aguardar a conclusão de uma solicitação de logon com uma conexão bem-sucedida pelo driver antes de retornar ao aplicativo. Se o usuário for solicitado a concluir a cadeia de conexão, um período de espera para cada solicitação de logon será iniciado quando o driver iniciar o processo de conexão.  
  
 O driver abre a conexão no modo de acesso SQL_MODE_READ_WRITE por padrão. Para definir o modo de acesso como SQL_MODE_READ_ONLY, o aplicativo deve chamar **SQLSetConnectAttr** com o atributo SQL_ATTR_ACCESS_MODE antes de chamar **SQLDriverConnect**.  
  
 Se uma biblioteca de tradução padrão for especificada nas informações do sistema para a fonte de dados, o driver a carregará. Uma biblioteca de tradução diferente pode ser carregada chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_LIB. Uma opção de conversão pode ser especificada chamando **SQLSetConnectAttr** com a opção SQL_ATTR_TRANSLATE_OPTION.  
  
 Para obter mais informações, consulte [conectando-se com SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
```cpp  
// SQLDriverConnect_ref.cpp  
// compile with: odbc32.lib user32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR OutConnStr[255];  
   SQLSMALLINT OutConnStrLen;  
  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect( // SQL_NULL_HDBC  
               hdbc,   
               desktopHandle,   
               (SQLCHAR*)"driver=SQL Server",   
               _countof("driver=SQL Server"),  
               OutConnStr,  
               255,   
               &OutConnStrLen,  
               SQL_DRIVER_PROMPT );  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {                 
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
 Consulte também [programa ODBC de exemplo](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando um identificador|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Descobrindo e enumerando os valores necessários para se conectar a uma fonte de dados|[Função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Conectando-se a uma fonte de dados|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Desconectando de uma fonte de dados|[Função SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Retornando descrições e atributos de driver|[Função SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Liberando um identificador|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Definindo um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
