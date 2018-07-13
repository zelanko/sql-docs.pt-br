---
title: Tipo de dados de uso | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41fc88722e93dd57f026f4e1e153d9c3e59aaaf6
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37432045"
---
# <a name="data-type-usage"></a>Uso do tipo de dados
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] impõem o seguinte uso de tipos de dados.  
  
|Tipo de dados|Limitação|  
|---------------|----------------|  
|Literais de data|Literais de data, quando armazenados em uma coluna SQL_TYPE_TIMESTAMP ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados de **datetime** ou **smalldatetime**), têm um valor de tempo de 12:00:00.000 A.M.|  
|**dinheiro** e **smallmoney**|Somente as partes de inteiro do **dinheiro** e **smallmoney** tipos de dados são significativos. Se a parte decimal do SQL **dinheiro** dados são truncados durante conversão de tipo de dados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client retorna um aviso, não um erro.|  
|SQL_BINARY (nullable)|Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 6.0 e anterior, se uma coluna SQL_BINARY permitir valores nulos (nullable), os dados armazenados na fonte de dados não serão preenchidos com zeros. Quando os dados de uma coluna desse tipo são recuperados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client acrescenta zeros à direita. Porém, os dados criados em operações executadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como concatenação, não recebem esse preenchimento.<br /><br /> Além disso, quando os dados são colocados em uma coluna desse tipo em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 ou anterior, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] truncará os dados à direita se eles forem muito grandes para o tamanho da coluna. **Observação:** as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece suporte a se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 e anteriores.|  
|SQL_CHAR (truncation)|Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 e anterior e os dados forem colocados em uma coluna SQL_CHAR, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] irá truncá-los à direita se eles não couberem na coluna. **Observação:** as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece suporte a se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 e anteriores.|  
|SQL_CHAR (nullable)|Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 e anterior, se uma coluna SQL_CHAR permitir valores nulos (nullable), os dados armazenados na fonte de dados não serão preenchidos com espaços em branco. Quando os dados de uma coluna desse tipo são recuperados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client acrescenta espaços em branco à direita. Porém, os dados criados em operações executadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como concatenação, não recebem esse preenchimento. **Observação:** as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece suporte a se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 e anteriores.|  
|SQL_LONGVARBINARY, SQL_LONGVARCHAR, SQL_WLONGVARCHAR|Atualizações de colunas com SQL_LONGVARBINARY, SQL_LONGVARCHAR ou SQL_WLONGVARCHAR tipos de dados (usando uma cláusula WHERE) que afetam várias linhas têm suporte total quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6. *x* e versões posteriores. Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*, um erro de S1000, "inserção/atualização parcial. A inserção/atualização de coluna(s) de text ou imagem não foi concluída com êxito" será retornado se a atualização afetar mais de uma linha. **Observação:** as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece suporte a se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 e anteriores.|  
|Parâmetros de função de cadeia de caracteres|*string_exp* tipo de parâmetros na cadeia de caracteres funções devem ser de dados SQL_CHAR ou SQL_VARCHAR. Não há suporte para os tipos de dados SQL_LONG_VARCHAR nas funções de cadeia de caracteres. O *contagem* parâmetro deve ser menor ou igual a 8.000 porque os tipos de dados SQL_CHAR e SQL_VARCHAR são limitados a um comprimento máximo de 8.000 caracteres.|  
|Literais de hora|Literais de hora, quando armazenados em uma coluna SQL_TIMESTAMP ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados de **datetime** ou **smalldatetime**), tem um valor de data do dia 1 de janeiro de 1900.|  
|**timestamp**|Somente um valor NULL pode ser inserido manualmente em um **carimbo de hora** coluna. No entanto, porque **timestamp**colunas são atualizadas automaticamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um valor NULL é substituído.|  
|**tinyint**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tinyint** tipo de dados não estiver assinado. Um **tinyint** coluna é associada a uma variável do tipo de dados SQL_C_UTINYINT por padrão.|  
|Tipos de dados de alias|Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*, o driver ODBC adiciona NULL a uma definição de coluna que não declara explicitamente a nulidade da coluna. Portanto, a nulidade armazenada na definição de um tipo de dados de alias é ignorada.<br /><br /> Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*, o tipo de colunas com um tipo de dados de alias que tem uma base de dados do **char** ou **binário** e para o qual nenhuma nulidade é declarada são criadas como tipo de dados **varchar** ou **varbinary**. [SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md), [SQLColumns](../native-client-odbc-api/sqlcolumns.md), e [SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md) retornam SQL_VARCHAR ou SQL_VARBINARY como os dados de tipo para essas colunas. Os dados recuperados dessas colunas não são preenchidos. **Observação:** as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece suporte a se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 e anteriores.|  
|Tipos de dados LONG|*dados em execução* parâmetros são restritos para SQL_LONGVARBINARY e os tipos de dados SQL_LONGVARCHAR.|  
|Tipos de valor grande|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client irá expor **varchar (max)**, **varbinary (max)**, e **nvarchar (max)** tipos como SQL_VARCHAR, SQL_VARBINARY e SQL _ WVARCHAR (respectivamente) em APIs que aceitam ou retornam tipos de dados SQL ODBC.|  
|UDT (tipo definido pelo usuário)|As colunas UDT são mapeadas como SQL_SS_UDT. Se você mapear uma coluna UDT explicitamente para outro tipo na instrução SQL usando os métodos ToString() ou ToXMLString() do UDT, ou as funções CAST/CONVERT, o tipo de coluna no conjunto de resultados refletirá o tipo para o qual a coluna foi convertida.<br /><br /> O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client só pode ser associado a uma coluna UDT como binary. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte somente à conversão entre os tipos de dados SQL_SS_UDT e SQL_C_BINARY.|  
|XML|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converterá automaticamente XML em um texto Unicode. O tipo XML é mapeado como SQL_SS_XML.|  
  
## <a name="see-also"></a>Consulte também  
 [Processando resultados &#40;ODBC&#41;](processing-results-odbc.md)  
  
  
