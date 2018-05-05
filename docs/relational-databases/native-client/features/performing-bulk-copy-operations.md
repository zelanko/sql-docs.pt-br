---
title: Executando operações de cópia em massa | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|features
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk copy [SQL Server Native Client]
- data access [SQL Server Native Client], bulk copy operations
- SQL Server Native Client, bulk copy operations
- SQLNCLI, bulk copy operations
ms.assetid: 50d8456b-e6a1-4b25-bc7e-56946ed654a7
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b62b7d320986394a0968f18e829cc9bfee3d978b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="performing-bulk-copy-operations"></a>Executando operações de cópia em massa
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  O recurso de cópia em massa do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suporta a transferência de grandes quantidades de dados de ou para uma tabela ou exibição do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os dados também podem ser transferidos com a especificação de uma instrução SELECT. É possível mover os dados entre o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e um arquivo de dados do sistema operacional, como um arquivo ASCII. O arquivo de dados pode ter diferentes formatos; o formato é definido para que a cópia em massa seja feita em um arquivo de formato. Como alternativa, os dados podem ser carregados para variáveis de programa e podem ser transferidos para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando funções e métodos de cópia em massa.  
  
 Para um aplicativo de exemplo que demonstra este recurso, consulte [em massa dados usando IRowsetFastLoad &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md).  
  
 Normalmente, um aplicativo usa o recurso de cópia em massa de uma destas maneiras:  
  
-   Faz cópia em massa a partir de uma tabela, exibição ou conjunto de resultados de uma instrução Transact-SQL para um arquivo de dados onde os dados são armazenados no mesmo formato que a tabela ou exibição.  
  
     Esse arquivo é chamado de arquivo de dados de modo nativo.  
  
-   Faz cópia em massa a partir de uma tabela, exibição ou conjunto de resultados de uma instrução Transact-SQL para um arquivo de dados onde os dados são armazenados em um formato diferente do formato da tabela ou exibição.  
  
     Nesse caso, um arquivo de formato separado é criado para definir as características (tipo de dados, posição, comprimento, terminador, e assim por diante) de cada coluna à medida que ela é armazenada no arquivo de dados. Se todas as colunas forem convertidas em um formato de caractere, o arquivo resultante será chamado de arquivo de dados do modo de caractere.  
  
-   Faz cópia em massa a partir de um arquivo de dados para uma tabela ou exibição.  
  
     Se necessário, um arquivo de formato é usado para determinar o layout do arquivo de dados.  
  
-   Faz o carregamento de dados para variáveis de programa e importa os dados para uma tabela ou exibição usando as funções de cópia em massa para executar a cópia em massa em uma linha de cada vez.  
  
 Os arquivos de dados usados pelas funções de cópia em massa não precisam ser criados por outro programa de cópia em massa. Qualquer outro sistema pode gerar um arquivo de dados e um arquivo de formato para executar a cópia em massa de definições; esses arquivos podem ser usados com um programa de cópia em massa do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para importar dados para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por exemplo, você poderia exportar dados de uma planilha em um arquivo delimitado por tabulação, criar um arquivo de formato descrevendo o arquivo delimitado por tabulação e usar um programa de cópia em massa para importar rapidamente os dados para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os arquivos de dados gerados pela cópia em massa também podem ser importados para outros aplicativos. Por exemplo, você poderia usar as funções de cópia em massa para exportar dados de uma tabela ou exibição para um arquivo delimitado por tabulação que poderia, por sua vez, ser carregado para a planilha.  
  
 Os aplicativos de codificação para programadores que usam funções de cópia em massa deveriam seguir as regras gerais para garantir o bom desempenho dessas funções. Para obter mais informações sobre o suporte para operações de cópia em massa em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [importação em massa e exportação de dados &#40;SQL Server&#41;](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Um UDT (tipo definido pelo usuário) CLR deve ser associado como dados binários. Mesmo se um arquivo de formato especificar SQLCHAR como o tipo de dados para uma coluna UDT de destino, o utilitário BCP interpretará os dados como binários.  
  
 Não use SET FMTONLY OFF com operações de cópia em massa. SET FMTONLY OFF pode fazer sua operação de cópia em massa falhar ou gerar resultados inesperados.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provedor OLE DB do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client implementa dois métodos para executar operações de cópia em massa com um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados. O primeiro método envolve o uso o [IRowsetFastLoad](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) interface para operações de cópia em massa baseadas em memória; e o segundo envolve o uso de [IBCPSession](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md) interface para operações de cópia em massa baseadas em arquivo.  
  
### <a name="using-memory-based-bulk-copy-operations"></a>Usando operações de cópia em massa baseadas em memória  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB provider implementa o **IRowsetFastLoad** interface para expor suporte para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] operações de cópia em massa baseadas em memória. O **IRowsetFastLoad** interface implementa o [IRowsetFastLoad:: Commit](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md) e [IRowsetFastLoad:: Insertrow](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-insertrow-ole-db.md) métodos.  
  
#### <a name="enabling-a-session-for-irowsetfastload"></a>Habilitando uma sessão para IRowsetFastLoad  
 O consumidor notifica o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client sobre sua necessidade de executar uma cópia em massa, definindo a propriedade de fonte de dados específica do provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client SSPROP_ENABLEFASTLOAD como VARIANT_TRUE. Com o conjunto de propriedades na fonte de dados, o consumidor cria uma sessão de provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A nova sessão permite que o consumidor acesse a **IRowsetFastLoad** interface.  
  
> [!NOTE]  
>  Se o **IDataInitialize** interface é usada para inicializar a fonte de dados e, em seguida, é necessário definir a propriedade SSPROP_IRowsetFastLoad no *rgPropertySets* parâmetro o  **IOpenRowset:: OPENROWSET** método; caso contrário, a chamada para o **OpenRowset** método retornará E_NOINTERFACE.  
  
 Habilitar uma sessão para a cópia em massa restringe o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para interfaces na sessão. Uma sessão habilitada para cópia em massa expõe apenas as seguintes interfaces:  
  
-   **IDBSchemaRowset**  
  
-   **IGetDataSource**  
  
-   **IOpenRowset**  
  
-   **ISupportErrorInfo**  
  
-   **ITransactionJoin**  
  
 Para desabilitar a criação de conjuntos de linhas habilitados para cópia em massa e fazer com que a sessão do provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client seja revertida para o processamento padrão, redefina SSPROP_ENABLEFASTLOAD como VARIANT_FALSE.  
  
#### <a name="irowsetfastload-rowsets"></a>Conjuntos de linhas IRowsetFastLoad  
 Os conjuntos de linhas de cópia em massa do provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client são somente gravação, mas eles expõe interfaces que permitem que o consumidor determine a estrutura de uma tabela [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. As seguintes interfaces são expostas em um conjunto de linhas do provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client habilitado para cópia em massa:  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
-   **IColumnsRowset**  
  
-   **IConvertType**  
  
-   **IRowsetFastLoad**  
  
-   **IRowsetInfo**  
  
-   **ISupportErrorInfo**  
  
 As propriedades específicas de provedor SSPROP_FASTLOADOPTIONS, SSPROP_FASTLOADKEEPNULLS e SSPROP_FASTLOADKEEPIDENTITY controlam o comportamento de um conjunto de linhas de cópia em massa do provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. As propriedades são especificadas no *rgProperties* membro de um * rgPropertySets ***IOpenRowset**de parâmetro.  
  
|ID da propriedade|Description|  
|-----------------|-----------------|  
|SSPROP_FASTLOADKEEPIDENTITY|Coluna: Não<br /><br /> Leitura/gravação: leitura/gravação<br /><br /> Tipo: VT_BOOL<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: Mantém valores de identidade fornecidos pelo consumidor.<br /><br /> VARIANT_FALSE: Valores para uma coluna de identidade na tabela [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são gerados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Qualquer valor associado a coluna é ignorada pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client.<br /><br /> VARIANT_TRUE: O consumidor associa um acessador fornecendo um valor para uma coluna de identidade [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A propriedade identity não está disponível em colunas que aceitam valores NULL, para que o consumidor fornece um valor exclusivo em cada **IRowsetFastLoad:: Insert** chamar.|  
|SSPROP_FASTLOADKEEPNULLS|Coluna: Não<br /><br /> Leitura/gravação: leitura/gravação<br /><br /> Tipo: VT_BOOL<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: Mantém valores NULL para colunas com uma restrição DEFAULT. Só afeta colunas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que aceitam valores NULL e que têm uma restrição DEFAULT aplicada.<br /><br /> VARIANT_FALSE: O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] insere o valor padrão para a coluna quando o consumidor do provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client insere uma linha que contém valores NULL para a coluna.<br /><br /> VARIANT_TRUE: O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] insere NULL para o valor da coluna quando o consumidor do provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client insere uma linha que contém valores NULL para a coluna.|  
|SSPROP_FASTLOADOPTIONS|Coluna: Não<br /><br /> Leitura/gravação: leitura/gravação<br /><br /> Tipo: VT_BSTR<br /><br /> Padrão: nenhum<br /><br /> Descrição: Esta propriedade é igual a **-h** "*dica*[,... *n*] "opção do **bcp** utilitário. A cadeia de caracteres a seguir pode ser usada como opção na cópia em massa de dados para uma tabela.<br /><br /> **ORDER**(*column*[**ASC** &#124; **DESC**][,... *n*]): ordem de classificação dos dados no arquivo de dados. O desempenho da operação de cópia em massa é aprimorado se o arquivo de dados que está sendo carregado for classificado de acordo com o índice clusterizado na tabela.<br /><br /> **ROWS_PER_BATCH** = *bb*: número de linhas de dados por lote (como *bb*). O servidor otimiza o carregamento em massa de acordo com o valor *bb*. Por padrão, **ROWS_PER_BATCH** é desconhecido.<br /><br /> **KILOBYTES_PER_BATCH** = *cc*: número de quilobytes (KB) de dados por lote (como cc). Por padrão, **KILOBYTES_PER_BATCH** é desconhecido.<br /><br /> **TABLOCK**: um bloqueio de nível de tabela é adquirido para a duração da operação de cópia em massa. Essa opção melhora significativamente o desempenho porque manter um bloqueio apenas durante a operação de cópia em massa reduz a contenção de bloqueios na tabela. Uma tabela pode ser carregada por vários clientes simultaneamente se a tabela não tiver nenhum índice e **TABLOCK** for especificado. Por padrão, o comportamento de bloqueio é determinado pela opção de tabela **bloqueio de tabela em carregamento em massa**.<br /><br /> **CHECK_CONSTRAINTS**: quaisquer restrições no *table_name* são verificadas durante a operação de cópia em massa. Por padrão, as restrições são ignoradas.<br /><br /> **FIRE_TRIGGER**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa o controle de versão de linha para gatilhos e armazena as versões de linha no repositório de versão no **tempdb**. Portanto, as otimizações de registro em massa estão disponíveis até mesmo quando os gatilhos estão habilitados. Antes da importação em massa de um lote com um grande número de linhas com gatilhos habilitados, você pode precisar expandir o tamanho de **tempdb**.|  
  
### <a name="using-file-based-bulk-copy-operations"></a>Usando operações de cópia em massa baseadas em arquivo  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB provider implementa o **IBCPSession** interface para expor suporte para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] operações de cópia em massa baseadas em arquivo. O **IBCPSession** interface implementa o [ibcpsession:: BCPColFmt](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md), [ibcpsession:: BCPColumns](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md), [ibcpsession:: Bcpcontrol](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md), [IBCPSession::BCPDone](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpdone-ole-db.md), [ibcpsession:: BCPExec](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpexec-ole-db.md), [ibcpsession:: BCPInit](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md), [ibcpsession:: Bcpreadfmt](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md), e [ibcpsession:: Bcpwritefmt](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)métodos.  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC do SQL Server Native Client  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client mantém o mesmo suporte para operações de cópia em massa que o das versões anteriores do driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter informações sobre operações de cópia em massa usando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o driver ODBC Native Client, consulte [executando operações de cópia em massa &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Propriedades da fonte de dados &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)   
 [Importação e exportação de dados &#40;em massa SQL Server&#41;](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [IRowsetFastLoad &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)   
 [IBCPSession &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [Otimizando o desempenho da importação em massa](http://msdn.microsoft.com/library/ms190421\(SQL.105\).aspx)  
  
  
