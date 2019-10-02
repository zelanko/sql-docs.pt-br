---
title: bcp_colfmt | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_colfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_colfmt function
ms.assetid: 5c3b6299-80c7-4e84-8e69-4ff33009548e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a08973bcfadb88750129fd440eeabb3f69bb2ddb
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71707728"
---
# <a name="bcp_colfmt"></a>bcp_colfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Especifica o formato de origem ou de destino dos dados em um arquivo de usuário. Quando usado como formato de origem, **bcp_colfmt** especifica o formato de um arquivo de dados existente usado como a fonte de dados em uma cópia em massa para uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando usado como formato de destino, o arquivo de dados é criado usando os formatos de coluna especificados com **bcp_colfmt**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_colfmt (  
        HDBC hdbc,  
        INT idxUserDataCol,  
        BYTE eUserDataType,  
        INT cbIndicator,  
        DBINT cbUserData,  
        LPCBYTE pUserDataTerm,  
        INT cbUserDataTerm,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *idxUserDataCol*  
 É o número de coluna ordinal no arquivo de dados de usuário para o qual o formato está sendo especificado. A primeira coluna é 1.  
  
 *eUserDataType*  
 É o tipo de dados desta coluna no arquivo de usuário. Se diferente do tipo de dados da coluna correspondente na tabela do banco de dados (*idxServerColumn*), a cópia em massa converterá os dados, caso seja possível.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introduziu o suporte para os tokens de tipo de dados SQLXML e SQLUDT no parâmetro *eUserDataType* .  
  
 O parâmetro *eUserDataType* é enumerado pelos tokens de tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em sqlncli.h e não pelos enumeradores de tipo de dados ODBC C. Por exemplo, você pode especificar uma cadeia de caracteres, o tipo ODBC SQL_C_CHAR, usando o tipo SQLCHARACTER específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para especificar a representação de dados padrão do tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , defina esse parâmetro como 0.  
  
 Para uma cópia em massa fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um arquivo, quando *eUserDataType* for SQLDECIMAL ou SQLNUMERIC:  
  
-   Se a coluna de origem não for **decimal** ou **numeric**, serão usadas a precisão e escala padrão.  
  
-   Se a coluna de origem não for **decimal** ou **numeric**, serão usadas a precisão e escala da coluna de origem.  
  
 *cbIndicator*  
 É o comprimento, em bytes, de um indicador de comprimento/nulo nos dados de coluna. Os valores de comprimento de indicador válidos são 0 (quando nenhum indicador é usado), 1, 2, 4 ou 8.  
  
 Para especificar o uso do indicador de cópia em massa padrão, defina esse parâmetro como SQL_VARLEN_DATA.  
  
 Os indicadores aparecem na memória diretamente antes de quaisquer dados, e no arquivo de dados diretamente antes dos dados aos quais se aplicam.  
  
 Se for usada mais de uma maneira de especificar um comprimento de coluna de arquivo de dados (como um indicador e um comprimento de coluna máximo ou um indicador e uma sequência de terminador), a cópia em massa escolherá aquela que resultar na menor quantidade de dados sendo copiados.  
  
 Os arquivos de dados gerados pela cópia em massa quando nenhuma intervenção de usuário ajusta o formato dos dados contêm indicadores quando os dados de coluna podem variar em comprimento ou a coluna pode aceitar NULL como valor.  
  
 *cbUserData*  
 É o comprimento máximo, em bytes, dos dados dessa coluna no arquivo de usuário, sem incluir o comprimento de qualquer indicador de comprimento ou terminador.  
  
 A definição de *cbUserData* como SQL_NULL_DATA indica que todos os valores na coluna de arquivo de dados são ou deveriam ser definidos como NULL.  
  
 A definição de *cbUserData* como SQL_VARLEN_DATA indica que o sistema deve determinar o comprimento dos dados em cada coluna. Para algumas colunas, isso poderia significar que um indicador de comprimento/nulo é gerado para anteceder os dados em uma cópia do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou que o indicador é esperado nos dados copiados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para os tipos de dados binary e character do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , *cbUserData* pode ser SQL_VARLEN_DATA, SQL_NULL_DATA, 0 ou algum valor positivo. Se *cbUserData* for SQL_VARLEN_DATA, o sistema usará o indicador de comprimento, se houver, ou uma sequência de terminador para determinar o comprimento dos dados. Se forem fornecidos um indicador de comprimento e uma sequência de terminador, a cópia em massa usará aquele que resultar na menor quantidade de dados sendo copiados. Se *cbUserData* for SQL_VARLEN_DATA, o tipo de dados for um tipo binary ou character do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e nem um indicador de comprimento nem uma sequência de terminador forem especificados, o sistema retornará uma mensagem de erro.  
  
 Se *cbUserData* for 0 ou um valor positivo, o sistema usará *cbUserData* como o comprimento de dados máximo. Entretanto, se, além de um *cbUserData*positivo, for fornecido um indicador de comprimento ou uma sequência de terminador, o sistema determinará o comprimento dos dados usando o método que resulta na menor quantidade de dados sendo copiados.  
  
 O valor *cbUserData* representa a contagem de bytes dos dados. Se dados de caracteres forem representados por caracteres que abrangem Unicode, um valor de parâmetro *cbUserData* positivo representará o número de caracteres multiplicado pelo tamanho, em bytes, de cada caractere.  
  
 *pUserDataTerm*  
 É a sequência de terminador a ser usada para esta coluna. Este parâmetro é útil principalmente para tipos de dados character porque todos os outros tipos têm comprimento fixo ou, no caso de dados binary, exigem um indicador de comprimento que permite registrar com precisão o número de bytes presentes.  
  
 Para evitar encerrar os dados extraídos ou indicar que os dados em um arquivo de usuário não foram encerrados, defina este parâmetro como NULL.  
  
 Se for usada mais de uma maneira de especificar um comprimento de coluna de arquivo de usuário (como um terminador e um indicador de comprimento ou um terminador e um comprimento de coluna máximo), a cópia em massa escolherá aquela que resultar na menor quantidade de dados sendo copiados.  
  
 A API de cópia em massa executa a conversão de caracteres Unicode em MBCS conforme necessário. É necessário tomar cuidado para garantir que tanto a cadeia de caracteres de bytes do terminador quanto o comprimento da cadeia de caracteres de bytes estejam definidos corretamente.  
  
 *cbUserDataTerm*  
 É o comprimento, em bytes, da sequência de terminador a ser usada para esta coluna. Se nenhum terminador estiver presente ou for desejado nos dados, defina esse valor como 0.  
  
 *idxServerCol*  
 É a posição ordinal da coluna na tabela do banco de dados. O número da primeira coluna é 1. A posição ordinal de uma coluna é relatada por [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md).  
  
 Se esse valor for 0, a cópia em massa irá ignorar a coluna no arquivo de dados.  
  
## <a name="returns"></a>Retorna  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 A função **bcp_colfmt** permite especificar o formato do arquivo de usuário para cópias em massa. Para cópia em massa, um formato contém as seguintes partes:  
  
-   Um mapeamento de colunas do arquivo de usuário para colunas de banco de dados.  
  
-   O tipo de dados de cada coluna do arquivo de usuário.  
  
-   O comprimento do indicador opcional para cada coluna.  
  
-   O comprimento máximo dos dados por coluna do arquivo de usuário.  
  
-   A sequência de bytes de encerramento opcional para cada coluna.  
  
-   O comprimento da sequência de bytes de encerramento opcional.  
  
 Cada chamada de **bcp_colfmt** especifica o formato de uma coluna do arquivo de usuário. Por exemplo, para alterar as configurações padrão de três colunas em um arquivo de dados de usuário de cinco colunas, primeiro chame [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) **(5)** e, em seguida, chame **bcp_colfmt** cinco vezes, sendo três dessas chamadas para definir seu formato personalizado. Para as duas chamadas restantes, defina *eUserDataType* como 0 e defina *cbIndicator*, *cbUserData*e *cbUserDataTerm* respectivamente como 0, SQL_VARLEN_DATA e 0. Esse procedimento copia todas as cinco colunas, três com seu formato personalizado e duas com o formato padrão.  
  
 Para *cbIndicator*, um valor 8 indica que agora um tipo de valor grande é válido. Se o prefixo for especificado para um campo cuja coluna correspondente é um novo tipo max, ele poderá ser definido somente como 8. Para obter detalhes, consulte [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md).  
  
 A função **bcp_columns** deve ser chamada antes de qualquer chamada de **bcp_colfmt**.  
  
 Chame **bcp_colfmt** uma vez para cada coluna no arquivo de usuário.  
  
 Chamar **bcp_colfmt** mais de uma vez para qualquer coluna do arquivo de usuário gera um erro.  
  
 Você não precisa copiar todos os dados de um arquivo de usuário para a tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para ignorar uma coluna, especifique o formato dos dados da coluna, definindo o parâmetro *idxServerCol* como 0. Se desejar ignorar uma coluna, especifique seu tipo.  
  
 A função [bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md) pode ser usada para persistir a especificação de formato.  
  
## <a name="bcp_colfmt-support-for-enhanced-date-and-time-features"></a>Suporte do bcp_colfmt a recursos aprimorados de data e hora  
 Para obter informações sobre os tipos usados com o parâmetro *eUserDataType* para tipos de data/hora, consulte [alterações de cópia em massa para tipos &#40;de data e&#41;hora aprimorados OLE DB e ODBC](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Para obter mais informações, consulte [melhorias &#40;de data e&#41;hora em ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
