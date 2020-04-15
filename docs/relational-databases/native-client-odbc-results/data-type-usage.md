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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0384857c53e898af9fca89bb2ee2351f0b65f986
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297848"
---
# <a name="data-type-usage"></a>Uso do tipo de dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Cliente Nativo e impõe o seguinte uso dos tipos de dados.  
  
|Tipo de dados|Limitações|  
|---------------|----------------|  
|Literais de data|Os literais de data,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando armazenados em uma coluna de SQL_TYPE_TIMESTAMP (tipos de dados de **data-hora** ou **data de data)** têm um valor de hora de 12:00:00.000 A.M.|  
|**dinheiro** e **dinheiro pequeno**|Apenas as partes inteiras do **dinheiro** e os tipos de dados **de smallmoney** são significativos. Se a parte decimal dos dados **de dinheiro** SQL for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] truncada durante a conversão do tipo de dados, o driver ODBC do Cliente Nativo reame um aviso, não um erro.|  
|SQL_BINARY (nullable)|Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 6.0 e anterior, se uma coluna SQL_BINARY permitir valores nulos (nullable), os dados armazenados na fonte de dados não serão preenchidos com zeros. Quando os dados de tal coluna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são recuperados, o driver Cliente Nativo ODBC os bloqueia com zeros à direita. Porém, os dados criados em operações executadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como concatenação, não recebem esse preenchimento.<br /><br /> Além disso, quando os dados são colocados em uma coluna desse tipo em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 ou anterior, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] truncará os dados à direita se eles forem muito grandes para o tamanho da coluna.<br /><br /> Nota: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O driver Cliente Nativo ODBC suporta conexão a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6,5 e anteriormente.|  
|SQL_CHAR (truncation)|Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 e anterior e os dados forem colocados em uma coluna SQL_CHAR, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] irá truncá-los à direita se eles não couberem na coluna.<br /><br /> Nota: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O driver Cliente Nativo ODBC suporta conexão a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6,5 e anteriormente.|  
|SQL_CHAR (nullable)|Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 e anterior, se uma coluna SQL_CHAR permitir valores nulos (nullable), os dados armazenados na fonte de dados não serão preenchidos com espaços em branco. Quando os dados de tal coluna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são recuperados, o driver Cliente Nativo ODBC os bloqueia com espaços em branco à direita. Porém, os dados criados em operações executadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como concatenação, não recebem esse preenchimento.<br /><br /> Nota: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O driver Cliente Nativo ODBC suporta conexão a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6,5 e anteriormente.|  
|SQL_LONGVARBINARY, SQL_LONGVARCHAR, SQL_WLONGVARCHAR|Atualizações de colunas com SQL_LONGVARBINARY, SQL_LONGVARCHAR ou SQL_WLONGVARCHAR tipos de dados (usando uma cláusula WHERE) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que afetam várias linhas são totalmente suportadas quando conectadas a uma instância de 6. *x* e depois. Quando conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uma ocorrência de 4,2*x*, um erro s1000, "Inserção/atualização parcial. A inserção/atualização de coluna(s) de text ou imagem não foi concluída com êxito" será retornado se a atualização afetar mais de uma linha.<br /><br /> Nota: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O driver Cliente Nativo ODBC suporta conexão a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6,5 e anteriormente.|  
|Parâmetros de função de cadeia de caracteres|*string_exp* parâmetros para as funções de string devem ser de SQL_CHAR de tipo de dados ou SQL_VARCHAR. Não há suporte para os tipos de dados SQL_LONG_VARCHAR nas funções de cadeia de caracteres. O parâmetro *de contagem* deve ser menor ou igual a 8.000 porque os SQL_CHAR e SQL_VARCHAR tipos de dados são limitados a um comprimento máximo de 8.000 caracteres.|  
|Literais de hora|Os literais de tempo,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando armazenados em uma coluna de SQL_TIMESTAMP (tipos de dados de **data-hora** ou **data-hora)** têm um valor de data de 1 º de janeiro de 1900.|  
|**timestamp**|Apenas um valor NULL pode ser inserido manualmente em uma coluna **de carimbo de tempo.** No entanto, como as colunas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de carimbo de **tempo**são automaticamente atualizadas por , um valor NULL é substituído.|  
|**tinyint**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados **tinyint** não está assinado. Uma **coluna tinyint** está vinculada a uma variável de tipo de dados SQL_C_UTINYINT por padrão.|  
|Tipos de dados alias|Quando conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uma instância de 4,2*x,* o driver ODBC adiciona NULL a uma definição de coluna que não declara explicitamente a nulidade de uma coluna. Portanto, a nulidade armazenada na definição de um tipo de dados de alias é ignorada.<br /><br /> Quando conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uma instância de 4,2*x*, colunas com um tipo de dados alias que tenha um tipo de **dados** base de char ou **binário** e para os quais nenhuma nulidade é declarada são criadas como tipo de dados **varchar** ou **varbinary**. [SQLColAttribute,](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)e [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) retornam SQL_VARCHAR ou SQL_VARBINARY como o tipo de dados dessas colunas. Os dados recuperados dessas colunas não são preenchidos.<br /><br /> Nota: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O driver Cliente Nativo ODBC suporta conexão a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6,5 e anteriormente.|  
|Tipos de dados LONG|os parâmetros *de data-at-execution* são restritos tanto para os SQL_LONGVARBINARY quanto para os tipos de dados SQL_LONGVARCHAR.|  
|Tipos de valor grande|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver Nativo Cliente ODBC exporá os tipos **varchar(max)**, **varbinary(max)** e **nvarchar(max)** como SQL_VARCHAR, SQL_VARBINARY e SQL_WVARCHAR (respectivamente) em APIs que aceitam ou devolvem tipos de dados ODBC SQL.|  
|UDT (tipo definido pelo usuário)|As colunas UDT são mapeadas como SQL_SS_UDT. Se você mapear uma coluna UDT explicitamente para outro tipo na instrução SQL usando os métodos ToString() ou ToXMLString() do UDT, ou as funções CAST/CONVERT, o tipo de coluna no conjunto de resultados refletirá o tipo para o qual a coluna foi convertida.<br /><br /> O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Cliente Nativo só pode se ligar a uma coluna UDT como binário. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte somente à conversão entre os tipos de dados SQL_SS_UDT e SQL_C_BINARY.|  
|XML|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converterá automaticamente XML em um texto Unicode. O tipo XML é mapeado como SQL_SS_XML.|  
  
## <a name="see-also"></a>Consulte Também  
 [Resultados de processamento &#40;&#41;Da ODBC](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
