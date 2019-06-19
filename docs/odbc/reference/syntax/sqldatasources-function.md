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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9207dde54a14e345e99d3c04d4cb66622d85972e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537634"
---
# <a name="sqldatasources-function"></a>Função SQLDataSources
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLDataSources** retorna informações sobre uma fonte de dados. Essa função é implementada somente pelo Gerenciador de Driver.  
  
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
 [Entrada] Identificador de ambiente.  
  
 *Direção*  
 [Entrada] Determina qual fonte de dados, o Gerenciador de Driver retorna informações sobre. Pode ser:  
  
 SQL_FETCH_NEXT (para buscar o próximo nome de fonte de dados na lista), SQL_FETCH_FIRST (para buscar desde o início da lista), SQL_FETCH_FIRST_USER (para o DSN de usuário de busca o primeiro) ou SQL_FETCH_FIRST_SYSTEM (para buscar o DSN do sistema primeiro).  
  
 Quando *direção* é definido como SQL_FETCH_FIRST, chamadas subsequentes para **SQLDataSources** com *direção* definido como SQL_FETCH_NEXT retornar os DSNs do sistema e usuário. Quando *direção* é definido como SQL_FETCH_FIRST_USER, todas as chamadas subsequentes para **SQLDataSources** com *direção* definido como SQL_FETCH_NEXT retornar os DSNs do usuário. Quando *direção* é definido como SQL_FETCH_FIRST_SYSTEM, todas as chamadas subsequentes para **SQLDataSources** com *direção* definido como SQL_FETCH_NEXT retornar apenas DSNs do sistema.  
  
 *ServerName*  
 [Saída] Ponteiro para um buffer no qual retornar o nome da fonte de dados.  
  
 Se *nome_do_servidor* for NULL, *NameLength1Ptr* ainda retornará o número total de caracteres (exceto o caractere nulo de terminação para dados de caracteres) disponíveis para retornar no buffer apontado por *Nome_do_servidor*.  
  
 *BufferLength1*  
 [Entrada] Comprimento do **ServerName* buffer em caracteres; isso não precisa ser maior do que SQL_MAX_DSN_LENGTH mais o caractere de finalização null.  
  
 *NameLength1Ptr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (exceto o caractere nulo de terminação) disponíveis para retornar na \* *ServerName*. Se o número de caracteres disponíveis para retornar for maior que ou igual a *BufferLength1*, o nome da fonte de dados no \* *ServerName* será truncado para *BufferLength1* menos o comprimento de um caractere nulo de terminação.  
  
 *Descrição*  
 [Saída] Ponteiro para um buffer no qual retornar a descrição do driver associado com a fonte de dados. Por exemplo, dBASE ou SQL Server.  
  
 Se *descrição* for NULL, *NameLength2Ptr* ainda retornará o número total de caracteres (exceto o caractere nulo de terminação para dados de caracteres) disponíveis para retornar no buffer apontado por *Descrição*.  
  
 *BufferLength2*  
 [Entrada] Comprimento em caracteres da **descrição* buffer.  
  
 *NameLength2Ptr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (exceto o caractere nulo de terminação) disponíveis para retornar na \* *descrição*. Se o número de caracteres disponíveis para retornar for maior que ou igual a *BufferLength2*, a descrição do driver na \* *descrição* será truncado para *BufferLength2*  menos o comprimento de um caractere nulo de terminação.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLDataSources** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType*SQL_HANDLE_ENV e uma *manipular* dos *EnvironmentHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLDataSources** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|(DM) mensagem informativa do Gerenciador de Driver específico. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|(DM) buffer \* *ServerName* não era grande o suficiente para retornar o nome de fonte de dados completos. Portanto, o nome foi truncado. O tamanho da fonte de dados inteira será retornado no \* *NameLength1Ptr*. (A função retornará SQL_SUCCESS_WITH_INFO.)<br /><br /> (DM) buffer \* *descrição* não era grande o suficiente para retornar a descrição completa do driver. Portanto, a descrição foi truncada. O comprimento da descrição da fonte de dados completo é retornado no **NameLength2Ptr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|(DM) Ocorreu um erro para o qual não havia nenhum SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O Gerenciador de Driver (DM) não pôde alocar memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor especificado para o argumento *BufferLength1* foi menor que 0.<br /><br /> (DM) o valor especificado para o argumento *BufferLength2* foi menor que 0.|  
|HY103|Código de recuperação inválido|(DM) o valor especificado para o argumento *direção* não era igual a SQL_FETCH_FIRST, SQL_FETCH_FIRST_USER, SQL_FETCH_FIRST_SYSTEM ou SQL_FETCH_NEXT.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
  
## <a name="comments"></a>Comentários  
 Porque **SQLDataSources** é implementado no Gerenciador de Driver, há suporte para todos os drivers, independentemente da conformidade com padrões de um driver específico.  
  
 Um aplicativo pode chamar **SQLDataSources** várias vezes para recuperar todos os nomes de fonte de dados. O Gerenciador de Driver recupera essas informações de informações do sistema. Quando não houver nenhum mais nomes de fonte de dados, o Gerenciador de Driver retorne SQL_NO_DATA. Se **SQLDataSources** é chamado com SQL_FETCH_NEXT imediatamente depois que ele retornar SQL_NO_DATA, ele retornará o primeiro nome de fonte de dados. Para obter informações sobre como um aplicativo usa as informações retornadas por **SQLDataSources**, consulte [escolhendo uma fonte de dados ou Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Se SQL_FETCH_NEXT é passado para **SQLDataSources** a primeira vez que ele é chamado, ele retornará o primeiro nome de fonte de dados.  
  
 O driver determina como nomes de fonte de dados são mapeados para as fontes de dados reais.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Descobrindo e listando os valores necessários para se conectar a uma fonte de dados|[Função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Conectando-se a uma fonte de dados|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Conectando a uma fonte de dados usando uma caixa de diálogo ou de cadeia de caracteres de conexão|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Retornando atributos e descrições de driver|[Função SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
