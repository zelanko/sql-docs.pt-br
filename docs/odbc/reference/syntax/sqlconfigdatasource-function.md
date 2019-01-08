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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ef74d98102c424a71ac1728d664fddbeac2296c
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53215595"
---
# <a name="sqlconfigdatasource-function"></a>Função SQLConfigDataSource
**Conformidade com**  
 Versão introduzida: ODBC 1.0  
  
 **Resumo**  
 **SQLConfigDataSource** adiciona, modifica ou exclui as fontes de dados.  
  
 A funcionalidade do **SQLConfigDataSource** também podem ser acessados com [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
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
 [Entrada] Identificador de janela pai. A função não exibirá nenhuma caixa de diálogo se o identificador for nulo.  
  
 *Frequentes*  
 [Entrada] Tipo de solicitação. O *frequentes* argumento deve conter um dos seguintes valores:  
  
 ODBC_ADD_DSN: Adicione uma nova fonte de dados do usuário.  
  
 ODBC_CONFIG_DSN: Configurar (modificar) uma fonte de dados de usuário existente.  
  
 ODBC_REMOVE_DSN: Remova uma fonte de dados de usuário existente.  
  
 ODBC_ADD_SYS_DSN: Adicione uma nova fonte de dados do sistema.  
  
 ODBC_CONFIG_SYS_DSN: Modificar uma fonte de dados do sistema existente.  
  
 ODBC_REMOVE_SYS_DSN: Remova uma fonte de dados do sistema existente.  
  
 ODBC_REMOVE_DEFAULT_DSN: Remova a seção de especificação de fonte de dados padrão de informações do sistema. (Ela também remove a seção de especificação de driver padrão da entrada Odbcinst. ini nas informações do sistema. Isso *frequentes* executa a mesma função como preteridas **SQLRemoveDefaultDataSource** função.) Quando essa opção for especificada, todos os outros parâmetros na chamada para **SQLConfigDataSource** devem ser valores nulos; se não forem nulos, eles serão ignorados.  
  
 *lpszDriver*  
 [Entrada] Descrição do driver (geralmente o nome do DBMS associado) apresentada aos usuários em vez do nome físico de driver.  
  
 *lpszAttributes*  
 [Entrada] Uma lista duplamente terminada em nulo de atributos na forma de pares de palavra-chave-valor. Para obter mais informações, consulte [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar. Se não houver nenhuma entrada nas informações do sistema quando essa função é chamada, a função retorna FALSE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLConfigDataSource** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_HWND|Identificador de janela inválido|O *hwndParent* argumento era inválido ou nulo.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O *frequentes* argumento não era um dos seguintes:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|Nome inválido de driver ou conversor|O *lpszDriver* argumento era inválido. Ele não pôde ser encontrado no registro.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de valor de palavra-chave inválido|O *lpszAttributes* argumento continha um erro de sintaxe.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* falhou|O instalador não foi possível executar a operação solicitada pelo *frequentes* argumento. A chamada para **ConfigDSN** falhou.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Não foi possível carregar a biblioteca de instalação do driver ou conversor|Não foi possível carregar a biblioteca de instalação do driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLConfigDataSource** usa o valor da *lpszDriver* para ler o caminho completo da instalação do DLL para o driver a partir das informações do sistema. Ele carrega a DLL e chama **ConfigDSN** com os mesmos argumentos foram passados para ele.  
  
 **SQLConfigDataSource** retorna FALSE se não for possível localizar ou carregar a DLL de instalação ou se o usuário cancelar a caixa de diálogo. Caso contrário, retornará o status recebido do **ConfigDSN**.  
  
 **SQLConfigDataSource** mapeia o DSN do sistema *frequentes*s para o DSN de usuário *frequentes*s (ODBC_ADD_SYS_DSN para ODBC_ADD_DSN, ODBC_CONFIG_SYS_DSN ODBC_CONFIG_DSN e ODBC_REMOVE_SYS_ DSN para ODBC_REMOVE_DSN). Para distinguir os DSNs de sistema e de usuário **SQLConfigDataSource** define o instalador do modo de configuração de acordo com a tabela a seguir. Antes de retornar, **SQLConfigDataSource** redefine o modo de configuração para BOTHDSN. **ConfigDSN** (implementado pelos drivers) deve chamar **SQLWriteDSNToIni** e **SQLWritePrivateProfileString** para dar suporte a um DSN de sistema. Para obter mais informações, consulte [função ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
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
|Removendo um nome de fonte de dados de informações do sistema|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Adicionando um nome de fonte de dados para as informações do sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
