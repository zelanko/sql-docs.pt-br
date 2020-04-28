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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299626"
---
# <a name="sqlconfigdatasource-function"></a>Função SQLConfigDataSource
**Conformidade**  
 Versão introduzida: ODBC 1,0  
  
 **Resumo**  
 O **SQLConfigDataSource** adiciona, modifica ou exclui fontes de dados.  
  
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
 *hwndParent*  
 Entrada Identificador de janela pai. A função não exibirá nenhuma caixa de diálogo se o identificador for nulo.  
  
 *fRequest*  
 Entrada Tipo de solicitação. O argumento *fRequest* deve conter um dos seguintes valores:  
  
 ODBC_ADD_DSN: adicionar uma nova fonte de dados de usuário.  
  
 ODBC_CONFIG_DSN: configurar (modificar) uma fonte de dados de usuário existente.  
  
 ODBC_REMOVE_DSN: remover uma fonte de dados de usuário existente.  
  
 ODBC_ADD_SYS_DSN: adicionar uma nova fonte de dados do sistema.  
  
 ODBC_CONFIG_SYS_DSN: modificar uma fonte de dados do sistema existente.  
  
 ODBC_REMOVE_SYS_DSN: remover uma fonte de dados do sistema existente.  
  
 ODBC_REMOVE_DEFAULT_DSN: Remova a seção especificação de fonte de dados padrão das informações do sistema. (Ele também remove a seção de especificação de driver padrão da entrada Odbcinst. ini nas informações do sistema. Esse *fRequest* executa a mesma função que a função de **SQLRemoveDefaultDataSource** preterida.) Quando essa opção é especificada, todos os outros parâmetros na chamada para **SQLConfigDataSource** devem ser nulos; Se eles não forem nulos, eles serão ignorados.  
  
 *lpszDriver*  
 Entrada Descrição do driver (geralmente o nome do DBMS associado) apresentado aos usuários em vez do nome do driver físico.  
  
 *lpszAttributes*  
 Entrada Uma lista dupla de atributos terminada em nulo na forma de pares de palavra-chave-valor. Para obter mais informações, consulte [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar. Se não existir nenhuma entrada nas informações do sistema quando essa função for chamada, a função retornará FALSE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLConfigDataSource** retorna false, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O argumento *hwndParent* era inválido ou nulo.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O argumento *fRequest* não era um dos seguintes:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou tradutor inválido|O argumento *lpszDriver* era inválido. Ele não foi encontrado no registro.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de palavra-chave-valor inválidos|O argumento *lpszAttributes* continha um erro de sintaxe.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na *solicitação*|O instalador não pôde executar a operação solicitada pelo argumento *fRequest* . Falha na chamada para **ConfigDSN** .|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de instalação do driver ou do Tradutor|Não foi possível carregar a biblioteca de instalação do driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLConfigDataSource** usa o valor de *lpszDriver* para ler o caminho completo da DLL de instalação do driver a partir das informações do sistema. Ele carrega a DLL e chama **ConfigDSN** com os mesmos argumentos que foram passados para ele.  
  
 **SQLConfigDataSource** retornará false se não for possível localizar ou carregar a DLL de instalação ou se o usuário cancelar a caixa de diálogo. Caso contrário, ele retorna o status recebido de **ConfigDSN**.  
  
 O **SQLConfigDataSource** mapeia os *fRequest*do DSN do sistema para o DSN do usuário *fRequest*s (ODBC_ADD_SYS_DSN para ODBC_ADD_DSN, ODBC_CONFIG_SYS_DSN para ODBC_CONFIG_DSN e ODBC_REMOVE_SYS_DSN para ODBC_REMOVE_DSN). Para distinguir os DSNs do usuário e do sistema, o **SQLConfigDataSource** define o modo de configuração do instalador de acordo com a tabela a seguir. Antes de retornar, **SQLConfigDataSource** redefine o modo de configuração para BOTHDSN. **ConfigDSN** (implementados por drivers) devem chamar **SQLWriteDSNToIni** e **SQLWritePrivateProfileString** para dar suporte a um DSN do sistema. Para obter mais informações, consulte [função ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
|*fRequest*|Modo de configuração|  
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
|Adicionando, modificando ou removendo uma fonte de dados|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (na DLL de instalação)|  
|Removendo um nome de fonte de dados das informações do sistema|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Adicionando um nome de fonte de dados às informações do sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
