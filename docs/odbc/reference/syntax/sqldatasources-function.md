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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301176"
---
# <a name="sqldatasources-function"></a>Função SQLDataSources
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLDataSources** retorna informações sobre uma fonte de dados. Esta função é implementada apenas pelo Driver Manager.  
  
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
 [Entrada] Alça do meio ambiente.  
  
 *Direção*  
 [Entrada] Determina sobre qual fonte de dados o Driver Manager retorna informações. Pode ser:  
  
 SQL_FETCH_NEXT (buscar o próximo nome de origem dos dados na lista), SQL_FETCH_FIRST (buscar desde o início da lista), SQL_FETCH_FIRST_USER (buscar o primeiro DSN do usuário) ou SQL_FETCH_FIRST_SYSTEM (buscar o primeiro DSN do sistema).  
  
 Quando *o Direction* é definido para SQL_FETCH_FIRST, chamadas subseqüentes para **SQLDataSources** com *Direção* definidas para SQL_FETCH_NEXT retornar dSNs do usuário e do sistema. Quando *o Direction* é definido como SQL_FETCH_FIRST_USER, todas as chamadas subseqüentes para **SQLDataSources** com *Direção* definidas para SQL_FETCH_NEXT retornar apenas DSNs do usuário. Quando *o Direction* é definido como SQL_FETCH_FIRST_SYSTEM, todas as chamadas subseqüentes para **SQLDataSources** com *Direção* definidas para SQL_FETCH_NEXT retornar apenas DSNs do sistema.  
  
 *Servername*  
 [Saída] Ponteiro para um buffer no qual retornar o nome de origem dos dados.  
  
 Se *ServerName* for NULL, *NameLength1Ptr* ainda retornará o número total de caracteres (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado pelo *ServerName*.  
  
 *Comprimento do buffer1*  
 [Entrada] Comprimento do buffer ** ServerName,* em caracteres; isso não precisa ser maior do que SQL_MAX_DSN_LENGTH mais o caractere de rescisão nula.  
  
 *NameLength1Ptr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo o caractere de rescisão nula) disponível para retornar em \* *ServerName*. Se o número de caracteres disponíveis para retornar for maior ou \*igual a *BufferLength1,* o nome de origem dos dados no *ServerName* será truncado para *BufferLength1* menos o comprimento de um caractere de rescisão nula.  
  
 *Descrição*  
 [Saída] Ponteiro para um buffer no qual retornar a descrição do driver associado à fonte de dados. Por exemplo, dBASE ou SQL Server.  
  
 Se *a descrição* for NULA, *NameLength2Ptr* ainda retornará o número total de caracteres (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado para *Description*.  
  
 *Comprimento do buffer2*  
 [Entrada] Comprimento em caracteres do tampão ** Descrição.*  
  
 *NameLength2Ptr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo o caractere de rescisão nula) disponível para retornar em \* *Descrição*. Se o número de caracteres disponíveis para retornar for maior ou \*igual a *BufferLength2,* a descrição do driver em *Descrição* será truncada para *BufferLength2* menos o comprimento de um caractere de rescisão nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLDataSources** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **sqlGetDiagRec** com um *HandleType* de SQL_HANDLE_ENV e uma *alça* de *EnvironmentHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLDataSources** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|(DM) Mensagem informacional específica do Driver Manager. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|(DM) O \*buffer *ServerName* não era grande o suficiente para retornar o nome de origem completa dos dados. Portanto, o nome foi truncado. O comprimento de todo o nome \*de origem dos dados é retornado em *NameLength1Ptr*. (Função retorna SQL_SUCCESS_WITH_INFO.)<br /><br /> (DM) A \* *descrição* do buffer não era grande o suficiente para retornar a descrição completa do driver. Portanto, a descrição foi truncada. O comprimento da descrição da fonte de dados não truncada é retornado em **NameLength2Ptr*. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|(DM) Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|(DM) O Driver Manager não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função.|  
|HY010|Erro de seqüência de função|(DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor especificado para o argumento *BufferLength1* foi inferior a 0.<br /><br /> (DM) O valor especificado para o argumento *BufferLength2* foi inferior a 0.|  
|HY103|Código de recuperação inválido|(DM) O valor especificado para o argumento *Direção* não era igual a SQL_FETCH_FIRST, SQL_FETCH_FIRST_USER, SQL_FETCH_FIRST_SYSTEM ou SQL_FETCH_NEXT.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
  
## <a name="comments"></a>Comentários  
 Como o **SQLDataSources** é implementado no Driver Manager, ele é suportado para todos os drivers, independentemente da conformidade com os padrões de um determinado driver.  
  
 Um aplicativo pode chamar **SQLDataSources** várias vezes para recuperar todos os nomes de origem dos dados. O Driver Manager recupera essas informações das informações do sistema. Quando não há mais nomes de origem de dados, o Driver Manager retorna SQL_NO_DATA. Se **o SQLDataSources** for chamado de SQL_FETCH_NEXT imediatamente após o retorno SQL_NO_DATA, ele retornará o primeiro nome de origem dos dados. Para obter informações sobre como um aplicativo usa as informações retornadas pelo **SQLDataSources,** consulte [Escolhendo uma Fonte de Dados ou Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Se SQL_FETCH_NEXT for passado para **SQLDataSources** na primeira vez que for chamado, ele retornará o primeiro nome de origem dos dados.  
  
 O driver determina como os nomes da fonte de dados são mapeados para fontes de dados reais.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Descobrir e listar valores necessários para se conectar a uma fonte de dados|[Função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Conectando-se a uma fonte de dados|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Conectando-se a uma fonte de dados usando uma seqüência de conexão ou caixa de diálogo|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Retornando descrições e atributos do driver|[Função SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
