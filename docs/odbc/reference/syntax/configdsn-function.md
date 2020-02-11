---
title: Função ConfigDSN | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 21a02107359b26c0dc30aa87acbf46c1ab1a172d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892848"
---
# <a name="configdsn-function"></a>Função ConfigDSN
**Conformidade**  
 Versão introduzida: ODBC 1,0  
  
 **Resumo**  
 O **ConfigDSN** adiciona, modifica ou exclui fontes de dados das informações do sistema. Ele pode solicitar ao usuário informações de conexão. Ele pode estar na DLL do driver ou em uma DLL de instalação separada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL ConfigDSN(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hwndParent*  
 Entrada Identificador de janela pai. A função não exibirá nenhuma caixa de diálogo se o identificador for nulo.  
  
 *fRequest*  
 Entrada Tipo de solicitação. O argumento *fRequest* deve conter um dos seguintes valores:  
  
 ODBC_ADD_DSN: adicionar uma nova fonte de dados.  
  
 ODBC_CONFIG_DSN: configurar (modificar) uma fonte de dados existente.  
  
 ODBC_REMOVE_DSN: remover uma fonte de dados existente.  
  
 *lpszDriver*  
 Entrada Descrição do driver (geralmente o nome do DBMS associado) apresentado aos usuários em vez do nome do driver físico.  
  
 *lpszAttributes*  
 Entrada Uma lista dupla de atributos terminada em nulo na forma de pares de palavra-chave-valor. Para obter mais informações, consulte "Comentários".  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **ConfigDSN** retorna false, um valor de * \*pfErrorCode* associado é Postado no buffer de erros do instalador por uma chamada para **SQLPostInstallerError** e pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|DESCRIÇÃO|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O argumento *hwndParent* era inválido.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de palavra-chave-valor inválidos|O argumento *lpszAttributes* continha um erro de sintaxe.|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou tradutor inválido|O argumento *lpszDriver* era inválido. Ele não foi encontrado no registro.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O argumento *fRequest* não era um dos seguintes:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|Falha na *solicitação*|Não foi possível executar a operação solicitada pelo argumento *fRequest* .|  
|ODBC_ERROR_DRIVER_SPECIFIC|Erro específico do driver ou do Tradutor|Um erro específico de driver para o qual não há erro de instalador ODBC definido. O argumento *SzError* em uma chamada para a função **SQLPostInstallerError** deve conter a mensagem de erro específica do driver.|  
  
## <a name="comments"></a>Comentários  
 O **ConfigDSN** recebe informações de conexão da dll do instalador como uma lista de atributos na forma de pares de palavras-chave/valor. Cada par é encerrado com um byte nulo e a lista inteira é encerrada com um byte nulo. (Ou seja, dois bytes nulos marcam o final da lista.) Os espaços não são permitidos em relação ao sinal de igual no par de palavra-chave-valor. O **ConfigDSN** pode aceitar palavras-chave que não são palavras-chave válidas para **SQLBrowseConnect** e **SQLDriverConnect**. O **ConfigDSN** não oferece necessariamente suporte a todas as palavras-chave que são palavras-chave válidas para **SQLBrowseConnect** e **SQLDriverConnect**. (O**ConfigDSN** não aceita a palavra-chave do **Driver** .) As palavras-chave usadas pela função **ConfigDSN** devem dar suporte a todas as opções necessárias para recriar a fonte de dados usando o recurso de configuração automática do instalador. Quando os valores de **ConfigDSN** e os valores de cadeia de conexão são os mesmos, as mesmas palavras-chave devem ser usadas.  
  
 Como em **SQLBrowseConnect** e **SQLDriverConnect**, as palavras-chave e seus valores não devem conter o **[]{}(),;? = \*! @** caracteres, e o valor da palavra-chave **DSN** não pode consistir apenas em espaços em branco. Devido à gramática do registro, as palavras-chave e os nomes de fonte de dados não podem\\conter o caractere de barra invertida ().  
  
 **ConfigDSN** deve chamar **SQLValidDSN** para verificar o comprimento do nome da fonte de dados e verificar se nenhum caractere inválido está incluído no nome. Se o nome da fonte de dados for maior que SQL_MAX_DSN_LENGTH ou incluir caracteres inválidos, **SQLValidDSN** retornará um erro e **ConfigDSN** retornará um erro. O comprimento do nome da fonte de dados também é verificado por **SQLWriteDSNToIni**.  
  
 Por exemplo, para configurar uma fonte de dados que exija uma ID de usuário, senha e nome de banco de dado, um aplicativo de instalação pode passar os seguintes pares de valores de palavra-chave:  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 Para obter mais informações sobre essas palavras-chave, consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) e a documentação de cada driver.  
  
 Para exibir uma caixa de diálogo, *hwndParent* não deve ser nulo.  
  
## <a name="adding-a-data-source"></a>Adicionando uma fonte de dados  
 Se um nome de fonte de dados for passado para **ConfigDSN** em *lpszAttributes*, **ConfigDSN** verificará se o nome é válido. Se o nome da fonte de dados corresponder a um nome de fonte de dados existente e *hwndParent* for nulo, **ConfigDSN** substituirá o nome existente. Se ele corresponder a um nome existente e *hwndParent* não for nulo, **ConfigDSN** solicitará que o usuário substitua o nome existente.  
  
 Se *lpszAttributes* contiver informações suficientes para se conectar a uma fonte de dados, o **ConfigDSN** poderá adicionar a fonte de dados ou exibir uma caixa de diálogo com a qual o usuário pode alterar as informações de conexão. Se *lpszAttributes* não contiver informações suficientes para se conectar a uma fonte de dados, **ConfigDSN** deverá determinar as informações necessárias; Se *hwndParent* não for NULL, ele exibirá uma caixa de diálogo para recuperar as informações do usuário.  
  
 Se **ConfigDSN** exibir uma caixa de diálogo, ele deverá exibir as informações de conexão passadas para ela em *lpszAttributes*. Em particular, se um nome de fonte de dados foi passado para ele, **ConfigDSN** exibirá esse nome, mas não permitirá que o usuário o altere. **ConfigDSN** pode fornecer valores padrão para informações de conexão não passadas para ele em *lpszAttributes*.  
  
 Se **ConfigDSN** não puder obter informações completas de conexão para uma fonte de dados, retornará false.  
  
 Se **ConfigDSN** puder obter informações completas de conexão para uma fonte de dados, ele chamará **SQLWriteDSNToIni** na DLL do instalador para adicionar a nova especificação de fonte de dados ao arquivo ODBC. ini (ou registro). **SQLWriteDSNToIni** adiciona o nome da fonte de dados à seção [fontes de dados ODBC], cria a seção especificação da fonte de dados e adiciona a palavra-chave do **Driver** com a descrição do driver como seu valor. **ConfigDSN** chama **SQLWritePrivateProfileString** na DLL do instalador para adicionar quaisquer palavras-chave e valores adicionais usados pelo driver.  
  
## <a name="modifying-a-data-source"></a>Modificando uma fonte de dados  
 Para modificar uma fonte de dados, um nome de fonte de dados deve ser passado para **ConfigDSN** em *lpszAttributes*. **ConfigDSN** verifica se o nome da fonte de dados está no arquivo ODBC. ini (ou registro).  
  
 Se *hwndParent* for nulo, **ConfigDSN** usará as informações em *lpszAttributes* para modificar as informações no arquivo ODBC. ini (ou registro). Se *hwndParent* não for NULL, **ConfigDSN** exibirá uma caixa de diálogo usando as informações em *lpszAttributes*; para informações que não estão no *lpszAttributes*, ele usa informações das informações do sistema. O usuário pode modificar as informações antes que **ConfigDSN** as armazene nas informações do sistema.  
  
 Se o nome da fonte de dados tiver sido alterado, **ConfigDSN** primeiro chamará **SQLRemoveDSNFromIni** na DLL do instalador para remover a especificação de fonte de dados existente do arquivo ODBC. ini (ou registro). Em seguida, ele segue as etapas na seção anterior para adicionar a nova especificação de fonte de dados. Se o nome da fonte de dados não tiver sido alterado, **ConfigDSN** chamará **SQLWritePrivateProfileString** na DLL do instalador para fazer outras alterações. **ConfigDSN** não pode excluir ou alterar o valor da palavra-chave do **Driver** .  
  
## <a name="deleting-a-data-source"></a>Excluindo uma fonte de dados  
 Para excluir uma fonte de dados, um nome de fonte de dados deve ser passado para **ConfigDSN** em *lpszAttributes*. **ConfigDSN** verifica se o nome da fonte de dados está no arquivo ODBC. ini (ou registro). Em seguida, ele chama **SQLRemoveDSNFromIni** na DLL do instalador para remover a fonte de dados.  
  
## <a name="note"></a>Observação
 Se estiver escrevendo uma versão Unicode dessa rotina, ela deverá ser chamada de **ConfigDSNW**, com argumentos LPCWSTR em vez de LPCSTR.
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo uma fonte de dados|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Obtendo um valor do arquivo ODBC. ini ou do registro|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|Removendo a fonte de dados padrão|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Removendo um nome de fonte de dados de ODBC. ini (ou registro)|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Adicionando um nome de fonte de dados a ODBC. ini (ou registro)|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|Gravando um valor no arquivo ODBC. ini ou no registro|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
