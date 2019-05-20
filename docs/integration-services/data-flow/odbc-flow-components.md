---
title: Componentes de fluxo ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cf751f1e-2348-4a77-904c-bd92c0d7d0ae
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e59efeb278c7d5f1236a9943f03ad471491f354a
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726653"
---
# <a name="odbc-flow-components"></a>Componentes de fluxo ODBC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Este tópico descreve os conceitos necessários para criar um fluxo de dados ODBC usando [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]  
  
 O Conector para ODBC para o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] ajuda os desenvolvedores do SSIS a criar pacotes com facilidade que carregam e descarregam dados de bancos de dados com suporte do ODBC.  
  
 O Conector ODBC foi criado para obter o desempenho ideal ao carregar ou descarregar dados de um banco de dados com suporte ODBC no contexto do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
## <a name="benefits"></a>Benefícios  
 A origem e o destino ODBC do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] fornecem uma margem competitiva para o SSIS em projetos que lidam com o carregamento ou descarregamento de dados de bancos de dados com suporte ODBC.  
  
 A origem e o destino ODBC permitem integração de dados de alto desempenho com bancos de dados com ODBC habilitado. Ambos os componentes podem ser configurados para funcionar com associações de matriz de parâmetro row-wise para provedores ODBC de alto funcionamento com suporte a esse modo de associação e associações de parâmetro de linha única para provedores ODBC de baixo funcionamento.  
  
## <a name="getting-started-with-the-odbc-source-and-destination"></a>Introdução à origem e destino ODBC  
 Antes de configurar pacotes que utilizam o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)], você deve assegurar que os itens a seguir estejam disponíveis.  
  
-   [Origem ODBC](../../integration-services/data-flow/odbc-source.md)  
  
-   [Destino ODBC](../../integration-services/data-flow/odbc-destination.md)  
  
 A origem e o destino ODBC fornecem um modo fácil para descarregar e carregar dados e transferir dados de um banco de dados de origem com suporte ODBC para um banco de dados de destino com suporte ODBC.  
  
 Para usar a origem ou destino para carregar ou descarregar dados, abra um novo [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] Project no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Em seguida, arraste a origem ou o destino para a superfície de design do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
-   O componente de origem ODBC lê dados do banco de dados de origem com suporte ODBC.  
  
 Você pode conectar a origem ODBC a qualquer destino ou pode transformar o componente com suporte SSIS.  
  
 **Consulte também:**  
  
 Origem ODBC  
  
 Editor de Origem ODBC (página Gerenciador de Conexões)  
  
 Editor de Origem ODBC (página Saída de Erro)  
  
-   O destino ODBC carrega dados em um banco de dados com suporte ODBC. Você pode conectar o destino a qualquer origem ou pode transformar o componente com suporte SSIS.  
  
 **Consulte também:**  
  
 Destino ODBC  
  
 Editor do Destino ODBC (página Gerenciador de Conexões)  
  
 Editor de Destinos ADO NET (página Saída de Erro)  
  
## <a name="operating-scenarios"></a>Cenários de operação  
 Esta seção descreve alguns dos usos principais para os componentes de origem e destino ODBC.  
  
### <a name="bulk-copy-data-from-sql-server-tables-to-any-odbc-supported-database-table"></a>Dados de Cópia em massa de tabelas do SQL Server para qualquer tabela de banco de dados com suporte ODBC  
 Você pode usar os componentes para copiar dados em massa de uma ou mais tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma única tabela de banco de dados com suporte ODBC.  
  
 O exemplo a seguir mostra como criar uma Tarefa de Fluxo de Dados SSIS que extrai dados de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os carrega em uma tabela DB2.  
  
-   Crie um [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] Project no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
-   Crie um gerenciador de conexões OLE DB que se conecta ao banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém os dados que você deseja copiar.  
  
-   Crie um gerenciador de conexões ODBC que usa um driver DB2 ODBC localmente instalado com um apontamento DSN para um banco de dados DB2 local ou remoto. Esse banco de dados é o local em que os dados do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são carregados.  
  
-   Arraste uma origem OLE DB para a superfície de design e configure a origem para obter os dados do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e da tabela com os dados que você vai extrair. Use o gerenciador de conexões OLE DB criado anteriormente.  
  
-   Arraste um destino ODBC para a superfície de design, conecte a saída de origem ao destino ODBC e configure o destino para carregar os dados na tabela DB2 com os dados extraídos do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use o gerenciador de conexões ODBC criado anteriormente.  
  
### <a name="bulk-copy-data-from-odbc-supported-database-tables-to-any-sql-server-table"></a>Dados de Cópia em massa de tabelas de banco de dados com suporte ODBC para qualquer tabela SQL Server  
 Você pode usar os componentes para copiar dados em massa de uma ou mais tabelas de banco de dados com suporte ODBC para uma única tabela de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 O exemplo a seguir mostra como criar uma Tarefa de Fluxo de Dados SSIS que extrai dados de uma tabela de banco de dados Sybase do e os carrega em uma tabela de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Crie um [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] Project no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
-   Crie um gerenciador de conexões ODBC que usa um driver Sybase ODBC localmente instalado com um apontamento DSN para um banco de dados Sybase local ou remoto. Esse banco de dados é o local onde os dados são extraídos.  
  
-   Crie um gerenciador de conexões OLE DB que se conecta ao banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde você deseja carregar os dados.  
  
-   Arraste uma origem ODBC DB para a superfície de design e configure a origem para obter os dados da tabela Sybase com os dados que você vai copiar. Use o gerenciador de conexões ODBC criado anteriormente.  
  
-   Arraste um destino OLE DB para a superfície de design, conecte a saída de origem ao destino OLE DB e configure o destino para carregar os dados na tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com os dados extraídos do banco de dados Sybase. Use o gerenciador de conexões OLE DB criado anteriormente.  
  
## <a name="supported-data-types"></a>Tipos de dados com suporte  
 Os componentes ODBC Bulk SSIS oferecem suporte a todos os tipos de dados ODBC internos, incluindo suporte para objetos grandes (CLOBs e BLOBs).  
  
Não há nenhum suporte de tipo de dados para tipos C extensíveis conforme descrito nas especificações ODBC 3.8. A tabela a seguir descreve quais tipos de dados SSIS são usados para cada tipo ODBC SQL. Um desenvolvedor de SSIS pode anular o mapeamento padrão e pode especificar um tipo de dados SSIS diferente para colunas de entrada/saída sem afetar o desempenho para as conversões de dados necessárias.  
  
|Tipo ODBC SQL|Tipo de dados SSIS|Comentários|  
|-----------------|------------------|------------|  
|SQL_BIT|DT_BOOL||  
|SQL_TINYINT|DT_I1<br /><br />DT_UI1|Os tipos de dados SQL são mapeados para tipos sem sinal SSIS (DT_UI1, DT_UI2, DT_UI4, DT_UI8) quando o driver ODBC define o UNSIGNED_ATTRIBUTE como SQL_TRUE para esse tipo de dados SQL.|  
|SQL_SMALLINT|DT_I2<br /><br />DT_UI2|Os tipos de dados SQL são mapeados para tipos sem sinal SSIS (DT_UI1, DT_UI2, DT_UI4, DT_UI8) quando o driver ODBC define o UNSIGNED_ATTRIBUTE como SQL_TRUE para esse tipo de dados SQL.|  
|SQL_INTEGER|DT_I4<br /><br />DTUI4|Os tipos de dados SQL são mapeados para tipos sem sinal SSIS (DT_UI1, DT_UI2, DT_UI4, DT_UI8) quando o driver ODBC define o UNSIGNED_ATTRIBUTE como SQL_TRUE para esse tipo de dados SQL.|  
|SQL_BIGINT|DT_I8<br /><br />DT_UI8|Os tipos de dados SQL são mapeados para tipos sem sinal SSIS (DT_UI1, DT_UI2, DT_UI4, DT_UI8) quando o driver ODBC define o UNSIGNED_ATTRIBUTE como SQL_TRUE para esse tipo de dados SQL.|  
|SQL_DOUBLE|DT_R8|  
|SQL_FLOAT|DT_R8|  
|SQL_REAL|DT_R4|  
|SQL_NUMERIC (p,s)|DT_NUMERIC (p,s)|O tipo de dados numeric é mapeado para DT_NUMERIC quando P é maior ou igual a 38 e S é maior ou igual a 0 e S é menor que ou igual a P.|  
||DT_R8|O tipo de dados numeric é mapeado para DT_R8 quando pelo menos uma das seguintes condições é verdadeira:<br /><br />A precisão é maior que 38<br /><br />A escala é menor que zero<br /><br />A escala é maior que 38<br /><br />A escala é maior que a Precisão|  
||DT_CY|O tipo de dados numeric é mapeado para DT_CY quando declarado como um tipo de dados money.|  
|SQL_DECIMAL (p,s)|DT_NUMERIC (p,s)|O tipo de dados decimal é mapeado para DT_NUMERIC quando P é maior ou igual a 38 e S é maior ou igual a 0 e S é menor que ou igual a P.|  
||DT_R8|O tipo de dados decimal é mapeado para DT_R8 quando pelo menos uma das seguintes condições é verdadeira:<br /><br />A precisão é maior que 38<br /><br />A escala é menor que zero<br /><br />A escala é maior que 38<br /><br />A escala é maior que a Precisão|  
||DT_CY|O tipo de dados decimal é mapeado para DT_CY quando declarado como um tipo de dados money.|  
|SQL_DATE<br /><br />SQL_TYPE_DATE|DT_DBDATE|  
|SQL_TIME<br /><br />SQL_TYPE_TIME|DT_DBTIME|  
|SQL_TIMESTAMP<br /><br />SQL_TYPE_TIMESTAMP|DT_DBTIMESTAMP<br /><br />DT_DBTIMESTAMP2|Os tipos de dados SQL_TIMESTAMP serão mapeados para DT_DBTIMESTAMP2 se a escala for maior que 3. Em todos os outros casos, eles são mapeados para DT_DBTIMESTAMP.|  
|SQL_CHAR<br /><br />SQLVARCHAR|DT_STR<br /><br />DT_WSTR<br /><br />DT_TEXT<br /><br />DT_NTEXT|DT_STR será usado se o comprimento de coluna for menor ou igual a 8000 e a propriedade **ExposeStringsAsUnicode** for falsa.<br /><br />DT_WSTR será usado se o comprimento de coluna for menor ou igual a 8000 e a propriedade **ExposeStringsAsUnicode** for verdadeira.<br /><br />DT_TEXT será usado se o comprimento de coluna for maior ou igual a 8000 e a propriedade **ExposeStringsAsUnicode** for falsa.<br /><br />DT_NTEXT será usado se o comprimento de coluna for maior ou igual a 8000 e a propriedade **ExposeStringsAsUnicode** for verdadeira.|  
|SQL_LONGVARCHAR|DT_TEXT<br /><br />DT_NTEXT|DT_NTEXT será usado se a propriedade **ExposeStringsAsUnicode** for verdadeira.|  
|SQL_WCHAR<br /><br />SQL_WVARCHAR|DT_WSTR<br /><br />DT_NTEXT|DT_WSTR será usado se o comprimento de coluna for menor ou igual a 4.000.<br /><br />DT_NTEXT será usado se o comprimento de coluna for maior ou igual a 4.000.|  
|SQL_WLONGVARCHAR|DT_NTEXT|  
|SQL_BINARY|DT_BYTE<br /><br />DT_IMAGE|DT_BYTES será usado se o comprimento de coluna for menor ou igual a 8.000.<br /><br />DT_IMAGE será usado se o comprimento de coluna for maior ou igual a 8.000.|  
|SQL_LONGVARBINARY|DT_IMAGE|  
|SQL_GUID|DT_GUID|  
|SQL_INTERVAL_YEAR<br /><br />SQL_INTERVAL_MONTH<br /><br />SQL_INTERVAL_DAY<br /><br />SQL_INTERVAL_HOUR<br /><br />SQL_INTERVAL_MINUTE<br /><br />SQL_INTERVAL_SECOND<br /><br />SQL_INTERVAL_YEAR_TO_MONTH<br /><br />SQL_INTERVAL_DAY_TO_HOUR<br /><br />SQL_INTERVAL_DAY_TO_MINUTE<br /><br />SQL_INTERVAL_DAY_TO_SECOND<br /><br />SQL_INTERVAL_HOUR_TO_MINUTE<br /><br />SQL_INTERVAL_HOUR_TO_SECOND<br /><br />SQL_INTERVAL_MINUTE_TO_SECOND|DT_WSTR|  
|Tipos de dados específicos de provedor|DT_BYTES<br /><br />DT_IMAGE|DT_BYTES será usado se o comprimento de coluna for menor ou igual a 8.000.<br /><br />DT_IMAGE será usado se o comprimento de coluna for zero ou maior que 8.000.|  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Origem ODBC](../../integration-services/data-flow/odbc-source.md)  
  
-   [Destino ODBC](../../integration-services/data-flow/odbc-destination.md)  
  
 
