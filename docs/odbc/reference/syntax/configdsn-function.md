---
title: Função ConfigDSN | Microsoft Docs
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
ms.topic: article
apiname:
- ConfigDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDSN
helpviewer_keywords:
- ConfigDSN [ODBC]
ms.assetid: 01ced74e-c575-4a25-83f5-bd7d918123f8
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dec94050079f41415983a63eac0669070145b2fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="configdsn-function"></a>Função ConfigDSN
**Conformidade**  
 Versão introduzidas: ODBC 1.0  
  
 **Resumo**  
 **ConfigDSN** adiciona, modifica ou exclui as fontes de dados das informações do sistema. Ele pode solicitar ao usuário informações de conexão. Pode ser em uma instalação separada DLL ou a DLL do driver.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL ConfigDSN(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hwndParent*  
 [Entrada] Identificador da janela pai. A função não exibirá caixas de diálogo se o identificador é nulo.  
  
 *Frequentes*  
 [Entrada] Tipo de solicitação. O *frequentes* argumento deve conter um dos seguintes valores:  
  
 ODBC_ADD_DSN: Adicione uma nova fonte de dados.  
  
 ODBC_CONFIG_DSN: Configurar (modificar) uma fonte de dados.  
  
 ODBC_REMOVE_DSN: Remova uma fonte de dados.  
  
 *lpszDriver*  
 [Entrada] Descrição do driver (geralmente o nome do DBMS associado) apresentada aos usuários em vez do nome físico do driver.  
  
 *lpszAttributes*  
 [Entrada] Uma lista de atributos na forma de pares de valor de palavra-chave duplamente terminada em nulo. Para obter mais informações, consulte "Comentários".  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **ConfigDSN** retorna FALSE, um tipo de  *\*pfErrorCode* valor é postado para o buffer de erro de instalador por uma chamada para **SQLPostInstallerError** e pode ser obtida chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O *hwndParent* argumento era inválido.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de valor de palavra-chave inválida|O *lpszAttributes* argumento continha um erro de sintaxe.|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou conversor inválido|O *lpszDriver* argumento era inválido. Ele não pôde ser encontrado no registro.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O *frequentes* argumento não era um dos seguintes:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* falha|Não foi possível executar a operação solicitada pelo *frequentes* argumento.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Erro específico do driver ou do conversor|Um erro específico do driver para o qual não há nenhum erro de instalador ODBC definido. O *SzError* argumento em uma chamada para o **SQLPostInstallerError** a função deve conter a mensagem de erro específica do driver.|  
  
## <a name="comments"></a>Comentários  
 **ConfigDSN** recebe informações de conexão do instalador do DLL como uma lista de atributos na forma de pares de valor de palavra-chave. Cada par é encerrada com um byte nulo e a lista inteira é encerrada com um byte nulo. (Ou seja, dois bytes nulos marcar o fim da lista.) Não são permitidos espaços em torno do sinal de igual do par de valor de palavra-chave. **ConfigDSN** pode aceitar as palavras-chave que não são palavras-chave válidas para **SQLBrowseConnect** e **SQLDriverConnect**. **ConfigDSN** não necessariamente suporte a todas as palavras-chave que são palavras-chave válidas para **SQLBrowseConnect** e **SQLDriverConnect**. (**ConfigDSN** não aceita o **DRIVER** palavra-chave.) As palavras-chave usadas pelo **ConfigDSN** função deve oferecer suporte a todas as opções necessárias para recriar a fonte de dados usando o recurso de configuração automática do instalador. Quando os usos do **ConfigDSN** valores e os valores de cadeia de caracteres de conexão são os mesmos, as mesmas palavras-chave devem ser usadas.  
  
 Como em **SQLBrowseConnect** e **SQLDriverConnect**, as palavras-chave e seus valores não devem conter o **[] {} (),? \*=! @** caracteres e o valor da **DSN** palavra-chave não pode consistir apenas de espaços em branco. Devido a gramática do registro, nomes de fontes de dados e palavras-chave não podem conter uma barra invertida (\\) caracteres.  
  
 **ConfigDSN** devem chamar **SQLValidDSN** para verificar se o comprimento do nome de fonte de dados e verificar que não há caracteres inválidos são incluídos no nome. Se o nome da fonte de dados é maior do que SQL_MAX_DSN_LENGTH ou contém caracteres inválidos, **SQLValidDSN** retorna um erro e **ConfigDSN** retornará um erro. O comprimento do nome de fonte de dados também é verificado por **SQLWriteDSNToIni**.  
  
 Por exemplo, para configurar uma fonte de dados que requer uma ID de usuário, senha e nome de banco de dados, um aplicativo de instalação pode passar os seguintes pares de valor de palavra-chave:  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 Para obter mais informações sobre essas palavras-chave, consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) e documentação do driver de cada.  
  
 Para exibir uma caixa de diálogo *hwndParent* não pode ser nulo.  
  
## <a name="adding-a-data-source"></a>Adicionando uma fonte de dados  
 Se um nome de fonte de dados é passado para **ConfigDSN** na *lpszAttributes*, **ConfigDSN** verifica se o nome é válido. Se o nome da fonte de dados corresponde a um nome de fonte de dados existente e *hwndParent* for nulo, **ConfigDSN** substitui o nome existente. Se ele corresponder a um nome existente e *hwndParent* não for null, **ConfigDSN** solicita ao usuário para substituir o nome existente.  
  
 Se *lpszAttributes* contém informações suficientes para se conectar a uma fonte de dados **ConfigDSN** pode adicionar os dados de origem ou exibem uma caixa de diálogo com a qual o usuário pode alterar as informações de conexão. Se *lpszAttributes* não contém informações suficientes para se conectar a uma fonte de dados **ConfigDSN** deve determinar as informações necessárias; se *hwndParent* não for null, ele exibe uma caixa de diálogo para recuperar as informações do usuário.  
  
 Se **ConfigDSN** exibe uma caixa de diálogo, ele deve exibir quaisquer informações de conexão passadas a ele no *lpszAttributes*. Em particular, se um nome de fonte de dados foi passado, **ConfigDSN** exibe esse nome, mas não permite que o usuário alterá-lo. **ConfigDSN** pode fornecer valores padrão para obter informações de conexão não são passados para ele no *lpszAttributes*.  
  
 Se **ConfigDSN** não é possível obter informações de conexão completa para uma fonte de dados, ele retorna FALSE.  
  
 Se **ConfigDSN** pode obter informações de conexão completa para uma fonte de dados, ele chama **SQLWriteDSNToIni** no instalador do DLL para adicionar a nova especificação de fonte de dados para o arquivo Odbc.ini (ou o registro). **SQLWriteDSNToIni** adiciona o nome da fonte de dados à seção [fontes de dados ODBC], cria a seção de especificação de fonte de dados e adiciona o **DRIVER** palavra-chave com a descrição do driver como seu valor. **ConfigDSN** chamadas **SQLWritePrivateProfileString** no instalador do DLL para adicionar quaisquer outras palavras-chave e valores usados pelo driver.  
  
## <a name="modifying-a-data-source"></a>Modificando uma fonte de dados  
 Para modificar uma fonte de dados, um nome de fonte de dados deve ser passado para **ConfigDSN** na *lpszAttributes*. **ConfigDSN** verifica se o nome da fonte de dados está no arquivo Odbc.ini (ou registro).  
  
 Se *hwndParent* for nulo, **ConfigDSN** usa as informações no *lpszAttributes* para modificar as informações no arquivo Odbc.ini (ou registro). Se *hwndParent* não for null, **ConfigDSN** exibe uma caixa de diálogo usando as informações em *lpszAttributes*; para obter informações não em *lpszAttributes* , ele usa as informações das informações do sistema. O usuário pode modificar as informações antes de **ConfigDSN** armazena as informações do sistema.  
  
 Se o nome da fonte de dados foi alterado, **ConfigDSN** primeiro chama **SQLRemoveDSNFromIni** no instalador do DLL para remover os dados existentes da fonte de especificação do arquivo Odbc.ini (ou registro). Em seguida, ele segue as etapas na seção anterior para adicionar a nova especificação de fonte de dados. Se o nome da fonte de dados não foi alterado, **ConfigDSN** chamadas **SQLWritePrivateProfileString** no instalador do DLL para fazer outras alterações. **ConfigDSN** não pode excluir ou alterar o valor da **Driver** palavra-chave.  
  
## <a name="deleting-a-data-source"></a>Excluindo uma fonte de dados  
 Para excluir uma fonte de dados, um nome de fonte de dados deve ser passado para **ConfigDSN** na *lpszAttributes*. **ConfigDSN** verifica se o nome da fonte de dados está no arquivo Odbc.ini (ou registro). Depois, ele chama **SQLRemoveDSNFromIni** no instalador do DLL para remover a fonte de dados.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionar, modificar ou remover uma fonte de dados|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Obtendo um valor do arquivo Odbc.ini ou o registro|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|Removendo a fonte de dados padrão|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Remover um nome de fonte de dados do Odbc.ini (ou do registro)|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Adicionar um nome de fonte de dados para Odbc.ini (ou registro)|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|Gravar um valor para o arquivo Odbc.ini ou o registro|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
