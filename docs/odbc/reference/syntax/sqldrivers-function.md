---
title: Função SQLDrivers | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2496e7cd5f2abe0831c72484bed374d7aa1513ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302757"
---
# <a name="sqldrivers-function"></a>Função SQLDrivers
**Conformidade**  
 Versão introduzida: ODBC 2.0 Normas Conformidade: ODBC  
  
 **Resumo**  
 **SQLDrivers** lista descrições do driver e palavras-chave de atributo do driver. Esta função é implementada apenas pelo Driver Manager.  
  
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
 [Entrada] Alça do meio ambiente.  
  
 *Direção*  
 [Entrada] Determina se o Driver Manager busca a próxima descrição do driver na lista (SQL_FETCH_NEXT) ou se a pesquisa começa desde o início da lista (SQL_FETCH_FIRST).  
  
 *DriverDescrição*  
 [Saída] Ponteiro para um buffer no qual para retornar a descrição do driver.  
  
 Se *driverDescription* for NULL, *DescriptionLengthPtr* ainda retornará o número total de caracteres (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado por *DriverDescription*.  
  
 *Comprimento do buffer1*  
 [Entrada] Comprimento do buffer **DriverDescription,* em caracteres.  
  
 *DescriçãoLengthPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo o caractere de rescisão nula) disponível para retornar em \* *DriverDescription*. Se o número de caracteres disponíveis para retornar for maior ou \*igual a *BufferLength1,* a descrição do driver em *DriverDescription* será truncada em *BufferLength1* menos o comprimento de um caractere de rescisão nula.  
  
 *Atributos de driver*  
 [Saída] Ponteiro para um buffer no qual retornar a lista de pares de valores de atributo do driver (consulte "Comentários").  
  
 Se *DriverAttributes* for NULL, *AttributesLengthPtr* ainda retornará o número total de bytes (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado por *DriverAttributes*.  
  
 *Comprimento do buffer2*  
 [Entrada] Comprimento do \* *buffer DriverAttributes,* em caracteres. Se * \** o valor DriverDescription for uma seqüência unicode (ao chamar **SQLDriversW),** o argumento *BufferLength* deve ser um número uniforme.  
  
 *AtributosLengthPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de bytes (excluindo \*o byte de rescisão nula) disponível para retornar em *DriverAttributes*. Se o número de bytes disponíveis para retornar for maior ou igual a \* *BufferLength2,* a lista de pares de valores de atributo sustais em *DriverAttributes* será truncada para *BufferLength2* menos o comprimento do caractere de rescisão nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLDrivers** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_ENV e uma *alça* de *EnvironmentHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLDrivers** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|(DM) Mensagem informacional específica do Driver Manager. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|(DM) O \*buffer *DriverDescription* não era grande o suficiente para retornar a descrição completa do driver. Portanto, a descrição foi truncada. O comprimento da descrição completa do \*driver é devolvido em *DescriptionLengthPtr*. (Função retorna SQL_SUCCESS_WITH_INFO.)<br /><br /> (DM) O \*buffer *DriverAttributes* não era grande o suficiente para retornar a lista completa de pares de valores de atributo. Portanto, a lista foi truncada. O comprimento da lista não truncada de pares de valores de atributo é retornado em **AtributosLengthPtr*. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|(DM) O Driver Manager não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função.|  
|HY010|Erro de seqüência de função|(DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor especificado para o argumento *BufferLength1* foi inferior a 0.<br /><br /> (DM) O valor especificado para o argumento *BufferLength2* foi inferior a 0 ou igual a 1.|  
|HY103|Código de recuperação inválido|(DM) O valor especificado para a *direção* do argumento não era igual a SQL_FETCH_FIRST ou SQL_FETCH_NEXT.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
  
## <a name="comments"></a>Comentários  
 **SQLDrivers** retorna a descrição \*do driver no buffer *DriverDescription.* Ele retorna informações adicionais \*sobre o driver no buffer *DriverAttributes* como uma lista de pares de valor esporas. Todas as palavras-chave listadas nas informações do sistema para drivers serão devolvidas para todos os drivers, exceto para **CreateDSN**, que é usado para solicitar a criação de fontes de dados e, portanto, é opcional. Cada par é encerrado com um byte nulo, e a lista completa é encerrada com um byte nulo (ou seja, dois bytes nulos marcam o fim da lista). Por exemplo, um driver baseado em arquivo usando sintaxe C pode retornar a seguinte lista de atributos ("\0" representa um caractere nulo):  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 Se \* *DriverAttributes* não for grande o suficiente para manter a lista inteira, a lista será truncada, **SQLDrivers** retorna SQLSTATE 01004 (Dados truncados) e o comprimento da lista (excluindo o byte final de rescisão nula) é devolvido em **AttributesLengthPtr*.  
  
 As palavras-chave do atributo do driver são adicionadas das informações do sistema quando o driver é instalado. Para obter mais informações, consulte [Instalando componentes ODBC](../../../odbc/reference/install/installing-odbc-components.md).  
  
 Um aplicativo pode ligar para **sqldrivers** várias vezes para recuperar todas as descrições do driver. O Driver Manager recupera essas informações das informações do sistema. Quando não há mais descrições de driver, **SQLDrivers** retorna SQL_NO_DATA. Se **o SQLDrivers** for chamado com SQL_FETCH_NEXT imediatamente após o retorno SQL_NO_DATA, ele retorna a primeira descrição do driver. Para obter informações sobre como um aplicativo usa as informações retornadas pelos **SQLDrivers,** consulte [Escolher uma Fonte de Dados ou Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Se SQL_FETCH_NEXT for passado para **SQLDrivers** na primeira vez que for chamado, **o SQLDrivers** reahde o primeiro nome de origem dos dados.  
  
 Como o **SQLDrivers** é implementado no Driver Manager, ele é suportado para todos os drivers, independentemente da conformidade dos padrões de um determinado driver.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Descobrir e listar valores necessários para se conectar a uma fonte de dados|[Função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Conectando-se a uma fonte de dados|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Retornando nomes de origem de dados|[Função SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|Conectando-se a uma fonte de dados usando uma seqüência de conexão ou caixa de diálogo|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
