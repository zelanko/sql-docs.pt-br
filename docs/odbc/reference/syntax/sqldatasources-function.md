---
title: Função SQLDataSources | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDataSources
helpviewer_keywords:
- SQLDataSources function [ODBC]
ms.assetid: 3f63b1b4-e70e-44cd-96c6-6878d50d0117
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b56a6c25e54897e67beaf39d3b7797ac45391d7b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301176"
---
# <a name="sqldatasources-function"></a>Função SQLDataSources
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLDataSources** retorna informações sobre uma fonte de dados. Essa função é implementada somente pelo Gerenciador de driver.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLDataSources(  
     SQLHENV          EnvironmentHandle,  
     SQLUSMALLINT     Direction,  
     SQLCHAR *        ServerName,  
     SQLSMALLINT      BufferLength1,  
     SQLSMALLINT *    NameLength1Ptr,  
     SQLCHAR *        Description,  
     SQLSMALLINT      BufferLength2,  
     SQLSMALLINT *    NameLength2Ptr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 Entrada Identificador de ambiente.  
  
 *Direção*  
 Entrada Determina a fonte de dados sobre a qual o Gerenciador de driver retorna informações. Pode ser:  
  
 SQL_FETCH_NEXT (para buscar o próximo nome da fonte de dados na lista), SQL_FETCH_FIRST (para buscar desde o início da lista), SQL_FETCH_FIRST_USER (para buscar o primeiro DSN do usuário) ou SQL_FETCH_FIRST_SYSTEM (para buscar o primeiro DSN do sistema).  
  
 Quando a *direção* é definida como SQL_FETCH_FIRST, as chamadas subsequentes para **SQLDataSources** com *Direction* definido como SQL_FETCH_NEXT retornam os DSNs do usuário e do sistema. Quando a *direção* é definida como SQL_FETCH_FIRST_USER, todas as chamadas subsequentes para **SQLDataSources** com *Direction* definido como SQL_FETCH_NEXT retornam somente DSNs do usuário. Quando a *direção* é definida como SQL_FETCH_FIRST_SYSTEM, todas as chamadas subsequentes para **SQLDataSources** com *Direction* definido como SQL_FETCH_NEXT retornam somente DSNs do sistema.  
  
 *ServerName*  
 Der Ponteiro para um buffer no qual retornar o nome da fonte de dados.  
  
 Se *ServerName* for NULL, *NameLength1Ptr* ainda retornará o número total de caracteres (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado pelo *ServerName*.  
  
 *BufferLength1*  
 Entrada Comprimento do buffer **ServerName* , em caracteres; Isso não precisa ser maior que SQL_MAX_DSN_LENGTH mais o caractere de terminação nula.  
  
 *NameLength1Ptr*  
 Der Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo o caractere de terminação nula) disponível para retornar \*no *ServerName*. Se o número de caracteres disponíveis para retornar for maior ou igual a *BufferLength1*, o nome da fonte de dados \*no *ServerName* será truncado para *BufferLength1* menos o comprimento de um caractere de terminação nula.  
  
 *Descrição*  
 Der Ponteiro para um buffer no qual retornar a descrição do driver associado à fonte de dados. Por exemplo, dBASE ou SQL Server.  
  
 Se *Description* for NULL, *NameLength2Ptr* ainda retornará o número total de caracteres (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *Descrição*.  
  
 *BufferLength2*  
 Entrada Comprimento em caracteres do buffer de*Descrição* *.  
  
 *NameLength2Ptr*  
 Der Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo o caractere de terminação nula) disponível para retornar \*na *Descrição*. Se o número de caracteres disponíveis para retornar for maior ou igual a *BufferLength2*, a descrição do driver em \* *Descrição* será truncada para *BufferLength2* menos o comprimento de um caractere de terminação nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLDataSources** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_ENV e um *identificador* de *EnvironmentHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLDataSources** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|(DM) Gerenciador de driver-mensagem informativa específica. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|(DM) o buffer \* *ServerName* não era grande o suficiente para retornar o nome de fonte de dados completo. Portanto, o nome foi truncado. O comprimento de todo o nome da fonte de dados é \*retornado em *NameLength1Ptr*. (A função retorna SQL_SUCCESS_WITH_INFO.)<br /><br /> (DM) a \* *Descrição* do buffer não era grande o suficiente para retornar a descrição completa do driver. Portanto, a descrição foi truncada. O comprimento da descrição da fonte de dados não truncada é retornado em **NameLength2Ptr*. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|(DM) ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|(DM) o Gerenciador de driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|(DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor especificado para o argumento *BufferLength1* era menor que 0.<br /><br /> (DM) o valor especificado para o argumento *BufferLength2* era menor que 0.|  
|HY103|Código de recuperação inválido|(DM) o valor especificado para a *direção* do argumento não era igual a SQL_FETCH_FIRST, SQL_FETCH_FIRST_USER, SQL_FETCH_FIRST_SYSTEM ou SQL_FETCH_NEXT.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
  
## <a name="comments"></a>Comentários  
 Como o **SQLDataSources** é implementado no Gerenciador de driver, ele tem suporte para todos os drivers, independentemente da conformidade com os padrões de um driver específico.  
  
 Um aplicativo pode chamar **SqlDataSource** várias vezes para recuperar todos os nomes de fonte de dados. O Gerenciador de driver recupera essas informações das informações do sistema. Quando não há mais nomes de fonte de dados, o Gerenciador de driver retorna SQL_NO_DATA. Se **SQLDataSources** for chamado com SQL_FETCH_NEXT imediatamente depois que ele retornar SQL_NO_DATA, ele retornará o primeiro nome da fonte de dados. Para obter informações sobre como um aplicativo usa as informações retornadas por **SQLDataSources**, consulte [escolhendo uma fonte de dados ou um driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Se SQL_FETCH_NEXT for passado para **SQLDataSources** na primeira vez que for chamado, ele retornará o primeiro nome da fonte de dados.  
  
 O driver determina como os nomes de fonte de dados são mapeados para as fontes de dados reais.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Descobrindo e listando os valores necessários para se conectar a uma fonte de dados|[Função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Conectando-se a uma fonte de dados|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Conectando-se a uma fonte de dados usando uma cadeia de conexão ou caixa de diálogo|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Retornando descrições e atributos de driver|[Função SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
