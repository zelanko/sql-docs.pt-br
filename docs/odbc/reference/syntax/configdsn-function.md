---
title: Função ConfigdSN | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fbae126c819088bd277621b207454503a86c8955
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306037"
---
# <a name="configdsn-function"></a>Função ConfigDSN
**Conformidade**  
 Versão introduzida: ODBC 1.0  
  
 **Resumo**  
 **O ConfigDSN** adiciona, modifica ou exclui fontes de dados das informações do sistema. Ele pode solicitar ao usuário informações de conexão. Pode estar no driver DLL ou em uma configuração separada DLL.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL ConfigDSN(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hwndparent*  
 [Entrada] Alça da janela dos pais. A função não exibirá nenhuma caixa de diálogo se a alça estiver nula.  
  
 *fSolicitar*  
 [Entrada] Tipo de pedido. O *argumento fRequest* deve conter um dos seguintes valores:  
  
 ODBC_ADD_DSN: Adicione uma nova fonte de dados.  
  
 ODBC_CONFIG_DSN: Configure (modificar) uma fonte de dados existente.  
  
 ODBC_REMOVE_DSN: Remova uma fonte de dados existente.  
  
 *Lpszdriver*  
 [Entrada] Descrição do driver (geralmente o nome do DBMS associado) apresentado aos usuários em vez do nome do motorista físico.  
  
 *Lpszattributes*  
 [Entrada] Uma lista duplamente nula de atributos na forma de pares de valor escancarando palavras-chave. Para obter mais informações, consulte "Comentários".  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o ConfigDSN** retorna FALSE, um valor * \*pfErrorCode* associado é postado no buffer de erro do instalador por uma chamada para **SQLPostInstallerError** e pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Alça de janela inválida|O argumento *hwndParent* era inválido.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de valores de palavras-chave inválidos|O argumento *lpszAttributes* continha um erro de sintaxe.|  
|ODBC_ERROR_INVALID_NAME|Nome de motorista ou tradutor inválido|O argumento *lpszDriver* era inválido. Não foi possível encontrar no registro.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválida|O argumento *fRequest* não foi um dos seguintes:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*Falha na solicitação*|Não foi possível realizar a operação solicitada pelo argumento *fRequest.*|  
|ODBC_ERROR_DRIVER_SPECIFIC|Erro específico do driver ou tradutor|Um erro específico do driver para o qual não há um erro de instalador ODBC definido. O argumento *SzError* em uma chamada para a função **SQLPostInstallerError** deve conter a mensagem de erro específica do driver.|  
  
## <a name="comments"></a>Comentários  
 **O ConfigDSN** recebe informações de conexão do instalador DLL como uma lista de atributos na forma de pares de valor de palavras-chave. Cada par é encerrado com um byte nulo, e toda a lista é encerrada com um byte nulo. (Ou seja, dois bytes nulos marcam o fim da lista.) Os espaços não são permitidos em torno do sinal igual no par de valor de palavra-chave. **O ConfigDSN** pode aceitar palavras-chave que não sejam palavras-chave válidas para **SQLBrowseConnect** e **SQLDriverConnect**. **O ConfigDSN** não suporta necessariamente todas as palavras-chave válidas para **SQLBrowseConnect** e **SQLDriverConnect**. (**ConfigDSN** não aceita a palavra-chave **DRIVER.)** As palavras-chave usadas pela função **ConfigDSN** devem suportar todas as opções necessárias para recriar a fonte de dados usando o recurso de configuração AUTO do instalador. Quando os usos dos valores **ConfigDSN** e os valores da seqüência de seqüência de conexão são os mesmos, as mesmas palavras-chave devem ser usadas.  
  
 Como em **SQLBrowseConnect** e **SQLDriverConnect,** as palavras-chave e seus valores não devem conter o **[];?{} \*=!@** caracteres, e o valor da palavra-chave **DSN** não pode consistir apenas em espaços em branco. Devido à gramática do registro, palavras-chave e nomes\\de fonte de dados não podem conter o caractere barra invertida ( ).  
  
 **O ConfigDSN** deve ligar para **o SQLValidDSN** para verificar o comprimento do nome da fonte de dados e verificar se nenhum caractere inválido está incluído no nome. Se o nome de origem dos dados for maior do que SQL_MAX_DSN_LENGTH ou incluir caracteres inválidos, **o SQLValidDSN** reameterá um erro e **o ConfigDSN** retorna um erro. O comprimento do nome de origem dos dados também é verificado por **SQLWriteDSNToIni**.  
  
 Por exemplo, para configurar uma fonte de dados que exija um ID do usuário, senha e nome do banco de dados, um aplicativo de configuração pode passar os seguintes pares de valor de palavra-chave:  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 Para obter mais informações sobre essas palavras-chave, consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) e a documentação de cada driver.  
  
 Para exibir uma caixa de diálogo, *hwndParent* não deve ser nulo.  
  
## <a name="adding-a-data-source"></a>Adicionando uma fonte de dados  
 Se um nome de origem de dados for passado para **ConfigDSN** em *lpszAttributes,* **configDSN** verificará se o nome é válido. Se o nome da fonte de dados corresponder a um nome de origem de dados existente e *hwndParent* for nulo, **o ConfigDSN** substitui o nome existente. Se corresponder a um nome existente e *hwndParent* não for nulo, **o ConfigDSN** solicitará ao usuário que sobreescreva o nome existente.  
  
 Se *lpszAttributes* contiver informações suficientes para se conectar a uma fonte de dados, o **ConfigDSN** poderá adicionar a fonte de dados ou exibir uma caixa de diálogo com a qual o usuário pode alterar as informações de conexão. Se *os lpszAttributes* não contiverem informações suficientes para se conectar a uma fonte de dados, **o ConfigDSN** deve determinar as informações necessárias; se *hwndParent* não for nulo, ele exibirá uma caixa de diálogo para recuperar as informações do usuário.  
  
 Se **o ConfigDSN** exibir uma caixa de diálogo, ele deve exibir qualquer informação de conexão passada a ela em *lpszAttributes*. Em particular, se um nome de origem de dados foi passado para ele, **o ConfigDSN** exibirá esse nome, mas não permite que o usuário o altere. **O ConfigDSN** pode fornecer valores padrão para informações de conexão não passadas a ele em *lpszAttributes*.  
  
 Se **o ConfigDSN** não conseguir obter informações completas de conexão para uma fonte de dados, ele retorna FALSO.  
  
 Se **o ConfigDSN** conseguir obter informações completas de conexão para uma fonte de dados, ele chamará **SQLWriteDSNToIni** no instalador DLL para adicionar a nova especificação de origem de dados ao arquivo Odbc.ini (ou registro). **SQLWriteDSNToIni** adiciona o nome de origem dos dados à seção [Fontes de dados oDBC], cria a seção de especificação de origem de dados e adiciona a palavra-chave **DRIVER** com a descrição do driver como seu valor. **ConfigDSN** chama **SQLWritePrivateProfileString** no instalador DLL para adicionar quaisquer palavras-chave adicionais e valores usados pelo driver.  
  
## <a name="modifying-a-data-source"></a>Modificando uma fonte de dados  
 Para modificar uma fonte de dados, um nome de origem de dados deve ser passado para **ConfigDSN** em *lpszAttributes*. **ConfigDSN** verifica se o nome de origem dos dados está no arquivo Odbc.ini (ou registro).  
  
 Se *hwndParent* for nulo, o **ConfigDSN** usará as informações em *lpszAttributes* para modificar as informações no arquivo Odbc.ini (ou registro). Se *hwndParent* não for nulo, **o ConfigDSN** exibirá uma caixa de diálogo usando as informações em *lpszAttributes*; para informações que não estão em *lpszAttributes,* ele usa informações das informações do sistema. O usuário pode modificar as informações antes **que o ConfigDSN** as atenha nas informações do sistema.  
  
 Se o nome de origem dos dados foi alterado, **o ConfigDSN** primeiro chamará **SQLRemoveDSNFromIni** no instalador DLL para remover a especificação de origem de dados existente do arquivo Odbc.ini (ou registro). Em seguida, segue as etapas da seção anterior para adicionar a nova especificação de origem de dados. Se o nome da fonte de dados não foi alterado, **o ConfigDSN** chamará **o SQLWritePrivateProfileString** no instalador DLL para fazer quaisquer outras alterações. **O ConfigDSN** não pode excluir ou alterar o valor da **palavra-chave Driver.**  
  
## <a name="deleting-a-data-source"></a>Excluindo uma fonte de dados  
 Para excluir uma fonte de dados, um nome de origem de dados deve ser passado para **ConfigDSN** em *lpszAttributes*. **ConfigDSN** verifica se o nome de origem dos dados está no arquivo Odbc.ini (ou registro). Em seguida, ele chama **SQLRemoveDSNFromIni** no instalador DLL para remover a fonte de dados.  
  
## <a name="note"></a>Observação
 Se escrever uma versão Unicode dessa rotina, ela deve ser chamada **de ConfigDSNW**, com argumentos LPCWSTR em vez de LPCSTR.
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo uma fonte de dados|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Obtendo um valor do arquivo Odbc.ini ou do registro|[SqlGetPrivateProfilestring](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|Removendo a fonte de dados padrão|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Removendo um nome de origem de dados do Odbc.ini (ou registro)|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Adicionando um nome de origem de dados ao Odbc.ini (ou registro)|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|Escrevendo um valor para o arquivo Odbc.ini ou para o registro|[SQLWritePrivateProfilestring](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
