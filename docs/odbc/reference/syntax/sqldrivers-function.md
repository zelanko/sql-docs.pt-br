---
title: Função sqldrives | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDrivers
helpviewer_keywords:
- SQLDrivers function [ODBC]
ms.assetid: 6b5b7514-e9cb-4cfd-8b7a-ab51dfab9efa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f54be3d11f4870533513f464c1afdae13e04f367
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104660"
---
# <a name="sqldrivers-function"></a>Função SQLDrivers
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 2,0: ODBC  
  
 **Resumo**  
 **Sqldriveres** lista descrições de driver e palavras-chave de atributo de driver. Essa função é implementada somente pelo Gerenciador de driver.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLDrivers(  
     SQLHENV         EnvironmentHandle,  
     SQLUSMALLINT    Direction,  
     SQLCHAR *       DriverDescription,  
     SQLSMALLINT     BufferLength1,  
     SQLSMALLINT *   DescriptionLengthPtr,  
     SQLCHAR *       DriverAttributes,  
     SQLSMALLINT     BufferLength2,  
     SQLSMALLINT *   AttributesLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 Entrada Identificador de ambiente.  
  
 *Direção*  
 Entrada Determina se o Gerenciador de driver busca a próxima descrição do driver na lista (SQL_FETCH_NEXT) ou se a pesquisa começa desde o início da lista (SQL_FETCH_FIRST).  
  
 *DriverDescription*  
 Der Ponteiro para um buffer no qual retornar a descrição do driver.  
  
 Se *DriverDescription* for NULL, *DescriptionLengthPtr* ainda retornará o número total de caracteres (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *DriverDescription*.  
  
 *BufferLength1*  
 Entrada Comprimento do buffer **DriverDescription* , em caracteres.  
  
 *DescriptionLengthPtr*  
 Der Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo o caractere de terminação nula) disponível para retornar \*em *DriverDescription*. Se o número de caracteres disponíveis para retornar for maior ou igual a *BufferLength1*, a descrição do driver em \* *DriverDescription* será truncada para *BufferLength1* menos o comprimento de um caractere de terminação nula.  
  
 *Driverattributes*  
 Der Ponteiro para um buffer no qual retornar a lista de pares de valor de atributo de driver (consulte "Comentários").  
  
 Se *driverattributes* for NULL, *AttributesLengthPtr* ainda retornará o número total de bytes (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *driverattributes*.  
  
 *BufferLength2*  
 Entrada Comprimento do buffer \*de *driverattributes* , em caracteres. Se o valor de * \*DriverDescription* for uma cadeia de caracteres Unicode (ao chamar **SQLDriversW**), o argumento *BufferLength* deverá ser um número par.  
  
 *AttributesLengthPtr*  
 Der Ponteiro para um buffer no qual retornar o número total de bytes (excluindo o byte de terminação nula) disponível para retornar \*em *driverattributes*. Se o número de bytes disponíveis para retornar for maior ou igual a *BufferLength2*, a lista de pares de valor de atributo \*em *driverattributes* será truncada para *BufferLength2* menos o comprimento do caractere de terminação nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando o **Sqldriveres** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_ENV e um *identificador* de *EnvironmentHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados pelos **Sqldrives** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|(DM) Gerenciador de driver-mensagem informativa específica. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|(DM) o buffer \* *DriverDescription* não era grande o suficiente para retornar a descrição completa do driver. Portanto, a descrição foi truncada. O comprimento da descrição completa do driver é retornado em \* *DescriptionLengthPtr*. (A função retorna SQL_SUCCESS_WITH_INFO.)<br /><br /> (DM) o buffer \* *driverattributes* não era grande o suficiente para retornar a lista completa de pares de valor de atributo. Portanto, a lista foi truncada. O comprimento da lista não truncada dos pares de valor de atributo é retornado em **AttributesLengthPtr*. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|(DM) o Gerenciador de driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|(DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor especificado para o argumento *BufferLength1* era menor que 0.<br /><br /> (DM) o valor especificado para o argumento *BufferLength2* era menor que 0 ou igual a 1.|  
|HY103|Código de recuperação inválido|(DM) o valor especificado para a *direção* do argumento não era igual a SQL_FETCH_FIRST ou SQL_FETCH_NEXT.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
  
## <a name="comments"></a>Comentários  
 **Sqldriveres** retorna a descrição do driver no \*buffer *DriverDescription* . Ele retorna informações adicionais sobre o driver no \*buffer de *driverattributes* como uma lista de pares de palavra-chave-valor. Todas as palavras-chave listadas nas informações do sistema para drivers serão retornadas para todos os drivers, exceto para **CreateDSN**, que é usado para solicitar a criação de fontes de dados e, portanto, é opcional. Cada par é encerrado com um byte nulo e a lista completa é encerrada com um byte nulo (ou seja, dois bytes nulos marcam o final da lista). Por exemplo, um driver baseado em arquivo usando a sintaxe C pode retornar a lista de atributos a seguir ("\ 0" representa um caractere nulo):  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 Se \*o *driverattributes* não for grande o suficiente para manter a lista inteira, a lista será truncada, os **sqldrives** retornam SQLSTATE 01004 (dados truncados) e o comprimento da lista (excluindo o byte de terminação nula final) é retornado em **AttributesLengthPtr*.  
  
 As palavras-chave de atributo de driver são adicionadas das informações do sistema quando o driver é instalado. Para obter mais informações, consulte [instalando componentes ODBC](../../../odbc/reference/install/installing-odbc-components.md).  
  
 Um aplicativo pode chamar **SQLDrivers** várias vezes para recuperar todas as descrições de driver. O Gerenciador de driver recupera essas informações das informações do sistema. Quando não há mais descrições de driver, os **Sqldriveres** retornam SQL_NO_DATA. Se **SQLDrivers** for chamado com SQL_FETCH_NEXT imediatamente depois de retornar SQL_NO_DATA, ele retornará a primeira descrição do driver. Para obter informações sobre como um aplicativo usa as informações retornadas por **SQLDrivers**, consulte [escolhendo uma fonte de dados ou um driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Se SQL_FETCH_NEXT for passado para **Sqldrives** na primeira vez em que for chamado, os **sqldriveres** retornarão o primeiro nome da fonte de dados.  
  
 Como os **Sqldrives** são implementados no Gerenciador de driver, há suporte para todos os drivers, independentemente da conformidade com os padrões de um driver específico.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Descobrindo e listando os valores necessários para se conectar a uma fonte de dados|[Função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Conectando-se a uma fonte de dados|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Retornando nomes de fonte de dados|[Função SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|Conectando-se a uma fonte de dados usando uma cadeia de conexão ou caixa de diálogo|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
