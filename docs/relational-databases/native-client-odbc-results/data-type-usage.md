---
title: Uso do tipo de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data types
- ODBC data types, about ODBC data types
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC]
- SQL Server Native Client ODBC driver, data types
- data types [ODBC], about data types
ms.assetid: 4f19b0d6-94ac-4a98-a121-57d38787864c
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c0ec45270c7ecd33dae1a441499adefabcc61bb3
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779262"
---
# <a name="data-type-usage"></a>Uso do tipo de dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC de cliente nativo e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] impõem o uso de tipos de dados a seguir.  
  
|Tipo de dados|Limitação|  
|---------------|----------------|  
|Literais de data|Os literais de data, quando armazenados em uma coluna de SQL_TYPE_TIMESTAMP ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados de **DateTime** ou **smalldatetime**), têm um valor de tempo de 12:00:00.000 A.M.|  
|**Money** e **smallmoney**|Somente as partes inteiras dos tipos de dados **Money** e **smallmoney** são significativas. Se a parte decimal dos dados do SQL **Money** for truncada durante a conversão do tipo de dados, o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client retornará um aviso, não um erro.|  
|SQL_BINARY (nullable)|Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 6.0 e anterior, se uma coluna SQL_BINARY permitir valores nulos (nullable), os dados armazenados na fonte de dados não serão preenchidos com zeros. Quando os dados de uma coluna desse tipo são recuperados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC de cliente nativo o acompanha com zeros à direita. Porém, os dados criados em operações executadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como concatenação, não recebem esse preenchimento.<br /><br /> Além disso, quando os dados são colocados em uma coluna desse tipo em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 ou anterior, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] truncará os dados à direita se eles forem muito grandes para o tamanho da coluna.<br /><br /> Observação: o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte à conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6,5 e anterior.|  
|SQL_CHAR (truncation)|Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 e anterior e os dados forem colocados em uma coluna SQL_CHAR, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] irá truncá-los à direita se eles não couberem na coluna.<br /><br /> Observação: o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte à conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6,5 e anterior.|  
|SQL_CHAR (nullable)|Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 e anterior, se uma coluna SQL_CHAR permitir valores nulos (nullable), os dados armazenados na fonte de dados não serão preenchidos com espaços em branco. Quando os dados de uma coluna desse tipo são recuperados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC de cliente nativo o acompanha com espaços em branco à direita. Porém, os dados criados em operações executadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como concatenação, não recebem esse preenchimento.<br /><br /> Observação: o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte à conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6,5 e anterior.|  
|SQL_LONGVARBINARY, SQL_LONGVARCHAR, SQL_WLONGVARCHAR|As atualizações de colunas com tipos de dados SQL_LONGVARBINARY, SQL_LONGVARCHAR ou SQL_WLONGVARCHAR (usando uma cláusula WHERE) que afetam várias linhas têm suporte total quando conectadas a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6. *x* e posterior. Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4,2*x*, um erro S1000, "inserção/atualização parcial. A inserção/atualização de coluna(s) de text ou imagem não foi concluída com êxito" será retornado se a atualização afetar mais de uma linha.<br /><br /> Observação: o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte à conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6,5 e anterior.|  
|Parâmetros de função de cadeia de caracteres|*string_exp* parâmetros para as funções de cadeia de caracteres devem ser do tipo de dados SQL_CHAR ou SQL_VARCHAR. Não há suporte para os tipos de dados SQL_LONG_VARCHAR nas funções de cadeia de caracteres. O parâmetro de *contagem* deve ser menor ou igual a 8.000 porque os tipos de dados SQL_CHAR e SQL_VARCHAR são limitados a um comprimento máximo de 8.000 caracteres.|  
|Literais de hora|Os literais de tempo, quando armazenados em uma SQL_TIMESTAMP coluna ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados de **DateTime** ou **smalldatetime**), têm um valor de data de 1º de janeiro de 1900.|  
|**timestamp**|Somente um valor nulo pode ser inserido manualmente em uma coluna de **carimbo de data/hora** . No entanto, como as colunas **timestamp**são atualizadas automaticamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um valor nulo é substituído.|  
|**tinyint**|O tipo de dados **tinyint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é assinado. Uma coluna **tinyint** é associada a uma variável do tipo de dados SQL_C_UTINYINT por padrão.|  
|Tipos de dados de alias|Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4,2*x*, o driver ODBC adiciona NULL a uma definição de coluna que não declara explicitamente a nulidade de uma coluna. Portanto, a nulidade armazenada na definição de um tipo de dados de alias é ignorada.<br /><br /> Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4,2*x*, as colunas com um tipo de dados de alias que tem um tipo de dados base **Char** ou **Binary** e para a qual nenhuma nulidade é declarada são criadas como tipo de dados **varchar** ou **varbinary**. [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md), [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)e [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) retornam SQL_VARCHAR ou SQL_VARBINARY como o tipo de dados para essas colunas. Os dados recuperados dessas colunas não são preenchidos.<br /><br /> Observação: o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte à conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6,5 e anterior.|  
|Tipos de dados LONG|os parâmetros de *dados em execução* são restritos para os tipos de dados SQL_LONGVARBINARY e SQL_LONGVARCHAR.|  
|Tipos de valor grande|O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client irá expor os tipos **varchar (max)** , **varbinary (max)** e **nvarchar (max)** como SQL_VARCHAR, SQL_VARBINARY e SQL_WVARCHAR (respectivamente) em APIs que aceitam ou retornam tipos de dados ODBC SQL.|  
|UDT (tipo definido pelo usuário)|As colunas UDT são mapeadas como SQL_SS_UDT. Se você mapear uma coluna UDT explicitamente para outro tipo na instrução SQL usando os métodos ToString() ou ToXMLString() do UDT, ou as funções CAST/CONVERT, o tipo de coluna no conjunto de resultados refletirá o tipo para o qual a coluna foi convertida.<br /><br /> O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client só pode ser associado a uma coluna UDT como Binary. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte somente à conversão entre os tipos de dados SQL_SS_UDT e SQL_C_BINARY.|  
|XML|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converterá automaticamente XML em um texto Unicode. O tipo XML é mapeado como SQL_SS_XML.|  
  
## <a name="see-also"></a>Consulte também  
 [Processando &#40;resultados ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
