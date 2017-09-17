---
title: "Função SQLConfigDataSource | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1d1fddaf67cfbdb8f8c8df7e66b86a681ca2e23d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlconfigdatasource-function"></a>Função SQLConfigDataSource
**Conformidade**  
 Versão introduzidas: ODBC 1.0  
  
 **Resumo**  
 **SQLConfigDataSource** adiciona, modifica ou exclui as fontes de dados.  
  
 A funcionalidade de **SQLConfigDataSource** também podem ser acessados com [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLConfigDataSource(  
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
  
 ODBC_ADD_DSN: Adicione uma nova fonte de dados do usuário.  
  
 ODBC_CONFIG_DSN: Configurar (modificar) uma fonte de dados de usuário existente.  
  
 ODBC_REMOVE_DSN: Remova uma fonte de dados de usuário existente.  
  
 ODBC_ADD_SYS_DSN: Adicione uma nova fonte de dados do sistema.  
  
 ODBC_CONFIG_SYS_DSN: Modificar uma fonte de dados de sistema existente.  
  
 ODBC_REMOVE_SYS_DSN: Remova uma fonte de dados de sistema existente.  
  
 ODBC_REMOVE_DEFAULT_DSN: Remova a seção de especificação de fonte de dados padrão das informações do sistema. (Ele também remove a seção de especificação de driver padrão da entrada Odbcinst.ini nas informações do sistema. Isso *frequentes* executa a mesma função preterido **SQLRemoveDefaultDataSource** função.) Quando essa opção for especificada, todos os outros parâmetros na chamada para **SQLConfigDataSource** devem ser valores nulos; se não forem nulos, eles serão ignorados.  
  
 *lpszDriver*  
 [Entrada] Descrição do driver (geralmente o nome do DBMS associado) apresentada aos usuários em vez do nome físico do driver.  
  
 *lpszAttributes*  
 [Entrada] Uma lista de atributos na forma de pares de valor de palavra-chave duplamente terminada em nulo. Para obter mais informações, consulte [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar. Se não houver nenhuma entrada nas informações do sistema quando esta função é chamada, a função retornará FALSE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLConfigDataSource** retorna FALSE, um tipo de * \*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o * \*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O *hwndParent* argumento era nulo ou inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O *frequentes* argumento não era um dos seguintes:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou conversor inválido|O *lpszDriver* argumento era inválido. Ele não pôde ser encontrado no registro.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de valor de palavra-chave inválida|O *lpszAttributes* argumento continha um erro de sintaxe.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* falha|O instalador não foi possível executar a operação solicitada pelo *frequentes* argumento. A chamada para **ConfigDSN** falhou.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de instalação de driver ou conversor|Não foi possível carregar a biblioteca de instalação do driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido a uma falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLConfigDataSource** usa o valor de *lpszDriver* para ler o caminho completo da DLL de instalação para o driver das informações do sistema. Ele carrega a DLL e chamadas **ConfigDSN** com os mesmos argumentos foram passados para ele.  
  
 **SQLConfigDataSource** retornará FALSE se não for possível localizar ou carregar a DLL de configuração ou se o usuário cancelar a caixa de diálogo. Caso contrário, retornará o status recebido do **ConfigDSN**.  
  
 **SQLConfigDataSource** mapeia o DSN do sistema *frequentes*s para o DSN do usuário *frequentes*s (ODBC_ADD_SYS_DSN para ODBC_ADD_DSN, ODBC_CONFIG_SYS_DSN ODBC_CONFIG_DSN e ODBC_REMOVE_SYS _DSN para ODBC_REMOVE_DSN). Para distinguir os DSNs de sistema e usuário **SQLConfigDataSource** define o instalador do modo de configuração de acordo com a tabela a seguir. Antes de retornar, **SQLConfigDataSource** redefine o modo de configuração para BOTHDSN. **ConfigDSN** (implementado pelos drivers) deve chamar **SQLWriteDSNToIni** e **SQLWritePrivateProfileString** para dar suporte a um DSN de sistema. Para obter mais informações, consulte [ConfigDSN função](../../../odbc/reference/syntax/configdsn-function.md).  
  
|*Frequentes*|Modo de configuração|  
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
|Adicionar, modificar ou remover uma fonte de dados|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (na configuração de DLL)|  
|Remover um nome de fonte de dados das informações do sistema|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Adicionar um nome de fonte de dados para as informações do sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
