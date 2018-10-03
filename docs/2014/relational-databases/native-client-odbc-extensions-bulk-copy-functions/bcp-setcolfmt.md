---
title: bcp_setcolfmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_setcolfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_setcolfmt function
ms.assetid: afb47987-39e7-4079-ad66-e0abf4d4c72b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d5d777686bd40fa1b405f20da6173fc2de82640
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48118366"
---
# <a name="bcpsetcolfmt"></a>bcp_setcolfmt
  O **bcp_setcolfmt** função substitui a [bcp_colfmt](bcp-colfmt.md). Ao especificar o agrupamento de coluna, a função **bcp_setcolfmt** precisa ser usada. [bcp_setbulkmode](bcp-setbulkmode.md) pode ser usado para especificar mais de um formato de coluna.  
  
 Essa função oferece uma abordagem flexível à especificação do formato de coluna em uma operação de cópia em massa. Ela é usada para definir atributos de formato de coluna individuais. Cada chamada para **bcp_setcolfmt** define um atributo de formato de coluna.  
  
 A função **bcp_setcolfmt** especifica o formato de origem ou destino dos dados em um arquivo de usuário. Quando usado como um formato de origem **bcp_setcolfmt** Especifica o formato de um arquivo de dados existente usado como uma fonte de dados em uma cópia em massa em uma tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando usado como um formato de destino, o arquivo de dados é criado usando os formatos de coluna especificados com **bcp_setcolfmt**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_setcolfmt (  
HDBC   
hdbc  
,  
INT   
field  
,  
INT   
property  
,  
void*   
pValue  
,  
INT   
cbValue  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *field*  
 É o número de coluna ordinal para o qual a propriedade está sendo definida.  
  
 *property*  
 É um das constantes de propriedade. As constantes de propriedade são definidas nesta tabela.  
  
|propriedade|Valor|Description|  
|--------------|-----------|-----------------|  
|BCP_FMT_TYPE|BYTE|É o tipo de dados desta coluna no arquivo de usuário. Se for diferente do tipo de dados da coluna correspondente na tabela do banco de dados, a cópia em massa converterá os dados se possível.<br /><br /> O parâmetro BCP_FMT_TYPE é enumerado pelos tokens de tipo de dados do SQL Server em sqlncli.h, e não nos enumeradores de tipo de dados ODBC C. Por exemplo, você pode especificar uma cadeia de caracteres, o tipo ODBC SQL_C_CHAR, usando o tipo SQLCHARACTER específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para especificar a representação de dados padrão do tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], defina esse parâmetro como 0.<br /><br /> Para uma cópia em massa do SQL Server para um arquivo, quando BCP_FMT_TYPE for SQLDECIMAL ou SQLNUMERIC:<br /><br /> -Se a coluna de origem não for **decimais** ou **numérico**, a precisão e escala padrão são usados.<br />-Se a coluna de origem for **decimais** ou **numérico**, a precisão e escala da coluna de origem são usados.|  
|BCP_FMT_INDICATOR_LEN|INT|É o comprimento em bytes do indicador (prefixo).<br /><br /> É o comprimento, em bytes, de um indicador de comprimento/nulo nos dados de coluna. Os valores de comprimento de indicador válidos são 0 (quando nenhum indicador é usado), 1, 2 ou 4.<br /><br /> Para especificar o uso do indicador de cópia em massa padrão, defina esse parâmetro como SQL_VARLEN_DATA.<br /><br /> Os indicadores aparecem na memória diretamente antes de quaisquer dados, e no arquivo de dados diretamente antes dos dados aos quais se aplicam.<br /><br /> Se for usada mais de uma maneira de especificar um comprimento de coluna de arquivo de dados (como um indicador e um comprimento de coluna máximo ou um indicador e uma sequência de terminador), a cópia em massa escolherá aquela que resultar na menor quantidade de dados sendo copiados.<br /><br /> Os arquivos de dados gerados pela cópia em massa quando nenhuma intervenção de usuário ajusta o formato dos dados contêm indicadores quando os dados de coluna podem variar em comprimento ou a coluna pode aceitar NULL como valor.|  
|BCP_FMT_DATA_LEN|DBINT|É o comprimento em bytes dos dados (comprimento da coluna).<br /><br /> É o comprimento máximo, em bytes, dos dados dessa coluna no arquivo de usuário, sem incluir o comprimento de qualquer indicador de comprimento ou terminador.<br /><br /> A definição de BCP_FMT_DATA_LEN como SQL_NULL_DATA indica que todos os valores na coluna de arquivo de dados são, ou deveriam ser, definidos como NULL.<br /><br /> A definição de BCP_FMT_DATA_LEN como SQL_VARLEN_DATA indica que o sistema deveria determinar o comprimento dos dados em cada coluna. Para algumas colunas, isso poderia significar que um indicador de comprimento/nulo é gerado para anteceder os dados em uma cópia do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou que o indicador é esperado nos dados copiados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para tipos de dados binários e de caractere do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], BCP_FMT_DATA_LEN pode ser SQL_VARLEN_DATA, SQL_NULL_DATA, 0 ou algum valor positivo. Se BCP_FMT_DATA_LEN for SQL_VARLEN_DATA, o sistema usará o indicador de comprimento, se estiver presente, ou uma sequência de terminador para determinar o comprimento dos dados. Se forem fornecidos um indicador de comprimento e uma sequência de terminador, a cópia em massa usará aquele que resultar na menor quantidade de dados sendo copiados. Se BCP_FMT_DATA_LEN for SQL_VARLEN_DATA, o tipo de dados for um tipo binário ou de caractere do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e nem um indicador de comprimento nem uma sequência de terminador for especificado, o sistema retornará uma mensagem de erro.<br /><br /> Se BCP_FMT_DATA_LEN for 0 ou um valor positivo, o sistema usará BCP_FMT_DATA_LEN como o comprimento de dados máximo. Entretanto, se, além de um BCP_FMT_DATA_LEN positivo, for fornecido um indicador de comprimento ou uma sequência de terminador, o sistema determinará o comprimento dos dados usando o método que resultar na menor quantidade de dados sendo copiados.<br /><br /> O valor BCP_FMT_DATA_LEN representa a contagem de bytes dos dados. Se os dados de caractere forem representados por caracteres que abranjam Unicode, um valor de parâmetro BCP_FMT_DATA_LEN positivo representará a quantidade de caracteres multiplicada pelo tamanho, em bytes, de cada caractere.|  
|BCP_FMT_TERMINATOR|LPCBYTE|Ponteiro para a sequência de terminador (ANSI ou Unicode, conforme apropriado) a ser usado para esta coluna. Este parâmetro é útil principalmente para tipos de dados character porque todos os outros tipos têm comprimento fixo ou, no caso de dados binary, exigem um indicador de comprimento que permite registrar com precisão o número de bytes presentes.<br /><br /> Para evitar encerrar os dados extraídos ou indicar que os dados em um arquivo de usuário não foram encerrados, defina este parâmetro como NULL.<br /><br /> Se for usada mais de uma maneira de especificar um comprimento de coluna de arquivo de usuário (como um terminador e um indicador de comprimento ou um terminador e um comprimento de coluna máximo), a cópia em massa escolherá aquela que resultar na menor quantidade de dados sendo copiados.<br /><br /> A API de cópia em massa executa a conversão de caracteres Unicode em MBCS conforme necessário. É necessário tomar cuidado para garantir que tanto a cadeia de caracteres de bytes do terminador quanto o comprimento da cadeia de caracteres de bytes estejam definidos corretamente.|  
|BCP_FMT_SERVER_COL|INT|Posição ordinal da coluna no banco de dados|  
|BCP_FMT_COLLATION|LPCSTR|Nome do agrupamento.|  
  
 *pValue*  
 É o ponteiro para o valor que será associado a *property*. Ele permite que cada propriedade de formato de coluna seja definida individualmente.  
  
 *cbvalue*  
 É o comprimento do buffer da propriedade em bytes.  
  
## <a name="returns"></a>Retorna  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 Esta função substitui a função **bcp_colfmt** . É oferecida toda a funcionalidade de **bcp_colfmt** na função **bcp_setcolfmt** . Além disso, também há suporte ao agrupamento de coluna. É recomendável que os atributos de formato de coluna a seguir sejam definidos nesta ordem:  
  
 BCP_FMT_SERVER_COL  
  
 BCP_FMT_DATA_LEN  
  
 BCP_FMT_TYPE  
  
 A função **bcp_setcolfmt** permite especificar o formato do arquivo de usuário para cópias em massa. Para cópia em massa, um formato contém as seguintes partes:  
  
-   Um mapeamento de colunas do arquivo de usuário para colunas de banco de dados.  
  
-   O tipo de dados de cada coluna do arquivo de usuário.  
  
-   O comprimento do indicador opcional para cada coluna.  
  
-   O comprimento máximo dos dados por coluna do arquivo de usuário.  
  
-   A sequência de bytes de encerramento opcional para cada coluna.  
  
-   O comprimento da sequência de bytes de encerramento opcional.  
  
 Cada chamada para **bcp_setcolfmt** especifica o formato para uma coluna do arquivo de usuário. Por exemplo, para alterar as configurações padrão para três colunas em um arquivo de dados de usuário de cinco colunas, primeiro chame [bcp_columns](bcp-columns.md)**(5)** e, em seguida, chame **bcp_setcolfmt** cinco vezes, com três dessas chamadas definindo o formato personalizado. Para as duas chamadas restantes, defina BCP_FMT_TYPE como 0 e defina BCP_FMT_INDICATOR_LENGTH, BCP_FMT_DATA_LEN e *cbValue* como 0, SQL_VARLEN_DATA e 0, respectivamente. Esse procedimento copia todas as cinco colunas, três com seu formato personalizado e duas com o formato padrão.  
  
 A função **bcp_columns** deve ser chamada antes de chamar **bcp_setcolfmt**.  
  
 Você deve chamar **bcp_setcolfmt** uma vez para cada propriedade de cada coluna no arquivo de usuário.  
  
 Você não precisa copiar todos os dados em um arquivo de usuário para a tabela do SQL Server. Para ignorar uma coluna, especifique o formato dos dados para a coluna, definindo o parâmetro BCP_FMT_SERVER_COL como 0. Se desejar ignorar uma coluna, especifique seu tipo.  
  
 O [bcp_writefmt](bcp-writefmt.md) função pode ser usada para persistir a especificação de formato.  
  
## <a name="bcpsetcolfmt-support-for-enhanced-date-and-time-features"></a>Suporte do bcp_setcolfmt a recursos aprimorados de data e hora  
 Os tipos usados com a propriedade BCP_FMT_TYPE para tipos de data/hora são como especificado na [alterações de cópia em massa para tipos aprimorada de data e hora &#40;OLE DB e ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Para obter mais informações, consulte [aprimoramentos de data e hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
