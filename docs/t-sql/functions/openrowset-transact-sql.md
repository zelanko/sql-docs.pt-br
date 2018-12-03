---
title: OPENROWSET (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: db0fbc2125ca748f0426eea95c4c1a059e5b67f5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52509961"
---
# <a name="openrowset-transact-sql"></a>OPENROWSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Inclui todas as informações de conexão exigidas para acessar dados remotos de uma fonte de dados OLE DB. Este método é uma alternativa para acessar tabelas em um servidor vinculado e se trata de um método de uso único e ad hoc para conexão e acesso a dados remotos por meio de OLE DB. Para mais referências frequentes a fontes de dados OLE DB, use servidores vinculados. Para obter mais informações, veja [Servidores vinculados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md). A função `OPENROWSET` pode ser referenciada na cláusula FROM de uma consulta como se fosse um nome de tabela. A função `OPENROWSET` também pode ser referenciada como a tabela de destino de uma instrução `INSERT`, `UPDATE` ou `DELETE`, sujeito às funcionalidades do Provedor OLE DB. Embora a consulta possa retornar vários conjuntos de resultados, `OPENROWSET` retorna somente o primeiro deles.  
  
 `OPENROWSET` também é compatível com a operações em massa por meio de um provedor BULK interno que permite que dados de um arquivo sejam lidos e retornados como um conjunto de linhas.  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 Uma constante de cadeia de caracteres que corresponder a uma fonte de dados OLE DB específica. *datasource* é a propriedade DBPROP_INIT_DATASOURCE a ser passada para a interface IDBProperties do provedor para inicializar o provedor. Normalmente, essa cadeia de caracteres inclui o nome do arquivo de banco de dados, o nome de um servidor de banco de dados ou um nome que o provedor entenda para localizar o banco de dados (ou bancos de dados).  
  
 '*user_id*'  
 É uma constante de cadeia de caracteres que é o nome de usuário passado para o provedor OLE DB especificado. *user_id* especifica o contexto de segurança para a conexão e é passado como a propriedade DBPROP_AUTH_USERID para inicializar o provedor. *user_id* não pode ser um nome de logon do Microsoft Windows.  
  
 '*password*'  
 É uma constante de cadeia de caracteres que é a senha de usuário a ser passada para o provedor OLE DB. *password* é passada pela propriedade DBPROP_AUTH_PASSWORD ao inicializar o provedor. *password* não pode ser uma senha do Microsoft Windows.  
  
 '*provider_string*'  
 É uma cadeia de conexão específica ao provedor, que é passada na propriedade DBPROP_INIT_PROVIDERSTRING para inicializar o provedor OLE DB. *provider_string* encapsula normalmente todas as informações de conexão necessárias para inicializar o provedor. Para obter uma lista de palavras-chave reconhecidas pelo Provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, consulte [Propriedades de inicialização e autorização](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
 *catalog*  
 É o nome do catálogo ou do banco de dados no qual reside o objeto especificado.  
  
 *schema*  
 É o nome do esquema ou do proprietário de objeto do objeto especificado.  
  
 *object*  
 É o nome de objeto que identifica com exclusividade o objeto com o qual trabalhar.  
  
 '*query*'  
 É uma constante de cadeia de caracteres enviada ao provedor e executada por ele. A instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não processa esta consulta, mas processa resultados de consulta retornados pelo provedor, uma consulta de passagem. Consultas de passagem são úteis quando usadas em provedores que não tornam disponíveis seus dados tabulares por meio de nomes de tabelas, mas somente via linguagem de comando. Há compatibilidade com consultas de passagem no servidor remoto, desde que o provedor de consulta dê suporte ao objeto Command do OLE DB e a suas interfaces obrigatórias. Para obter mais informações, consulte [Referência do SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md).  
  
 BULK  
 Usa o provedor de conjuntos de linhas BULK para que OPENROWSET leia dados de um arquivo. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], OPENROWSET pode ler de um arquivo de dados sem carregar os dados em uma tabela de destino. Permite que você use OPENROWSET com uma instrução SELECT simples.  

> [!IMPORTANT]
> O Banco de Dados SQL do Azure não oferece suporte à leitura de arquivos do Windows.
  
 Os argumentos da opção BULK permitem um controle significativo sobre os pontos de início e término da leitura de dados, o modo de manipulação dos erros e o modo de interpretação dos dados. Por exemplo, você pode especificar que o arquivo de dados seja lido como uma única linha, um conjunto de linhas de coluna única do tipo **varbinary**, **varchar** ou **nvarchar**. O comportamento padrão é descrito nas descrições de argumento que se seguem.  
  
 Para obter informações sobre como usar a opção BULK, consulte "Comentários", mais adiante neste tópico. Para obter informações sobre as permissões exigidas pela opção BULK, consulte "Permissões" mais adiante, neste tópico.  
  
> [!NOTE]  
>  Quando usado para importar dados com o modelo de recuperação completa, OPENROWSET (BULK...) não otimiza o registro.  
  
 Para obter informações sobre como preparar dados para importação em massa, consulte [Preparar dados para exportação ou importação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 '*data_file*'  
 É o caminho completo do arquivo de dados cujos dados serão copiados para a tabela de destino.   
 **Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
A partir do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1, o data_file pode estar localizado no Armazenamento de Blobs do Azure. Para obter exemplos, consulte [Exemplos de acesso em massa a dados no Armazenamento de Blobs do Azure](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).

> [!IMPORTANT]
> O Banco de Dados SQL do Azure não oferece suporte à leitura de arquivos do Windows.
  
 \<bulk_options>  
 Especifica um ou mais argumentos para a opção BULK.  
  
 CODEPAGE = { 'ACP'| 'OEM'| 'RAW'| '*code_page*' }  
 Especifica a página de código dos dados no arquivo de dados. CODEPAGE apenas será relevante se os dados contiverem colunas **char**, **varchar** ou **text** com valores de caractere maiores que 127 ou menores que 32.  

> [!IMPORTANT]
> CODEPAGE não é uma opção compatível com o Linux.

> [!NOTE]  
>  Recomendamos a especificação de um nome de ordenação para cada coluna em um arquivo de formato, exceto quando você desejar que a opção 65001 tenha prioridade sobre a especificação de ordenação/página de código.  
  
|Valor de CODEPAGE|Descrição|  
|--------------------|-----------------|  
|ACP|Converte colunas do tipo de dados **char**, **varchar** ou **text** da página de código do ANSI/[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows (ISO 1252) na página de código do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|OEM (padrão)|Converte colunas do tipo de dados **char**, **varchar** ou **text** da página de código de OEM do sistema na página de código do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|RAW|Não ocorre nenhuma conversão de uma página de código em outra. Esta é a opção mais rápida.|  
|*code_page*|Indica a página de código de origem na qual são codificados os dados de caracteres do arquivo de dados; por exemplo, 850.<br /><br /> **&#42;&#42; Importante &#42;&#42;** As versões anteriores à [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] não são compatíveis com a página de código 65001 (codificação UTF-8).|  
  
 ERRORFILE ='*file_name*'  
 Especifica o arquivo usado para coletar linhas com erros de formatação e que não podem ser convertidas em um conjunto de linhas OLE DB. Essas linhas são copiadas do arquivo de dados para esse arquivo de erro "no estado em que se encontram".  
  
 O arquivo de erro é criado no início da execução do comando. Um erro será gerado se o arquivo já existir. Além disso, é criado um arquivo de controle com a extensão .ERROR.txt. Esse arquivo faz referência a cada linha do arquivo de erro e fornece um diagnóstico dos erros. Corrigidos os erros, os dados podem ser carregados.  
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
Começando pelo [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], o `error_file_path` pode estar no Armazenamento de Blobs do Azure. 

'errorfile_data_source_name'   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
É uma fonte de dados externa nomeada que aponta para o local de Armazenamento de Blobs do Azure do arquivo de erro que conterá os erros encontrados durante a importação. A fonte de dados externa deve ser criada usando a opção `TYPE = BLOB_STORAGE` adicionada no [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).
  
 FIRSTROW =*first_row*  
 Especifica o número da primeira linha a carregar. O padrão é 1. Indica a primeira linha no arquivo de dados especificado. Os números de linhas são determinados pela contagem dos terminadores de linha. FIRSTROW tem base 1.  
  
 LASTROW =*last_row*  
 Especifica o número da última linha a ser carregada. O padrão é 0. Indica a última linha no arquivo de dados especificado.  
  
 MAXERRORS =*maximum_errors*  
 Especifica o número máximo de erros de sintaxe ou de linhas fora de conformidade, conforme definido no arquivo de formato, que podem ocorrer antes de OPENROWSET lançar uma exceção. Até que MAXERRORS seja atingido, OPENROWSET ignora as linhas inválidas, deixando de carregá-las, e as conta como erros.  
  
 O padrão de *maximum_errors* é 10.  
  
> [!NOTE]  
>  MAX_ERRORS não se aplica a restrições CHECK ou à conversão dos tipos de dados **money** e **bigint**.  
  
 ROWS_PER_BATCH =*rows_per_batch*  
 Especifica o número aproximado de linhas de dados no arquivo de dados. Este valor deve ser da mesma ordem que o número real de linhas.  
  
 OPENROWSET sempre importa um arquivo de dados como um único lote. No entanto, se você especificar *rows_per_batch* com um valor > 0, o processador de consulta usará o valor de *rows_per_batch* como dica para alocar recursos no plano de consulta.  
  
 Por padrão, ROWS_PER_BATCH é desconhecido. Especificar ROWS_PER_BATCH = 0 é o mesmo que omitir ROWS_PER_BATCH.  
  
 ORDER ( { *column* [ ASC | DESC ] } [ ,... *n* ] [ UNIQUE ] )  
 Uma dica opcional que especifica como os dados são classificados no arquivo de dados. Por padrão, a operação em massa presume que o arquivo de dados não está ordenado. O desempenho poderá melhorar se a ordem especificada puder ser explorada pelo otimizador de consulta para gerar um plano de consulta mais eficiente. São exemplos de quando especificar uma classificação pode ser benéfico:  
  
-   Ao inserir linhas em uma tabela que tem um índice clusterizado, na qual os dados dos conjuntos de linhas são classificados na chave do índice clusterizado.  
  
-   Ao unir o conjunto de linhas com outra tabela, cujas colunas de classificação e de união correspondam.  
  
-   Ao agregar os dados dos conjuntos de linhas pelas colunas de classificação.  
  
-   Ao usar o conjunto de linhas como tabela de origem na cláusula FROM de uma consulta, cujas colunas de classificação e de junção correspondam.  
  
 UNIQUE especifica que o arquivo de dados não tem entradas duplicadas.  
  
 Se as linhas reais do arquivo de dados não estiverem classificadas na ordem especificada, ou se a dica UNIQUE tiver sido especificada e houver chaves duplicadas, será retornado um erro.  
  
 Aliases de coluna são necessários quando se usa ORDER. A lista de aliases de coluna deve referenciar a tabela derivada que está sendo acessada pela cláusula BULK. Os nomes de coluna especificados na cláusula ORDER se referem a essa lista de aliases de coluna. Tipos de valor grande (**varchar(max)**, **nvarchar(max)**, **varbinary(max)** e **xml**) e colunas de tipos LOB (objeto grande) (**text**, **ntext** e **image**) não podem ser especificados.  
  
 SINGLE_BLOB  
 Retorna o conteúdo de *data_file* como um conjunto de linhas de linha e coluna únicas do tipo **varbinary(max)**.  
  
> [!IMPORTANT]  
>  Recomendamos importar apenas os dados XML que usam a opção SINGLE_BLOB, em vez de SINGLE_CLOB e SINGLE_NCLOB, porque só SINGLE_BLOB oferece suporte a todas as conversões de codificação do Windows.  
  
 SINGLE_CLOB  
 A leitura de *data_file* como ASCII retorna o conteúdo como um conjunto de linhas de linha e coluna únicas do tipo **varchar(max)**, usando a ordenação do banco de dados atual.  
  
 SINGLE_NCLOB  
 A leitura de *data_file* como UNICODE retorna o conteúdo como um conjunto de linhas de linha e coluna únicas do tipo **nvarchar(max)**, usando a ordenação do banco de dados atual.  

### <a name="input-file-format-options"></a>Opções de formato de arquivo de entrada
  
FORMAT **=** 'CSV'   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Especifica um arquivo de valores separados por vírgula em conformidade com o padrão [RFC 4180](https://tools.ietf.org/html/rfc4180).

 FORMATFILE ='*format_file_path*'  
 Especifica o caminho completo de um arquivo de formato. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a dois tipos de arquivos de formato: XML e não XML.  
  
 É necessário um arquivo de formato para definir tipos de coluna no conjunto de resultados. A única exceção é quando SINGLE_CLOB, SINGLE_BLOB ou SINGLE_NCLOB é especificado; nesses casos, o arquivo de formato não é obrigatório.  
  
 Para obter informações sobre arquivos de formato, consulte [Usar um arquivo de formato para importar dados em massa &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  

**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Começando com o [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1, o format_file_path pode estar localizado no Armazenamento de Blobs do Azure. Para obter exemplos, consulte [Exemplos de acesso em massa a dados no Armazenamento de Blobs do Azure](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).

FIELDQUOTE **=** 'field_quote'   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Especifica um caractere que será usado como o caractere de aspas no arquivo CSV. Se não for especificado, o caractere de aspas (") será usado como o caractere de aspas, conforme definido no padrão [RFC 4180](https://tools.ietf.org/html/rfc4180).

  
## <a name="remarks"></a>Remarks  
 `OPENROWSET` pode ser usado para acessar dados remotos de fontes de dados OLE DB somente quando a opção do Registro **DisallowAdhocAccess** está definida explicitamente como 0 para o provedor especificado, e a opção de configuração avançada Consultas Distribuídas Ad Hoc está habilitada. Quando essas opções não estão definidas, o comportamento padrão não permite acesso ad hoc.  
  
 No acesso a fontes de dados OLE DB remotas, a identidade de logon das conexões confiáveis não são delegadas automaticamente do servidor no qual o cliente é conectado ao servidor que está sendo consultado. A delegação de autenticação deve ser configurada.  
  
 Serão necessários os nomes de catálogo e de esquema, se o provedor OLE DB oferecer suporte a vários catálogos e esquemas na fonte de dados especificada. Os valores de _catalog_ e )_schema_ poderão ser omitidos quando o provedor OLE DB não for compatível com eles. Se o provedor for compatível apenas com nomes de esquema, um nome de duas partes no formato _schema_**.**_object_ deverá ser especificado. Se o provedor for compatível apenas com nomes de catálogo, um nome de três partes no formato _catalog_**.**_schema_**.**_object_ deverá ser especificado. Devem ser especificados nomes de três partes para consultas de passagem que usam o Provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Para obter mais informações, consulte [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
 `OPENROWSET` não aceita variáveis para seus argumentos.  
  
 Qualquer chamada a `OPENDATASOURCE`, `OPENQUERY` ou `OPENROWSET` na cláusula `FROM` é avaliada separada e independentemente de qualquer chamada a essas funções usadas como o destino da atualização, mesmo se argumentos idênticos forem fornecidos às duas chamadas. Em particular, as condições de filtro ou junção aplicadas no resultado de uma dessas chamadas não têm efeito sobre os resultado da outra.  
  
## <a name="using-openrowset-with-the-bulk-option"></a>Usando OPENROWSET com a opção BULK  
 Os seguintes aperfeiçoamentos de [!INCLUDE[tsql](../../includes/tsql-md.md)] oferecem suporte à função OPENROWSET(BULK...):  
  
-   Uma cláusula FROM que é usada com `SELECT` pode chamar `OPENROWSET(BULK...)` em vez de um nome de tabela, com funcionalidade completa de `SELECT`.  
  
     `OPENROWSET` com a opção `BULK` exige um nome de correlação, também conhecido como variável ou alias de intervalo, na cláusula `FROM`. Podem ser especificados aliases de coluna. Se uma lista de aliases de coluna não for especificada, o arquivo de formato deverá ter nomes de coluna. Especificar aliases de coluna faz com que os nomes de coluna sejam substituídos no arquivo de formato; por exemplo:  
  
     `FROM OPENROWSET(BULK...) AS table_alias`  
  
     `FROM OPENROWSET(BULK...) AS table_alias(column_alias,...n)`  
>    [!IMPORTANT]  
>    A falha ao adicionar o `AS <table_alias>` resultará no erro:    
>    Mensagem 491, Nível 16, Estado 1, Linha 20    
>    Um nome de correlação deve ser especificado para o conjunto de linhas em massa na cláusula from.    
  
-   Uma instrução `SELECT...FROM OPENROWSET(BULK...)` consulta diretamente os dados em um arquivo, sem importá-los para uma tabela. As instruções `SELECT...FROM OPENROWSET(BULK...)` também podem listar aliases de colunas em massa, usando um formato de arquivo para especificar nomes de coluna, além de tipos de dados.  
  
-   O uso de `OPENROWSET(BULK...)` como uma tabela de origem em uma instrução `INSERT` ou `MERGE` importa dados em massa de um arquivo de dados para uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Importar dados em massa usando BULK INSERT ou OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
-   Quando a opção `OPENROWSET BULK` for usada com uma instrução `INSERT`, a cláusula BULK será compatível com dicas de tabela. Além de dicas de tabela normais, como `TABLOCK`, a cláusula `BULK` pode aceitar as seguintes dicas de tabela especializadas: `IGNORE_CONSTRAINTS` (ignora somente as restrições `CHECK` e `FOREIGN KEY`), `IGNORE_TRIGGERS`, `KEEPDEFAULTS` e `KEEPIDENTITY`. Para obter mais informações, consulte [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Para obter informações sobre como usar instruções `INSERT...SELECT * FROM OPENROWSET(BULK...)`, consulte [Importação e exportação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md). Para obter informações sobre quando as operações de inserção de linhas executadas por importações em massa são registradas no log de transações, veja [Pré-requisitos para log mínimo em importação em massa](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
> [!NOTE]  
>  Ao usar `OPENROWSET`, é importante entender como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuida da representação. Para obter informações sobre considerações sobre segurança, consulte [Importação em massa de dados usando BULK INSERT ou OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="bulk-importing-sqlchar-sqlnchar-or-sqlbinary-data"></a>Importação em massa de dados SQLCHAR, SQLNCHAR ou SQLBINARY  
 OPENROWSET(BULK...) pressupõe que, se não especificado, o comprimento máximo de dados SQLCHAR, SQLNCHAR ou SQLBINARY não excede 8000 bytes. Se os dados importados estiverem em um campo de dados LOB que contém objetos **varchar(max)**, **nvarchar(max)** ou **varbinary(max)** que excedem 8.000 bytes, será necessário usar um arquivo de formato XML que define o tamanho máximo para o campo de dados. Para especificar o comprimento máximo, edite o arquivo de formato e declare o atributo MAX_LENGTH.  
  
> [!NOTE]  
>  Um arquivo de formato gerado automaticamente não especifica o comprimento ou o comprimento máximo para um campo de LOB. No entanto, você pode editar um arquivo de formato e especificar o comprimento ou o comprimento máximo manualmente.  
  
### <a name="bulk-exporting-or-importing-sqlxml-documents"></a>Exportando ou importando documentos SQLXML em massa  
 Para exportar ou importar dados SQLXML em massa, use um dos tipos de dados a seguir em seu arquivo de formato.  
  
|Tipo de dados|Efeito|  
|---------------|------------|  
|SQLCHAR ou SQLVARYCHAR|Os dados são enviados na página de código do cliente ou na página de código implicada pela ordenação.|  
|SQLNCHAR ou SQLNVARCHAR|Os dados são enviados como Unicode.|  
|SQLBINARY ou SQLVARYBIN|Os dados são enviados sem qualquer conversão.|  
  
## <a name="permissions"></a>Permissões  
 As permissões `OPENROWSET` são determinadas pelas permissões do nome de usuário que está sendo passado ao Provedor OLE DB. Para usar a opção `BULK`, é necessário ter a permissão `ADMINISTER BULK OPERATIONS`.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-openrowset-with-select-and-the-sql-server-native-client-ole-db-provider"></a>A. Usando OPENROWSET com SELECT e o provedor OLE DB SQL Server Native Client  
 O exemplo a seguir usa o Provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para acessar a tabela `HumanResources.Department` do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] no servidor remoto `Seattle1`. (Use SQLNCLI, e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fará o redirecionamento para a última versão do provedor OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.) Uma instrução `SELECT` é usada para definir o conjunto de linhas retornado. A cadeia de caracteres de provedor contém as palavras-chave `Server` e `Trusted_Connection`. Essas palavras-chave são reconhecidas pelo Provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
```sql  
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
  
```sql  
SELECT CustomerID, CompanyName  
   FROM OPENROWSET('Microsoft.Jet.OLEDB.4.0',  
      'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';  
      'admin';'',Customers);  
GO  
```  
> [!IMPORTANT]
> O Banco de Dados SQL do Azure não oferece suporte à leitura de arquivos do Windows.
  
### <a name="c-using-openrowset-and-another-table-in-an-inner-join"></a>C. Usando OPENROWSET e outra tabela em um INNER JOIN  
 O exemplo a seguir seleciona todos os dados da tabela `Customers` da instância local do banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `Northwind` e da tabela `Orders` do banco de dados `Northwind` do Access armazenado no mesmo computador.  
  
> [!NOTE]  
>  Este exemplo pressupõe que o Access esteja instalado. Para executar este exemplo, é necessário instalar o banco de dados Northwind.  
  
```sql  
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

> [!IMPORTANT]
> O Banco de Dados SQL do Azure não oferece suporte à leitura de arquivos do Windows.

  
### <a name="d-using-openrowset-to-bulk-insert-file-data-into-a-varbinarymax-column"></a>D. Usando OPENROWSET para inserir dados de arquivo em massa em uma coluna varbinary(max)  
 O exemplo a seguir cria uma pequena tabela a título de demonstração e insere dados de um arquivo denominado `Text1.txt`, localizado no diretório raiz `C:`, em uma coluna `varbinary(max)`.  
  
```sql  
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

> [!IMPORTANT]
> O Banco de Dados SQL do Azure não oferece suporte à leitura de arquivos do Windows.
  

### <a name="e-using-the-openrowset-bulk-provider-with-a-format-file-to-retrieve-rows-from-a-text-file"></a>E. Usando o provedor OPENROWSET BULK com um arquivo de formato para recuperar linhas de um arquivo de texto  
 O exemplo a seguir usa um arquivo de formato para recuperar linhas de um arquivo de texto delimitado por tabulação, `values.txt`, que contém os seguintes dados:  
  
```sql  
1     Data Item 1  
2     Data Item 2  
3     Data Item 3  
```  
  
 O arquivo de formato `values.fmt` descreve as colunas em `values.txt`:  
  
```sql  
9.0  
2  
1  SQLCHAR  0  10 "\t"        1  ID                SQL_Latin1_General_Cp437_BIN  
2  SQLCHAR  0  40 "\r\n"      2  Description        SQL_Latin1_General_Cp437_BIN  
```  
  
 Eis a consulta que recupera esses dados:  
  
```sql  
SELECT a.* FROM OPENROWSET( BULK 'c:\test\values.txt',   
   FORMATFILE = 'c:\test\values.fmt') AS a;  
```  

> [!IMPORTANT]
> O Banco de Dados SQL do Azure não oferece suporte à leitura de arquivos do Windows.
  

### <a name="f-specifying-a-format-file-and-code-page"></a>F. Especificando um arquivo de formato e uma página de código  
 O exemplo a seguir mostra como usar as opções de arquivo de formato e página de código ao mesmo tempo.  
  
```sql  
INSERT INTO MyTable SELECT a.* FROM  
OPENROWSET (BULK N'D:\data.csv', FORMATFILE =   
    'D:\format_no_collation.txt', CODEPAGE = '65001') AS a;  
```  
### <a name="g-accessing-data-from-a-csv-file-with-a-format-file"></a>G. Acessando dados de um arquivo CSV com um arquivo de formato  
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
```sql
SELECT *
FROM OPENROWSET(BULK N'D:\XChange\test-csv.csv',
    FORMATFILE = N'D:\XChange\test-csv.fmt', 
    FIRSTROW=2, 
    FORMAT='CSV') AS cars;  
```

> [!IMPORTANT]
> O Banco de Dados SQL do Azure não oferece suporte à leitura de arquivos do Windows.


### <a name="h-accessing-data-from-a-csv-file-without-a-format-file"></a>H. Acessando dados de um arquivo CSV sem um arquivo de formato

```sql
SELECT * FROM OPENROWSET(
   BULK 'C:\Program Files\Microsoft SQL Server\MSSQL14.CTP1_1\MSSQL\DATA\inv-2017-01-19.csv',
   SINGLE_CLOB) AS DATA;
```

> [!IMPORTANT]
> O Banco de Dados SQL do Azure não oferece suporte à leitura de arquivos do Windows.


### <a name="i-accessing-data-from-a-file-stored-on-azure-blob-storage"></a>I. Acessando dados de um arquivo armazenado no Armazenamento de Blobs do Azure   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
O exemplo a seguir usa uma fonte de dados externa que aponta para um contêiner em uma conta de armazenamento do Azure e uma credencial no escopo do banco de dados criada para uma Assinatura de Acesso Compartilhado.     

```sql
SELECT * FROM OPENROWSET(
   BULK  'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   SINGLE_CLOB) AS DataFile;
```   
Para obter exemplos de `OPENROWSET` completos, incluindo a configuração da credencial e da fonte de dados externa, consulte [Exemplos de acesso em massa a dados no Armazenamento de Blobs do Azure](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).
 
### <a name="additional-examples"></a>Exemplos adicionais  
 Para obter outros exemplos que mostram como usar `INSERT...SELECT * FROM OPENROWSET(BULK...)`, consulte os seguintes tópicos:  
  
-   [Exemplos de importação e exportação em massa de documentos XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Manter valores de identidade ao importar dados em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Manter valores nulos ou use os valores padrão durante a importação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Usar um arquivo de formato para importação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Importação e exportação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENQUERY &#40;Transact-SQL&#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [Funções de conjunto de linhas &#40;Transact-SQL&#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
