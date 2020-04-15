---
title: Função SQLConfigDataSource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConfigDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDataSource
helpviewer_keywords:
- SQLConfigDataSource function [ODBC]
ms.assetid: f8d6e342-c010-434e-b1cd-f5371fb50a14
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90a51193a8f4edbb013527c4dde0625b75131583
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299626"
---
# <a name="sqlconfigdatasource-function"></a>Função SQLConfigDataSource
**Conformidade**  
 Versão introduzida: ODBC 1.0  
  
 **Resumo**  
 **SQLConfigDataSource** adiciona, modifica ou exclui fontes de dados.  
  
 A funcionalidade do **SQLConfigDataSource** também pode ser acessada com [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLConfigDataSource(  
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
  
 ODBC_ADD_DSN: Adicione uma nova fonte de dados do usuário.  
  
 ODBC_CONFIG_DSN: Configure (modificar) uma fonte de dados existente do usuário.  
  
 ODBC_REMOVE_DSN: Remova uma fonte de dados do usuário existente.  
  
 ODBC_ADD_SYS_DSN: Adicione uma nova fonte de dados do sistema.  
  
 ODBC_CONFIG_SYS_DSN: Modifique uma fonte de dados do sistema existente.  
  
 ODBC_REMOVE_SYS_DSN: Remova uma fonte de dados do sistema existente.  
  
 ODBC_REMOVE_DEFAULT_DSN: Remova a seção de especificação de origem de dados padrão das informações do sistema. (Também remove a seção de especificação padrão do driver da entrada Odbcinst.ini nas informações do sistema. Este *fRequest* executa a mesma função que a função **depreciada SQLRemoveDefaultDataSource.)** Quando essa opção for especificada, todos os outros parâmetros da chamada para **SQLConfigDataSource** devem ser NULLs; se eles não são NULOS, eles serão ignorados.  
  
 *Lpszdriver*  
 [Entrada] Descrição do driver (geralmente o nome do DBMS associado) apresentado aos usuários em vez do nome do motorista físico.  
  
 *Lpszattributes*  
 [Entrada] Uma lista duplamente nula de atributos na forma de pares de valor escancarando palavras-chave. Para obter mais informações, consulte [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar. Se não houver entrada nas informações do sistema quando essa função for chamada, a função retorna FALSA.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLConfigDataSource** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_INVALID_HWND|Alça de janela inválida|O argumento *hwndParent* era inválido ou NULO.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválida|O argumento *fRequest* não foi um dos seguintes:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|Nome de motorista ou tradutor inválido|O argumento *lpszDriver* era inválido. Não foi possível encontrar no registro.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de valores de palavras-chave inválidos|O argumento *lpszAttributes* continha um erro de sintaxe.|  
|ODBC_ERROR_REQUEST_FAILED|*Falha na solicitação*|O instalador não pôde realizar a operação solicitada pelo argumento *fRequest.* A chamada para **configDSN** falhou.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de configuração do driver ou tradutor|A biblioteca de configuração do driver não pôde ser carregada.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLConfigDataSource** usa o valor do *lpszDriver* para ler o caminho completo da configuração DLL para o driver a partir das informações do sistema. Ele carrega o DLL e chama **ConfigDSN** com os mesmos argumentos que foram passados para ele.  
  
 **SQLConfigDataSource** retorna FALSA se não conseguir encontrar ou carregar a Configuração DLL ou se o usuário cancelar a caixa de diálogo. Caso contrário, ele retorna o status que recebeu do **ConfigDSN**.  
  
 **SQLConfigDataSource** mapeia o sistema DSN *fRequest*s para o Usuário DSN *fRequest*s (ODBC_ADD_SYS_DSN para ODBC_ADD_DSN, ODBC_CONFIG_SYS_DSN para ODBC_CONFIG_DSN e ODBC_REMOVE_SYS_DSN para ODBC_REMOVE_DSN). Para distinguir dSNs do usuário e do sistema, **o SQLConfigDataSource** define o modo de configuração do instalador de acordo com a tabela a seguir. Antes de retornar, **SQLConfigDataSource** redefine o modo de configuração para BOTHDSN. **O ConfigDSN** (implementado pelos drivers) deve chamar **SQLWriteDSNToIni** e **SQLWritePrivateProfileString** para suportar um DSN do sistema. Para obter mais informações, consulte [Função ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
|*fSolicitar*|Modo de configuração|  
|----------------|------------------------|  
|ODBC_ADD_DSN|USERDSN_ONLY|  
|ODBC_CONFIG_DSN|USERDSN_ONLY|  
|ODBC_REMOVE_DSN|USERDSN_ONLY|  
|ODBC_ADD_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_CONFIG_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_REMOVE_SYS_DSN|SYSTEMDSN_ONLY|  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo uma fonte de dados|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (na configuração DLL)|  
|Removendo um nome de origem de dados das informações do sistema|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Adicionando um nome de origem de dados às informações do sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
