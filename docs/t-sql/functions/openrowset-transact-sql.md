---
title: OPENROWSET (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENROWSET_TSQL
- OPENROWSET
dev_langs:
- TSQL
helpviewer_keywords:
- data sources [SQL Server]
- OPENROWSET function
- remote data access [SQL Server], OPENROWSET
- ad hoc distributed queries
- OPENROWSET function, Transact-SQL
- OPENROWSET statement
- OLE DB data sources [SQL Server]
- ad hoc connection information
ms.assetid: f47eda43-33aa-454d-840a-bb15a031ca17
caps.latest.revision: 130
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3c23ec85299af595305a5f6d5141dbbf3ffab96d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="openrowset-transact-sql"></a>OPENROWSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inclui todas as informações de conexão exigidas para acessar dados remotos de uma fonte de dados OLE DB. Este método é uma alternativa para acessar tabelas em um servidor vinculado e se trata de um método de uso único e ad hoc para conexão e acesso a dados remotos por meio de OLE DB. Para mais referências frequentes a fontes de dados OLE DB, use servidores vinculados. Para obter mais informações, veja [Servidores vinculados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md). O `OPENROWSET` função pode ser referenciada na cláusula FROM de uma consulta como se fosse um nome de tabela. O `OPENROWSET` função também pode ser referenciada como a tabela de destino de um `INSERT`, `UPDATE`, ou `DELETE` instrução, sujeita aos recursos do provedor OLE DB. Embora a consulta pode retornar vários conjuntos de resultados, `OPENROWSET` retorna somente o primeiro deles.  
  
 `OPENROWSET`também oferece suporte a operações em massa por meio de um provedor BULK interno que permite que os dados de um arquivo para ser lidos e retornados como um conjunto de linhas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
OPENROWSET   
( { 'provider_name' , { 'datasource' ; 'user_id' ; 'password'   
   | 'provider_string' }   
   , {   [ catalog. ] [ schema. ] object   
       | 'query'   
     }   
   | BULK 'data_file' ,   
       { FORMATFILE = 'format_file_path' [ <bulk_options> ]  
       | SINGLE_BLOB | SINGLE_CLOB | SINGLE_NCLOB }  
} )   
  
<bulk_options> ::=  
   [ , CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } ]   
   [ , DATASOURCE = 'data_source_name' ]
   [ , ERRORFILE = 'file_name' ]  
   [ , ERRORFILE_DATASOURCE = 'data_source_name' ]   
   [ , FIRSTROW = first_row ]   
   [ , LASTROW = last_row ]   
   [ , MAXERRORS = maximum_errors ]   
   [ , ROWS_PER_BATCH = rows_per_batch ]  
   [ , ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) [ UNIQUE ] ]
  
   -- bulk_options related to input file format
   [ , FORMAT = 'CSV' ]
   [ , FIELDQUOTE = 'quote_characters']
   [ , FORMATFILE = 'format_file_path' ]   
```

  
## <a name="arguments"></a>Argumentos  
 '*provider_name*'  
 É uma cadeia de caracteres que representa o nome amigável (ou PROGID) do provedor OLE DB conforme especificado no registro. *provider_name* não tem valor padrão.  
  
 '*datasource*'  
 Uma constante de cadeia de caracteres que corresponder a uma fonte de dados OLE DB específica. *fonte de dados* é a propriedade DBPROP_INIT_DATASOURCE a ser passado para a interface IDBProperties do provedor para inicializar o provedor. Normalmente, essa cadeia de caracteres inclui o nome do arquivo de banco de dados, o nome de um servidor de banco de dados ou um nome que o provedor entenda para localizar o banco de dados (ou bancos de dados).  
  
 '*user_id*'  
 É uma constante de cadeia de caracteres que é o nome de usuário passado para o provedor OLE DB especificado. *USER_ID* Especifica o contexto de segurança para a conexão e é passado como propriedade DBPROP_AUTH_USERID para inicializar o provedor. *USER_ID* não pode ser um nome de logon do Microsoft Windows.  
  
 '*senha*'  
 É uma constante de cadeia de caracteres que é a senha de usuário a ser passada para o provedor OLE DB. *senha* é passado como propriedade DBPROP_AUTH_PASSWORD ao inicializar o provedor. *senha* não pode ser uma senha do Microsoft Windows.  
  
 '*provider_string*'  
 É uma cadeia de conexão específica ao provedor, que é passada na propriedade DBPROP_INIT_PROVIDERSTRING para inicializar o provedor OLE DB. *provider_string* encapsula normalmente todas as informações de conexão necessárias para inicializar o provedor. Para obter uma lista de palavras-chave reconhecidas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client, consulte [propriedades de inicialização e autorização](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
 *Catálogo*  
 É o nome do catálogo ou do banco de dados no qual reside o objeto especificado.  
  
 *esquema*  
 É o nome do esquema ou do proprietário de objeto do objeto especificado.  
  
 *objeto*  
 É o nome de objeto que identifica com exclusividade o objeto com o qual trabalhar.  
  
 '*consulta*'  
 É uma constante de cadeia de caracteres enviada ao provedor e executada por ele. A instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não processa esta consulta, mas processa resultados de consulta retornados pelo provedor, uma consulta de passagem. Consultas de passagem são úteis quando usadas em provedores que não tornam disponíveis seus dados tabulares por meio de nomes de tabelas, mas somente via linguagem de comando. Consultas de passagem têm suporte no servidor remoto, como o provedor de consulta dá suporte ao objeto de comando OLE DB e suas interfaces obrigatórias. Para obter mais informações, consulte [SQL Server Native Client &#40; OLE DB &#41; Referência](../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md).  
  
 BULK  
 Usa o provedor de conjuntos de linhas BULK para que OPENROWSET leia dados de um arquivo. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], OPENROWSET pode ler de um arquivo de dados sem carregar os dados em uma tabela de destino. Permite que você use OPENROWSET com uma instrução SELECT simples.  
  
 Os argumentos da opção BULK permitem um controle significativo sobre os pontos de início e término da leitura de dados, o modo de manipulação dos erros e o modo de interpretação dos dados. Por exemplo, você pode especificar que o arquivo de dados ser lido como um conjunto de linhas de uma linha e coluna única do tipo **varbinary**, **varchar**, ou **nvarchar**. O comportamento padrão é descrito nas descrições de argumento que se seguem.  
  
 Para obter informações sobre como usar a opção BULK, consulte "Comentários", mais adiante neste tópico. Para obter informações sobre as permissões exigidas pela opção BULK, consulte "Permissões" mais adiante, neste tópico.  
  
> [!NOTE]  
>  Quando usado para importar dados com o modelo de recuperação completa, OPENROWSET (BULK...) não otimiza o registro.  
  
 Para obter informações sobre como preparar dados para importação em massa, consulte [preparar dados para importação ou exportação em massa &#40; SQL Server &#41; ](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 '*data_file*'  
 É o caminho completo do arquivo de dados cujos dados serão copiados para a tabela de destino.   
 **Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Começando com [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1 CTP, o data_file pode ser no armazenamento de blob do Azure. Para obter exemplos, consulte [exemplos de Bulk acesso aos dados no armazenamento de BLOBs do Azure](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).
  
 \<bulk_options >  
 Especifica um ou mais argumentos para a opção BULK.  
  
 PÁGINA DE CÓDIGO = {'ACP' | 'OEM' | 'BRUTAS' | *code_page*'}  
 Especifica a página de código dos dados no arquivo de dados. Página de código é relevante apenas se os dados contiverem **char**, **varchar**, ou **texto** colunas com valores de caractere mais de 127 ou inferiores a 32.  
  
> [!NOTE]  
>  É recomendável que você especificar um nome de agrupamento para cada coluna em um arquivo de formato, exceto quando você deseja que a opção 65001 tenha prioridade sobre a especificação de página de código/agrupamento.  
  
|Valor de CODEPAGE|Description|  
|--------------------|-----------------|  
|ACP|Converte colunas de **char**, **varchar**, ou **texto** tipo de dados do ANSI /[!INCLUDE[msCoName](../../includes/msconame-md.md)] página de código do Windows (ISO 1252) para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] página de código.|  
|OEM (padrão)|Converte colunas de **char**, **varchar**, ou **texto** tipo de dados da página de código OEM do sistema para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] página de código.|  
|RAW|Nenhuma conversão ocorre de uma página de código para outra. Esta é a opção mais rápida.|  
|*code_page*|Indica a página de código de origem na qual são codificados os dados de caracteres do arquivo de dados; por exemplo, 850.<br /><br /> **\*\*Importante \* \***  versões anteriores ao [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] não oferecem suporte a página de código 65001 (codificação UTF-8).|  
  
 ERRORFILE ='*file_name*'  
 Especifica o arquivo usado para coletar linhas com erros de formatação e que não podem ser convertidas em um conjunto de linhas OLE DB. Essas linhas são copiadas do arquivo de dados para esse arquivo de erro "no estado em que se encontram".  
  
 O arquivo de erro é criado no início da execução do comando. Um erro será gerado se o arquivo já existe. Além disso, é criado um arquivo de controle com a extensão .ERROR.txt. Esse arquivo faz referência a cada linha do arquivo de erro e fornece um diagnóstico dos erros. Corrigidos os erros, os dados podem ser carregados.  
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
Começando com [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], o `error_file_path` pode estar no armazenamento de blob do Azure. 

'errorfile_data_source_name'   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
Uma fonte de dados externa nomeada está apontando para o local de armazenamento de BLOBs do Azure do arquivo de erro que conterá os erros encontrados durante a importação. Fonte de dados externa deve ser criada usando o `TYPE = BLOB_STORAGE` opção adicionada no [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).
  
 FIRSTROW =*first_row*  
 Especifica o número da primeira linha a carregar. O padrão é 1. Indica a primeira linha no arquivo de dados especificado. Os números de linhas são determinados pela contagem dos terminadores de linha. FIRSTROW tem base 1.  
  
 LASTROW =*last_row*  
 Especifica o número da última linha a ser carregada. O padrão é 0. Indica a última linha no arquivo de dados especificado.  
  
 MAXERRORS =*maximum_errors*  
 Especifica o número máximo de erros de sintaxe ou de linhas fora de conformidade, conforme definido no arquivo de formato, que podem ocorrer antes de OPENROWSET lançar uma exceção. Até que MAXERRORS seja atingido, OPENROWSET ignora as linhas inválidas, deixando de carregá-las, e as conta como erros.  
  
 O padrão para *maximum_errors* é 10.  
  
> [!NOTE]  
>  MAX_ERRORS não se aplica a restrições CHECK ou à conversão **money** e **bigint** tipos de dados.  
  
 ROWS_PER_BATCH =*rows_per_batch*  
 Especifica o número aproximado de linhas de dados no arquivo de dados. Este valor deve ser da mesma ordem que o número real de linhas.  
  
 OPENROWSET sempre importa um arquivo de dados como um único lote. No entanto, se você especificar *rows_per_batch* com um valor > 0, o processador de consultas usa o valor de *rows_per_batch* como uma dica para alocar recursos no plano de consulta.  
  
 Por padrão, ROWS_PER_BATCH é desconhecido. Especificar ROWS_PER_BATCH = 0 é o mesmo que omitir ROWS_PER_BATCH.  
  
 ORDEM ({ *coluna* [ASC | DESC]} [,...  *n*  ] [UNIQUE])  
 Uma dica opcional que especifica como os dados são classificados no arquivo de dados. Por padrão, a operação em massa presume que o arquivo de dados não está ordenado. O desempenho poderá melhorar se a ordem especificada puder ser explorada pelo otimizador de consulta para gerar um plano de consulta mais eficiente. São exemplos de quando especificar uma classificação pode ser benéfico:  
  
-   Ao inserir linhas em uma tabela que tem um índice clusterizado, na qual os dados dos conjuntos de linhas são classificados na chave do índice clusterizado.  
  
-   Ao unir o conjunto de linhas com outra tabela, cujas colunas de classificação e de união correspondam.  
  
-   Ao agregar os dados dos conjuntos de linhas pelas colunas de classificação.  
  
-   Ao usar o conjunto de linhas como tabela de origem na cláusula FROM de uma consulta, cujas colunas de classificação e de junção correspondam.  
  
 UNIQUE especifica que o arquivo de dados não tem entradas duplicadas.  
  
 Se as linhas reais do arquivo de dados não estiverem classificadas na ordem especificada, ou se a dica UNIQUE tiver sido especificada e houver chaves duplicadas, será retornado um erro.  
  
 Aliases de coluna são necessários quando se usa ORDER. A lista de aliases de coluna deve referenciar a tabela derivada que está sendo acessada pela cláusula BULK. Os nomes de coluna especificados na cláusula ORDER se referem a essa lista de aliases de coluna. Tipos de valor grande (**varchar (max)**, **nvarchar (max)**, **varbinary (max)**, e **xml**) e tipos de objeto grande (LOB) (**texto**, **ntext**, e **imagem**) colunas não podem ser especificadas.  
  
 SINGLE_BLOB  
 Retorna o conteúdo de *data_file* como um conjunto de linhas de uma linha e coluna única do tipo **varbinary (max)**.  
  
> [!IMPORTANT]  
>  Recomendamos importar apenas os dados XML que usam a opção SINGLE_BLOB, em vez de SINGLE_CLOB e SINGLE_NCLOB, porque só SINGLE_BLOB oferece suporte a todas as conversões de codificação do Windows.  
  
 SINGLE_CLOB  
 Lendo *data_file* como ASCII retorna o conteúdo como um conjunto de linhas de uma linha e coluna única do tipo **varchar (max)**, usando o agrupamento do banco de dados atual.  
  
 SINGLE_NCLOB  
 Lendo *data_file* como UNICODE, retorna o conteúdo como um conjunto de linhas de uma linha e coluna única do tipo **nvarchar (max)**, usando o agrupamento do banco de dados atual.  

### <a name="input-file-format-options"></a>Opções de formato de arquivo de entrada
  
FORMATO  **=**  'CSV'   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Especifica um arquivo de valores separados por vírgula compatível para o [RFC 4180](https://tools.ietf.org/html/rfc4180) padrão.

 FORMATFILE ='*format_file_path*'  
 Especifica o caminho completo de um arquivo de formato. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a dois tipos de arquivos de formato: XML e não XML.  
  
 É necessário um arquivo de formato para definir tipos de coluna no conjunto de resultados. A única exceção é quando SINGLE_CLOB, SINGLE_BLOB ou SINGLE_NCLOB é especificado; nesses casos, o arquivo de formato não é obrigatório.  
  
 Para obter informações sobre arquivos de formato, consulte [usar um arquivo de formato para importar dados em massa &#40; SQL Server &#41; ](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  

**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Começando com [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1 CTP, o format_file_path pode ser no armazenamento de blob do Azure. Para obter exemplos, consulte [exemplos de Bulk acesso aos dados no armazenamento de BLOBs do Azure](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).

FIELDQUOTE  **=**  'field_quote'   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Especifica um caractere que será usado como o caractere de aspas no arquivo CSV. Se não for especificado, o caractere de aspas (") será usado como o caractere de aspas conforme definido no [RFC 4180](https://tools.ietf.org/html/rfc4180) padrão.

  
## <a name="remarks"></a>Comentários  
 `OPENROWSET`pode ser usado para acessar dados remotos de fontes OLE DB dados somente quando o **DisallowAdhocAccess** opção do registro é definida explicitamente como 0 para o provedor especificado, e é a consultas distribuídas Ad Hoc opção de configuração avançada habilitado. Quando essas opções não estão definidas, o comportamento padrão não permite acesso ad hoc.  
  
 No acesso a fontes de dados OLE DB remotas, a identidade de logon das conexões confiáveis não são delegadas automaticamente do servidor no qual o cliente é conectado ao servidor que está sendo consultado. A delegação de autenticação deve ser configurada.  
  
 Serão necessários os nomes de catálogo e de esquema, se o provedor OLE DB oferecer suporte a vários catálogos e esquemas na fonte de dados especificada. Os valores para *catálogo* e *esquema* pode ser omitido quando o provedor OLE DB não oferece suporte a eles. Se o provedor oferece suporte a nomes de esquema apenas, um nome de duas partes do formulário *esquema***.** *objeto* deve ser especificado. Se o provedor oferece suporte a nomes de catálogo apenas, um nome de três partes do formulário *catálogo***.** *esquema***.** *objeto* deve ser especificado. Nomes de três partes devem ser especificados para consultas de passagem que usam o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client. Para obter mais informações, consulte [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
 `OPENROWSET`não aceita variáveis para seus argumentos.  
  
 Qualquer chamada para `OPENDATASOURCE`, `OPENQUERY`, ou `OPENROWSET` no `FROM` cláusula é avaliada separada e independentemente de qualquer chamada para essas funções usadas como o destino da atualização, mesmo se argumentos idênticos forem fornecidos às duas chamadas. Em particular, as condições de filtro ou junção aplicadas no resultado de uma dessas chamadas não têm efeito sobre os resultado da outra.  
  
## <a name="using-openrowset-with-the-bulk-option"></a>Usando OPENROWSET com a opção BULK  
 Os seguintes aperfeiçoamentos de [!INCLUDE[tsql](../../includes/tsql-md.md)] oferecem suporte à função OPENROWSET(BULK...):  
  
-   Uma cláusula FROM que é usada com `SELECT` pode chamar `OPENROWSET(BULK...)` em vez de um nome de tabela com completo `SELECT` funcionalidade.  
  
     `OPENROWSET`com o `BULK` opção requer um nome de correlação, também conhecido como uma variável de intervalo ou alias, no `FROM` cláusula. Podem ser especificados aliases de coluna. Se uma lista de aliases de coluna não for especificada, o arquivo de formato deverá ter nomes de coluna. Especificar aliases de coluna faz com que os nomes de coluna sejam substituídos no arquivo de formato; por exemplo:  
  
     `FROM OPENROWSET(BULK...) AS table_alias`  
  
     `FROM OPENROWSET(BULK...) AS table_alias(column_alias,...n)`  
>    [!IMPORTANT]  
>    Falha ao adicionar o `AS <table_alias>` resultará no erro:    
>    Msg 491, nível 16, estado 1, linha 20    
>    Um nome de correlação deve ser especificado para o conjunto de linhas em massa na cláusula from.    
  
-   Um `SELECT...FROM OPENROWSET(BULK...)` instrução consulta dados em um arquivo diretamente, sem importar os dados em uma tabela. `SELECT…FROM OPENROWSET(BULK...)`instruções também podem listar aliases de coluna em massa usando um arquivo de formato para especificar nomes de coluna e tipos de dados.  
  
-   Usando `OPENROWSET(BULK...)` como uma tabela de origem em um `INSERT` ou `MERGE` em massa de instrução importa dados de um arquivo de dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela. Para obter mais informações, consulte [importação em massa dados usando BULK INSERT ou OPENROWSET &#40; BULK... &#41; &#40; SQL Server &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md) .  
  
-   Quando o `OPENROWSET BULK` opção é usada com um `INSERT` instrução, a cláusula BULK dá suporte a dicas de tabela. Além de normal dicas de tabela, como `TABLOCK`, o `BULK` cláusula pode aceitar as seguintes dicas de tabela especializadas: `IGNORE_CONSTRAINTS` (ignora somente o `CHECK` e `FOREIGN KEY` restrições), `IGNORE_TRIGGERS`, `KEEPDEFAULTS`, e `KEEPIDENTITY`. Para obter mais informações, consulte [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Para obter informações sobre como usar `INSERT...SELECT * FROM OPENROWSET(BULK...)` consulte [importação e exportação de dados &#40; SQL Server &#41; ](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md). Para obter informações sobre quando as operações de inserção de linhas executadas por importações em massa são registradas no log de transações, veja [Pré-requisitos para log mínimo em importação em massa](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
> [!NOTE]  
>  Quando você usa `OPENROWSET`, é importante entender como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controla a representação. Para obter informações sobre considerações de segurança, consulte [importação em massa dados usando BULK INSERT ou OPENROWSET &#40; BULK... &#41; &#40; SQL Server &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="bulk-importing-sqlchar-sqlnchar-or-sqlbinary-data"></a>Importação em massa de dados SQLCHAR, SQLNCHAR ou SQLBINARY  
 OPENROWSET(BULK...) pressupõe que, se não especificado, o comprimento máximo de dados SQLCHAR, SQLNCHAR ou SQLBINARY não excede 8000 bytes. Se os dados que estão sendo importados estão em um campo de dados LOB que contenha **varchar (max)**, **nvarchar (max)**, ou **varbinary (max)** objetos que excedam 8000 bytes, você deve usar um Arquivo de formato XML que define o comprimento máximo para o campo de dados. Para especificar o comprimento máximo, edite o arquivo de formato e declare o atributo MAX_LENGTH.  
  
> [!NOTE]  
>  Um arquivo de formato gerado automaticamente não especifica o comprimento ou o comprimento máximo para um campo de LOB. No entanto, você pode editar um arquivo de formato e especificar o comprimento ou o comprimento máximo manualmente.  
  
### <a name="bulk-exporting-or-importing-sqlxml-documents"></a>Exportando ou importando documentos SQLXML em massa  
 Para exportar ou importar dados SQLXML em massa, use um dos tipos de dados a seguir em seu arquivo de formato.  
  
|Tipo de dados|Efeito|  
|---------------|------------|  
|SQLCHAR ou SQLVARYCHAR|Os dados são enviados na página de código do cliente ou na página de código implicada pelo agrupamento.|  
|SQLNCHAR ou SQLNVARCHAR|Os dados são enviados como Unicode.|  
|SQLBINARY ou SQLVARYBIN|Os dados são enviados sem qualquer conversão.|  
  
## <a name="permissions"></a>Permissões  
 `OPENROWSET`permissões são determinadas pelas permissões do nome de usuário que está sendo passado para o provedor OLE DB. Para usar o `BULK` requer a opção `ADMINISTER BULK OPERATIONS` permissão.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-openrowset-with-select-and-the-sql-server-native-client-ole-db-provider"></a>A. Usando OPENROWSET com SELECT e o provedor OLE DB SQL Server Native Client  
 O exemplo a seguir usa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB para acessar o `HumanResources.Department` tabela o [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] banco de dados no servidor remoto `Seattle1`. (Use SQLNCLI, e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fará o redirecionamento para a última versão do provedor OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.) Uma instrução `SELECT` é usada para definir o conjunto de linhas retornado. A cadeia de caracteres de provedor contém as palavras-chave `Server` e `Trusted_Connection`. Essas palavras-chave reconhecidas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client.  
  
```tsql  
SELECT a.*  
FROM OPENROWSET('SQLNCLI', 'Server=Seattle1;Trusted_Connection=yes;',  
     'SELECT GroupName, Name, DepartmentID  
      FROM AdventureWorks2012.HumanResources.Department  
      ORDER BY GroupName, Name') AS a;  
```  
  
### <a name="b-using-the-microsoft-ole-db-provider-for-jet"></a>B. Usando o Microsoft OLE DB Provider for Jet  
 O exemplo a seguir acessa a tabela `Customers` no banco de dados [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access `Northwind` via [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet.  
  
> [!NOTE]  
>  Este exemplo pressupõe que o Access esteja instalado. Para executar este exemplo, é necessário instalar o banco de dados Northwind.  
  
```tsql  
SELECT CustomerID, CompanyName  
   FROM OPENROWSET('Microsoft.Jet.OLEDB.4.0',  
      'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';  
      'admin';'',Customers);  
GO  
```  
  
### <a name="c-using-openrowset-and-another-table-in-an-inner-join"></a>C. Usando OPENROWSET e outra tabela em um INNER JOIN  
 O exemplo a seguir seleciona todos os dados do `Customers` tabela da instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `Northwind` banco de dados e o `Orders` tabela contra o acesso `Northwind` banco de dados armazenado no mesmo computador.  
  
> [!NOTE]  
>  Este exemplo pressupõe que o Access esteja instalado. Para executar este exemplo, é necessário instalar o banco de dados Northwind.  
  
```tsql  
USE Northwind  ;  
GO  
SELECT c.*, o.*  
FROM Northwind.dbo.Customers AS c   
   INNER JOIN OPENROWSET('Microsoft.Jet.OLEDB.4.0',   
   'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';'admin';'', Orders)      
   AS o   
   ON c.CustomerID = o.CustomerID ;  
GO  
```  
  
### <a name="d-using-openrowset-to-bulk-insert-file-data-into-a-varbinarymax-column"></a>D. Usando OPENROWSET para inserir dados de arquivo em massa em uma coluna varbinary(max)  
 O exemplo a seguir cria uma pequena tabela a título de demonstração e insere dados de um arquivo denominado `Text1.txt`, localizado no diretório raiz `C:`, em uma coluna `varbinary(max)`.  
  
```tsql  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTable(FileName nvarchar(60),   
  FileType nvarchar(60), Document varbinary(max));  
GO  
  
INSERT INTO myTable(FileName, FileType, Document)   
   SELECT 'Text1.txt' AS FileName,   
      '.txt' AS FileType,   
      * FROM OPENROWSET(BULK N'C:\Text1.txt', SINGLE_BLOB) AS Document;  
GO  
```  
  
### <a name="e-using-the-openrowset-bulk-provider-with-a-format-file-to-retrieve-rows-from-a-text-file"></a>E. Usando o provedor OPENROWSET BULK com um arquivo de formato para recuperar linhas de um arquivo de texto  
 O exemplo a seguir usa um arquivo de formato para recuperar linhas de um arquivo de texto delimitado por tabulação, `values.txt`, que contém os seguintes dados:  
  
```tsql  
1     Data Item 1  
2     Data Item 2  
3     Data Item 3  
```  
  
 O arquivo de formato `values.fmt` descreve as colunas em `values.txt`:  
  
```tsql  
9.0  
2  
1  SQLCHAR  0  10 "\t"        1  ID                SQL_Latin1_General_Cp437_BIN  
2  SQLCHAR  0  40 "\r\n"      2  Description        SQL_Latin1_General_Cp437_BIN  
```  
  
 Eis a consulta que recupera esses dados:  
  
```tsql  
SELECT a.* FROM OPENROWSET( BULK 'c:\test\values.txt',   
   FORMATFILE = 'c:\test\values.fmt') AS a;  
```  
  
### <a name="f-specifying-a-format-file-and-code-page"></a>F. Especificar uma página de arquivo e o código de formato  
 O exemplo a seguir mostram como usar ambas as os formato de arquivo e código de página Opções ao mesmo tempo.  
  
```tsql  
INSERT INTO MyTable SELECT a.* FROM  
OPENROWSET (BULK N'D:\data.csv', FORMATFILE =   
    'D:\format_no_collation.txt', CODEPAGE = '65001') AS a;  
```  
### <a name="g-accessing-data-from-a-csv-file-with-a-format-file"></a>G. Acesso a dados de um arquivo CSV com um arquivo de formato  
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
```tsql
SELECT *
FROM OPENROWSET(BULK N'D:\XChange\test-csv.csv',
    FORMATFILE = N'D:\XChange\test-csv.fmt', 
    FIRSTROW=2, 
    FORMAT='CSV') AS cars;  
```

### <a name="h-accessing-data-from-a-csv-file-without-a-format-file"></a>H. Acesso a dados de um arquivo CSV sem um arquivo de formato

```tsql
SELECT * FROM OPENROWSET(
   BULK 'C:\Program Files\Microsoft SQL Server\MSSQL14.CTP1_1\MSSQL\DATA\inv-2017-01-19.csv',
   SINGLE_CLOB) AS DATA;
```

### <a name="i-accessing-data-from-a-file-stored-on-azure-blob-storage"></a>I. Acesso a dados de um arquivo armazenado no armazenamento de BLOBs do Azure   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
O exemplo a seguir usa uma fonte de dados externa que aponta para um contêiner em uma conta de armazenamento do Azure e uma credencial no escopo do banco de dados criado para uma assinatura de acesso compartilhado.     

```tsql
SELECT * FROM OPENROWSET(
   BULK  'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   SINGLE_CLOB) AS DataFile;
```   
Para concluir `OPENROWSET` exemplos, incluindo a configuração de credencial e a fonte de dados externa, consulte [exemplos de Bulk acesso aos dados no armazenamento de BLOBs do Azure](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).
 
### <a name="additional-examples"></a>Exemplos adicionais  
 Para obter exemplos adicionais que mostram como usar `INSERT...SELECT * FROM OPENROWSET(BULK...)`, consulte os seguintes tópicos:  
  
-   [Exemplos de importação e exportação em massa de documentos XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Manter valores de identidade ao importar dados em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Manter valores nulos ou use os valores padrão durante a importação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Usar um arquivo de formato para importação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Importação e exportação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENQUERY &#40; Transact-SQL &#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [Funções de conjunto de linhas &#40; Transact-SQL &#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [ONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

