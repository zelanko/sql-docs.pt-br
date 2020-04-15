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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 88ec70d68b46beca97fd6b0d758e21aab5d4f4b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302767"
---
# <a name="sqldriverconnect-function"></a>Função SQLDriverConnect
**Conformidade**  
 Versão introduzida: ODBC 1.0 Normas Conformidade: ODBC  
  
 **Resumo**  
 **SQLDriverConnect** é uma alternativa ao **SQLConnect**. Ele suporta fontes de dados que requerem mais informações de conexão do que os três argumentos no **SQLConnect**, caixas de diálogo para solicitar ao usuário todas as informações de conexão e fontes de dados que não são definidas nas informações do sistema.  
  
 **O SQLDriverConnect** fornece os seguintes atributos de conexão:  
  
-   Estabeleça uma conexão usando uma seqüência de conexão que contenha o nome de origem dos dados, um ou mais IDs de usuário, uma ou mais senhas e outras informações exigidas pela fonte de dados.  
  
-   Estabelecer uma conexão usando uma seqüência de conexão parcial ou nenhuma informação adicional; neste caso, o Driver Manager e o driver podem solicitar ao usuário informações de conexão.  
  
-   Estabeleça uma conexão com uma fonte de dados que não esteja definida nas informações do sistema. Se o aplicativo forre uma seqüência de conexão parcial, o motorista pode solicitar informações ao usuário sobre a conexão.  
  
-   Estabeleça uma conexão a uma fonte de dados usando uma seqüência de conexão construída a partir das informações em um arquivo .dsn.  
  
 Depois que uma conexão é estabelecida, **o SQLDriverConnect** retorna a seqüência de conexões concluída. O aplicativo pode usar essa seqüência para solicitações de conexão subseqüentes. Para obter mais informações, consulte [Conectando com sqldriverconnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
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
 *ConexãoHandle*  
 [Entrada] Identificador de conexão.  
  
 *Windowhandle*  
 [Entrada] Alça da janela. O aplicativo pode passar a alça da janela pai, se aplicável, ou um ponteiro nulo se a alça da janela não for aplicável ou o **SQLDriverConnect** não apresentar nenhuma caixa de diálogo.  
  
 *String de inconexão*  
 [Entrada] Uma seqüência de conexão completa (veja a sintaxe em "Comentários"), uma seqüência de conexão parcial ou uma seqüência de string vazia.  
  
 *Comprimento da corda1*  
 [Entrada] Comprimento de **InConnectionString*, em caracteres se a seqüência é Unicode, ou bytes se string é ANSI ou DBCS.  
  
 *OutConnectionString*  
 [Saída] Ponteiro para um buffer para a seqüência de conexão concluída. Após a conexão bem-sucedida com a fonte de dados de destino, este buffer contém a seqüência de conexões concluída. Os aplicativos devem alocar pelo menos 1.024 caracteres para este buffer.  
  
 Se *OutConnectionString* for NULL, *StringLength2Ptr* ainda retornará o número total de caracteres (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado por *OutConnectionString*.  
  
 *BufferLength*  
 [Entrada] Comprimento do buffer ** OutConnectionString,* em caracteres.  
  
 *StringLength2Ptr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo o caractere de rescisão nula) disponível para retornar em \* *OutConnectionString*. Se o número de caracteres disponíveis para retornar for maior ou \*igual a *BufferLength,* a seqüência de caracteres de conexão concluída em *OutConnectionString* será truncada em *BufferLength* menos o comprimento de um caractere de rescisão nula.  
  
 *Conclusão do driver*  
 [Entrada] Sinalizador que indica se o Driver Manager ou o driver devem solicitar mais informações de conexão:  
  
 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED ou SQL_DRIVER_NOPROMPT.  
  
 (Para obter informações adicionais, consulte "Comentários.")  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLDriverConnect** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *fHandleType* de SQL_HANDLE_DBC e um *hHandle* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLDriverConnect** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|O \*buffer *OutConnectionString* não era grande o suficiente para retornar toda a seqüência de conexões, de modo que a seqüência de conexão foi truncada. O comprimento da seqüência de conexão não truncada é devolvido em **StringLength2Ptr*. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S00|Atributo de seqüência de conexão inválido|Uma palavra-chave de atributo inválida foi especificada na seqüência de conexões *(InConnectionString),* mas o driver foi capaz de se conectar à fonte de dados de qualquer maneira. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor da opção alterado|O driver não suportava o valor especificado apontado pelo argumento *ValuePtr* no **SQLSetConnectAttr** e substituiu um valor semelhante. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S08|DSN de salvamento de erros|A seqüência de string * \*em InConnectionString* continha uma palavra-chave **FILEDSN,** mas o arquivo .dsn não foi salvo. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S09|Palavra-chave inválida|(DM) A seqüência de string * \*em InConnectionString* continha uma palavra-chave **SAVEFILE,** mas não uma **palavra-chave DRIVER** ou **FILEDSN.** (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08001|Cliente incapaz de estabelecer conexão|O motorista não conseguiu estabelecer uma conexão com a fonte de dados.|  
|08002|Nome de conexão em uso|(DM) O *ConnectionHandle* especificado já havia sido usado para estabelecer uma conexão com uma fonte de dados, e a conexão ainda estava aberta.|  
|08004|Servidor rejeitou a conexão|A fonte de dados rejeitou o estabelecimento da conexão por razões definidas pela implementação.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava tentando se conectar falhou antes que a função **SQLDriverConnect** concluísse o processamento.|  
|28000|Especificação de autorização inválida|O identificador de usuário ou a seqüência de autorização, ou ambos, conforme especificado na seqüência de conexões *(InConnectionString),* violaram as restrições definidas pela fonte de dados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \*buffer szMessageText* descreve o erro e sua causa.|  
|HY000|Erro geral: Arquivo inválido dsn|(DM) A string in **InConnectionString* continha uma palavra-chave FILEDSN, mas o nome do arquivo .dsn não foi encontrado.|  
|HY000|Erro geral: Não é possível criar buffer de arquivos|(DM) A string em **InConnectionString* continha uma palavra-chave FILEDSN, mas o arquivo .dsn era ilegível.|  
|HY001|Erro de alocação de memória|O Gerenciador de driver não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função **SQLDriverConnect.**<br /><br /> O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *ConnectionHandle*. A função foi chamada e, antes de ser concluída, a [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamada no *ConnectionHandle*e, em seguida, a função **SQLDriverConnect** foi chamada novamente no *ConnectionHandle*.<br /><br /> Ou, a função **SQLDriverConnect** foi chamada e, antes de ser concluída, o **SQLCancelHandle** foi chamado no *ConnectionHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) Outra função de execução assíncrona (não **SQLDriverConnect)** foi chamada para o *ConnectionHandle* e ainda estava sendo executada quando a função **SQLDriverConnect** foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função **SQLDriverConnect** não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória baixas.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor especificado para o argumento *StringLength1* era inferior a 0 e não era igual a SQL_NTS.<br /><br /> (DM) O valor especificado para *o argumento BufferLength* foi inferior a 0.|  
|HY092|Identificador de atributo/opção inválido|(DM) O argumento *DriverComplet* foi SQL_DRIVER_PROMPT, e o argumento *WindowHandle* foi um ponteiro nulo.|  
|HY110|Conclusão inválida do driver|(DM) O valor especificado para o argumento *DriverComplet* não era igual a SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED ou SQL_DRIVER_NOPROMPT.<br /><br /> (DM) O pool de conexões foi ativado e o valor especificado para o argumento *DriverComplet* não era igual a SQL_DRIVER_NOPROMPT.|  
|HYC00|Recurso opcional não implementado|O driver não suporta a versão do comportamento ODBC que o aplicativo solicitou.|  
|HYT00|Tempo limite esgotado|O período de tempo de tempo de login expirou antes da conexão com a fonte de dados concluída. O período de tempo é definido através de **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver correspondente ao nome de origem de dados especificado não suporta a função.|  
|IM002|Fonte de dados não encontrada e nenhum driver padrão especificado|(DM) O nome de origem dos dados especificado na seqüência de conexões *(InConnectionString)* não foi encontrado nas informações do sistema e não havia especificação padrão do driver.<br /><br /> (DM) A fonte de dados ODBC e as informações padrão do driver não puderam ser encontradas nas informações do sistema.|  
|IM003|Driver especificado não pôde ser carregado|(DM) O driver listado na especificação de origem de dados nas informações do sistema ou especificado pela palavra-chave **DRIVER** não foi encontrado ou não pôde ser carregado por algum outro motivo.|  
|IM004|**SQLAllocHandle** do motorista no SQL_HANDLE_ENV falhou|(DM) Durante o **SQLDriverConnect,** o Driver Manager ligou para a função **SQLAllocHandle** do driver com um *fHandleType* de SQL_HANDLE_ENV e o motorista retornou um erro.|  
|IM005|**O SQLAllocHandle** do motorista no SQL_HANDLE_DBC falhou.|(DM) Durante o **SQLDriverConnect,** o Driver Manager ligou para a função **SQLAllocHandle** do driver com um *fHandleType* de SQL_HANDLE_DBC e o motorista retornou um erro.|  
|IM006|Falha no **SQLSetConnectAttr** do driver|(DM) Durante o **SQLDriverConnect,** o Driver Manager ligou para a função **SQLSetConnectAttr** do driver e o driver retornou um erro.|  
|IM007|Nenhuma fonte de dados ou driver especificado; diálogo proibido|Nenhum nome de origem de dados ou driver foi especificado na seqüência de conexões, e *DriverComplet* foi SQL_DRIVER_NOPROMPT.|  
|IM008|Falha no diálogo|O driver tentou exibir sua caixa de diálogo de login e falhou.<br /><br /> *WindowHandle* era um ponteiro nulo, e *DriverComplet* não foi SQL_DRIVER_NO_PROMPT.|  
|IM009|Não é possível carregar dll de tradução|O driver não conseguiu carregar a DLL de tradução especificada para a fonte de dados ou para a conexão.|  
|IM010|Nome de origem de dados muito longo|(DM) O valor de atributo para a palavra-chave DSN foi maior do que SQL_MAX_DSN_LENGTH caracteres.|  
|IM011|Nome do motorista muito longo|(DM) O valor de atributo para a palavra-chave **DRIVER** era superior a 255 caracteres.|  
|IM012|Erro de sintaxe de palavra-chave DRIVER|(DM) O par de valor de palavra-chave para a palavra-chave **DRIVER** continha um erro de sintaxe.<br /><br /> (DM) A string in * \*InConnectionString* continha uma palavra-chave **FILEDSN,** mas o arquivo .dsn não continha uma palavra-chave **DRIVER** ou uma palavra-chave **DSN.**|  
|IM014|O DSN especificado contém uma incompatibilidade de arquitetura entre o Driver e o Aplicativo|(DM) O aplicativo de 32 bits usa uma conexão DSN a um driver de 64 bits; ou vice-versa.|  
|IM015|Falha no SQLDriverConnect do driver em SQL_HANDLE_DBC_INFO_HANDLE|Se um motorista retornar SQL_ERROR, o Gerenciador de Driver retornará SQL_ERROR ao aplicativo e a conexão falhará.<br /><br /> Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [Developing Connection-Pool Awareness em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
|S1118|O driver não suporta notificação assíncrona|Quando o driver não suporta notificação assíncrona, não é possível definir SQL_ATTR_ASYNC_DBC_EVENT ou SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>Comentários  
 Uma seqüência de conexões tem a seguinte sintaxe:  
  
 *string de conexão* ::= *string vazio*[;] *&#124; atributo*[;] &#124; *atributo;* *conexão-string*  
  
 *string vazio* ::=*atributo* ::= *atributo-chave-palavra-valor-valor*=*attribute-value* &#124; DRIVER=[{]*valor de atributo*[}]  
  
 *palavra-chave de atributo* ::= DSN &#124; UID &#124; PWD &#124; *palavra-chave de atributo definida pelo driver*  
  
 *valor do atributo* ::= *caractere-string*  
  
 *palavra-chave de atributo definido pelo driver* ::= *identificador*  
  
 onde *a seqüência de caracteres* tem zero ou mais caracteres; *identificador* tem um ou mais caracteres; *apalavra-chave de atributo* não é sensível a maiúsculas e minúsculas; *o valor do atributo* pode ser sensível a maiúsculas e minúsculas; e o valor da palavra-chave **DSN** não consiste apenas em espaços em branco.  
  
 Por causa da gramática do arquivo de seqüência de conexão e inicialização, palavras-chave e valores de atributos que contêm os caracteres **[];?{} \*=!@** não fechado com aparelhos deve ser evitado. O valor da palavra-chave **DSN** não pode consistir apenas em espaços em branco e não deve conter espaços em branco. Devido à gramática das informações do sistema, palavras-chave e\\nomes de fonte de dados não podem conter o caractere barra invertida ( ).  
  
 As aplicações não têm que adicionar chaves em torno do valor do atributo após a palavra-chave **DRIVER,** a menos que o atributo contenha um ponto e vírgula (;), nesse caso as chaves são necessárias. Se o valor de atributo que o motorista recebe inclui chaves, o motorista não deve removê-los, mas eles devem fazer parte da seqüência de conexão retornada.  
  
 Um valor de seqüência de dSN ou conexão fechado com aparelhos (){}contendo qualquer um dos caracteres **[];?{} \*=!@** é passado intacto para o motorista. No entanto, ao usar esses caracteres em uma palavra-chave, o Gerenciador de driver retorna um erro ao trabalhar com DSNs de arquivo, mas passa a seqüência de conexão para o driver para seqüências de conexão regulares. Evite usar aparelhos incorporados em um valor de palavra-chave.  
  
 A seqüência de conexões pode incluir qualquer número de palavras-chave definidas pelo driver. Como a palavra-chave **DRIVER** não usa informações das informações do sistema, o driver deve definir palavras-chave suficientes para que um driver possa se conectar a uma fonte de dados usando apenas as informações na seqüência de conexão. (Para obter mais informações, consulte "Diretrizes do motorista", mais tarde nesta seção.) O driver define quais palavras-chave são necessárias para se conectar à fonte de dados.  
  
 A tabela a seguir descreve os valores de atributo das palavras-chave **DSN**, **FILEDSN,** **DRIVER,** **UID,** **PWD**e **SAVEFILE.**  
  
|Palavra-chave|Descrição do valor do atributo|  
|-------------|---------------------------------|  
|**DSN**|Nome de uma fonte de dados como retornado pelo **SQLDataSources** ou pela caixa de diálogo de fontes de dados do **SQLDriverConnect**.|  
|**FILEDSN**|Nome de um arquivo .dsn a partir do qual uma seqüência de conexão será construída para a fonte de dados. Essas fontes de dados são chamadas de fontes de dados de arquivos.|  
|**Driver**|Descrição do driver conforme devolvido pela função **SQLDrivers.** Por exemplo, Rdb ou SQL Server.|  
|**UID**|Uma ID de usuário.|  
|**Pwd**|A senha correspondente ao ID do usuário ou uma seqüência vazia se não houver senha para o ID do usuário (PWD=;).|  
|**Savefile**|O nome do arquivo de um arquivo .dsn no qual os valores de atributo das palavras-chave usadas para fazer o presente, conexão bem sucedida deve ser salvo.|  
  
 Para obter informações sobre como um aplicativo escolhe uma fonte de dados ou driver, consulte [Escolher uma Fonte de Dados ou Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Se alguma palavra-chave for repetida na seqüência de conexões, o driver usará o valor associado à primeira ocorrência da palavra-chave. Se as palavras-chave **DSN** e **DRIVER** estiverem incluídas na mesma seqüência de conexões, o Driver Manager e o driver usarão qual palavra-chave aparecer primeiro.  
  
 As palavras-chave **FILEDSN** e **DSN** são mutuamente exclusivas: qualquer palavra-chave que aparece primeiro é usada, e a que aparece em segundo é ignorada. As palavras-chave **FILEDSN** e **DRIVER,** por outro lado, não são mutuamente exclusivas. Se alguma palavra-chave aparecer em uma seqüência de conexão com **FILEDSN,** então o valor de atributo da palavra-chave na seqüência de conexões é usado em vez do valor de atributo da mesma palavra-chave no arquivo .dsn.  
  
 Se a palavra-chave **FILEDSN** for usada, as palavras-chave especificadas em um arquivo .dsn serão usadas para criar uma seqüência de conexões. (Para obter mais informações, consulte "Fontes de dados de arquivo", mais tarde nesta seção.) A **palavra-chave UID** é opcional; um arquivo .dsn pode ser criado apenas com a palavra-chave **DRIVER.** A **palavra-chave PWD** não está armazenada em um arquivo .dsn. O diretório padrão para salvar e carregar um arquivo .dsn será uma combinação do caminho especificado pelo **CommonFileDir** em HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion e "ODBC\DataSources". (Se o CommonFileDir fosse "C:\Program Files\Common Files", o diretório padrão seria "C:\Program Files\Common Files\ODBC\Data Sources".)  
  
> [!NOTE]  
>  Um arquivo .dsn pode ser manipulado diretamente chamando as funções [SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md) e [SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md) no instalador DLL.  
  
 Se a palavra-chave **SAVEFILE** for usada, os valores de atributo das palavras-chave usadas para fazer o presente, a conexão bem sucedida será salva como um arquivo .dsn com o nome do valor de atributo da palavra-chave **SAVEFILE.** A palavra-chave **SAVEFILE** deve ser usada em conjunto com a palavra-chave **DRIVER,** a palavra-chave **FILEDSN** ou ambas, ou a função retorna SQL_SUCCESS_WITH_INFO com SQLSTATE 01S09 (palavra-chave inválida). A palavra-chave **SAVEFILE** deve aparecer antes da palavra-chave **DRIVER** na seqüência de conexões, ou os resultados serão indefinidos.  
  
## <a name="driver-manager-guidelines"></a>Diretrizes do Driver Manager  
 O Gerenciador de driver constrói uma string de conexão para passar para o driver no argumento *InConnectionString* da função **SQLDriverConnect** do driver. O Gerenciador de driver não modifica o argumento *InConnectionString* aprovado pelo aplicativo.  
  
 A ação do Driver Manager baseia-se no valor do argumento *DriverCompletude:*  
  
-   SQL_DRIVER_PROMPT: Se a seqüência de conexões não contiver a palavra-chave **DRIVER,** **DSN**ou **FILEDSN,** o Gerenciador de driver exibirá a caixa de diálogo Fontes de dados. Ele constrói uma seqüência de conexão a partir do nome da fonte de dados retornado pela caixa de diálogo e quaisquer outras palavras-chave passadas a ele pelo aplicativo. Se o nome da fonte de dados retornado pela caixa de diálogo estiver vazio, o Gerenciador de driver especificará o par de valor de palavra-chave DSN=Default. (Esta caixa de diálogo não exibirá uma fonte de dados com o nome "Padrão".)  
  
-   SQL_DRIVER_COMPLETE ou SQL_DRIVER_COMPLETE_REQUIRED: Se a seqüência de conexão especificada pelo aplicativo incluir a palavra-chave **DSN,** o Gerenciador de driver saqueia a seqüência de conexões especificada pelo aplicativo. Caso contrário, ele toma as mesmas ações que faz quando *drivercomplet é* SQL_DRIVER_PROMPT.  
  
-   SQL_DRIVER_NOPROMPT: O Gerenciador de driver copia a seqüência de conexão especificada pelo aplicativo.  
  
 Se a seqüência de conexão especificada pelo aplicativo contiver a palavra-chave **DRIVER,** o Gerenciador de driver saqueia a seqüência de conexões especificada pelo aplicativo.  
  
 Usando a seqüência de conexões que construiu, o Driver Manager determina qual driver usar, conecta-se a esse driver e passa a string de conexão que construiu para o driver; para obter mais informações sobre a interação do Driver Manager e do driver, consulte a seção "Comentários" na [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). Se a seqüência de conexões não contiver a palavra-chave **DRIVER,** o Gerenciador de driver determinará qual driver usar da seguinte forma:  
  
1.  Se a seqüência de conexões contiver a palavra-chave **DSN,** o Gerenciador de driver recuperará o driver associado à fonte de dados das informações do sistema.  
  
2.  Se a seqüência de conexões não contiver a palavra-chave **DSN** ou a fonte de dados não for encontrada, o Gerenciador de driver recupera o driver associado à fonte de dados Padrão das informações do sistema. (Para obter mais informações, consulte [Subchave padrão](../../../odbc/reference/install/default-subkey.md).) O Gerenciador de driver altera o valor da palavra-chave **DSN** na seqüência de conexões para "DEFAULT".  
  
3.  Se a palavra-chave **DSN** na seqüência de conexões estiver definida como "DEFAULT", o Gerenciador de driver recuperará o driver associado à fonte de dados Padrão das informações do sistema.  
  
4.  Se a fonte de dados não for encontrada e a fonte de dados Padrão não for encontrada, o Gerenciador de driver retorna SQL_ERROR com o SQLSTATE IM002 (fonte de dados não encontrada e nenhum driver padrão especificado).  
  
## <a name="file-data-sources"></a>Fontes de dados do arquivo  
 Se a seqüência de conexão especificada pelo aplicativo na chamada para **SQLDriverConnect** contiver a palavra-chave **FILEDSN** e essa palavra-chave não for substituída pela palavra-chave **DSN** ou **DRIVER,** o Driver Manager criará uma seqüência de conexão usando as informações no arquivo .dsn e no argumento *InConnectionString.* O Driver Manager prossegue da seguinte forma:  
  
1.  Verifica se o nome do arquivo do arquivo .dsn é válido. Caso assim, ele retorna SQL_ERROR com SQLSTATE IM014 (nome inválido do arquivo DSN). Se o nome do arquivo for uma seqüência de string vazia ("") e SQL_DRIVER_NOPROMPT não for especificado, a caixa de diálogo **Abrir** arquivos será exibida. Se o nome do arquivo contiver um caminho válido, mas nenhum nome de arquivo ou um nome de arquivo inválido, e SQL_DRIVER_NOPROMPT não for especificado, a caixa de diálogo **Abrir arquivo** será exibida com o diretório atual definido para o especificado no nome do arquivo. Se o nome do arquivo for uma seqüência vazia ("") ou o nome do arquivo contiver um caminho válido, mas nenhum nome de arquivo ou um nome de arquivo inválido, e SQL_DRIVER_NOPROMPT for especificado, SQL_ERROR é retornado com SQLSTATE IM014 (nome inválido do arquivo DSN).  
  
2.  Lê todas as palavras-chave na seção [ODBC] do arquivo .dsn. Se a palavra-chave **DRIVER** não estiver presente, ela retorna SQL_ERROR com SQLSTATE IM012 (erro de sintaxe de palavra-chave driver), exceto quando o arquivo .dsn estiver incompartilhável e, portanto, contenha apenas a palavra-chave **DSN.**  
  
     Se a fonte de dados do arquivo não for compartilhável, o Driver Manager lê o valor da palavra-chave **DSN** e se conecta conforme necessário à fonte de dados do usuário ou do sistema apontada pela fonte de dados de arquivo incompartilhável. As etapas 3 a 5 não são executadas.  
  
3.  Constrói uma seqüência de conexão para o driver. A seqüência de conexão driver é a união das palavras-chave especificadas no arquivo .dsn e aquelas especificadas na seqüência de conexão de aplicativo original. Regras para a construção da cadeia de conexão do driver onde as palavras-chave se sobrepõem são as seguintes:  
  
    -   Se a palavra-chave **DRIVER** existir na seqüência de conexões de aplicativo e os drivers especificados pelas palavras-chave **DRIVER** não forem os mesmos no arquivo .dsn e na seqüência de conexão do aplicativo, então as informações do driver no arquivo .dsn são ignoradas e as informações do driver na cadeia de conexão de aplicativo são usadas. Se os drivers especificados pela palavra-chave **DRIVER** forem os mesmos no arquivo .dsn e na seqüência de conexões do aplicativo, então, quando todas as palavras-chave se sobrepõem, as especificadas na seqüência de conexão do aplicativo têm precedência sobre as especificadas no arquivo .dsn.  
  
    -   Na nova seqüência de conexões, a palavra-chave **FILEDSN** é eliminada.  
  
4.  Carrega o driver olhando na entrada do registro HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. INI\\<\>Nome do \<Driver \Driver onde o nome do motorista> é especificado pela palavra-chave **DRIVER.**  
  
5.  Passa ao driver a nova seqüência de conexões.  
  
 Para exemplos de arquivos .dsn, consulte [Conectar usando fontes de dados de arquivo](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md).  
  
## <a name="savefile-keyword"></a>SAVEFILE Palavra-chave  
 Se a seqüência de conexões especificada pelo aplicativo contiver a palavra-chave **SAVEFILE,** o Gerenciador de driver salvará a seqüência de conexões em um arquivo .dsn. O Driver Manager prossegue da seguinte forma:  
  
1.  Verifica se o nome do arquivo .dsn incluído como o valor de atributo da palavra-chave **SAVEFILE** é válido. Caso assim, ele retorna SQL_ERROR com SQLSTATE IM014 (nome inválido do arquivo DSN). A validade do nome do arquivo é determinada pelas regras padrão de nomeação do sistema. Se o nome do arquivo for uma seqüência de arquivos ("") e o argumento *DriverComplet* não for SQL_DRIVER_NOPROMPT, então o nome do arquivo é válido. Se o nome do arquivo já existir, se *DriverComplet for* SQL_DRIVER_NOPROMPT, o arquivo será substituído. Se *driverCompleta* estiver SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE ou SQL_DRIVER_COMPLETE_REQUIRED, uma caixa de diálogo solicita ao usuário que especifique se o arquivo deve ser substituído. Se Não for inserido, a caixa de diálogo **Salvar arquivos** será exibida.  
  
2.  Se o driver retornar SQL_SUCCESS e o nome do arquivo não for uma seqüência de arquivos, o Gerenciador de driver sapresentará as informações de conexão retornadas no argumento *OutConnectionString* para o arquivo especificado com o formato especificado na seção "Strings de conexão" anteriormente nesta seção.  
  
3.  Se o driver retornar SQL_SUCCESS e o nome do arquivo for uma seqüência de string vazia ("),então o Gerenciador de driver chamará a caixa de diálogo comum **File-Save** com o *hwnd* especificado e escreverá as informações de conexão retornadas no *OutConnectionString* para o arquivo especificado na caixa de diálogo 'Salvar arquivo' com o formato especificado na seção "Strings de conexão" anteriormente nesta seção.  
  
4.  Se o driver retornar SQL_SUCCESS, ele retorna o argumento *OutConnectionString* contendo a seqüência de conexões para o aplicativo.  
  
5.  Se o driver retornar SQL_SUCCESS_WITH_INFO ou SQL_ERROR, o Driver Manager readmente o SQLSTATE para o aplicativo.  
  
## <a name="driver-guidelines"></a>Diretrizes do motorista  
 O motorista verifica se a seqüência de conexão passada a ele pelo Driver Manager contém a palavra-chave **DSN** ou **DRIVER.** Se a seqüência de conexões contiver a palavra-chave **DRIVER,** o driver não poderá recuperar informações sobre a fonte de dados das informações do sistema. Se a seqüência de conexões contiver a palavra-chave **DRIVER** **DSN** ou não contiver a palavra-chave **DSN** ou driver, o driver poderá recuperar informações sobre a fonte de dados das informações do sistema da seguinte forma:  
  
1.  Se a seqüência de conexões contiver a palavra-chave **DSN,** o driver recuperará as informações para a fonte de dados especificada.  
  
2.  Se a seqüência de conexões não contiver a palavra-chave **DSN,** a fonte de dados especificada não será encontrada ou a palavra-chave **DSN** será definida como "DEFAULT", o driver recuperará as informações para a fonte de dados Padrão.  
  
 O driver usa qualquer informação que ele recupera das informações do sistema para aumentar as informações passadas a ele na seqüência de conexão. Se as informações nas informações do sistema duplicarem as informações na cadeia de conexão, o driver usará as informações na seqüência de conexão.  
  
 Com base no valor do *DriverComplet,* o driver solicita ao usuário informações de conexão, como o ID do usuário e a senha, e se conecta à fonte de dados:  
  
-   SQL_DRIVER_PROMPT: O driver exibe uma caixa de diálogo, usando os valores da seqüência de conexão e informações do sistema (se houver) como valores iniciais. Quando o usuário sai da caixa de diálogo, o driver se conecta à fonte de dados. Ele também constrói uma seqüência de conexão **DRIVER** a partir \*do valor da palavra-chave **DSN** ou DRIVER no *InConnectionString* e as informações retornadas da caixa de diálogo. Ele coloca esta seqüência de conexões no buffer ** OutConnectionString.*  
  
-   SQL_DRIVER_COMPLETE ou SQL_DRIVER_COMPLETE_REQUIRED: Se a seqüência de conexão contiver informações suficientes \*e essa \*informação estiver correta, o driver se conecta à fonte de dados e copia *InConnectionString* para *OutConnectionString*. Se alguma informação estiver faltando ou incorreta, o driver toma as mesmas ações que faz quando o *DriverComplet* é SQL_DRIVER_PROMPT, exceto que se o *DriverComplet* for SQL_DRIVER_COMPLETE_REQUIRED, o motorista desativa os controles para quaisquer informações não necessárias para se conectar à fonte de dados.  
  
-   SQL_DRIVER_NOPROMPT: Se a seqüência de conexões contiver informações \*suficientes, \*o driver se conecta à fonte de dados e copia *InConnectionString* para *OutConnectionString*. Caso contrário, o driver retorna SQL_ERROR para **SQLDriverConnect**.  
  
 Na conexão bem-sucedida com a \*fonte de dados, o driver também define *StringLength2Ptr* para o comprimento da seqüência de conexão de saída disponível para retornar em **OutConnectionString*.  
  
 Se o usuário cancelar uma caixa de diálogo apresentada pelo Gerenciador de driver ou pelo driver, o **SQLDriverConnect** retorna SQL_NO_DATA.  
  
 Para obter informações sobre como o Driver Manager e o driver interagem durante o processo de conexão, consulte [SQLConnect Function](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Se um driver suportar **o SQLDriverConnect,** a seção de palavras-chave do driver deve conter a palavra-chave **ConnectFunctions** com o segundo caractere definido como "Y".  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>Conectar quando o pool de conexões é ativado  
 O pool de conexões permite que um aplicativo reutilize uma conexão que já foi criada. Quando **o SQLDriverConnect** é chamado, o Driver Manager tenta fazer a conexão usando uma conexão que faz parte de um pool de conexões em um ambiente designado para pool de conexões. Para obter mais informações sobre o pool de conexões, consulte [SQLConnect Function](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Um aplicativo pode definir SQL_ATTR_RESET_CONNECTION antes de chamar SQLDisconnect em uma conexão onde o pooling está ativado. Para obter mais informações, consulte [SQLSetConnectAttr Function](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 As seguintes restrições se aplicam quando um aplicativo chama **o SQLDriverConnect** para se conectar a uma conexão agrupada:  
  
-   Nenhum processamento de pooling de conexão é realizado quando a palavra-chave **SAVEFILE** é especificada na seqüência de conexões.  
  
-   Se o pool de conexões estiver ativado, **o SQLDriverConnect** só poderá ser chamado com um argumento *DriverComplet* de SQL_DRIVER_NOPROMPT; se **o SQLDriverConnect** for chamado com qualquer outro *DriverCompletion*, SQLSTATE HY110 (Conclusão inválida do driver) será devolvido.  
  
## <a name="connection-attributes"></a>Atributos de conexão  
 O SQL_ATTR_LOGIN_TIMEOUT atributo de conexão, definido usando **SQLSetConnectAttr,** define o número de segundos para esperar que uma solicitação de login seja concluída com uma conexão bem-sucedida pelo driver antes de retornar ao aplicativo. Se o usuário for solicitado a concluir a seqüência de conexões, um período de espera para cada solicitação de login começa quando o driver inicia o processo de conexão.  
  
 O driver abre a conexão em SQL_MODE_READ_WRITE modo de acesso por padrão. Para definir o modo de acesso a SQL_MODE_READ_ONLY, o aplicativo deve chamar **SQLSetConnectAttr** com o atributo SQL_ATTR_ACCESS_MODE antes de chamar **SQLDriverConnect**.  
  
 Se uma biblioteca de tradução padrão for especificada nas informações do sistema para a fonte de dados, o driver a carregará. Uma biblioteca de tradução diferente pode ser carregada ligando para **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_LIB. Uma opção de tradução pode ser especificada ligando para **SQLSetConnectAttr** com a opção SQL_ATTR_TRANSLATE_OPTION.  
  
 Para obter mais informações, consulte [Conectando com sqldriverconnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
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
  
 Consulte também [o Programa Amostra ODBC](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando uma alça|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Descobrir e enumerar valores necessários para se conectar a uma fonte de dados|[Função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Conectando-se a uma fonte de dados|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Desconectando-se de uma fonte de dados|[Função SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Retornando descrições e atributos do driver|[Função SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Liberando uma alça|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Definindo um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
