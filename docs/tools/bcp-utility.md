---
title: Utilitário bcp | Microsoft Docs
ms.custom: ''
ms.date: 02/12/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.component: bcp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server]
- exporting data
- row exporting [SQL Server]
- copying data [SQL Server], bcp utility
- command prompt utilities [SQL Server], bcp
- tables [SQL Server], importing data
- column importing [SQL Server]
- bcp utility [SQL Server], command options
- file exporting [SQL Server]
- bulk copy [SQL Server]
- bcp utility [SQL Server], about bcp utility
- tables [SQL Server], exporting data
- row importing [SQL Server]
- importing data, bcp utility
- file importing [SQL Server]
- column exporting [SQL Server]
ms.assetid: c0af54f5-ca4a-4995-a3a4-0ce39c30ec38
caps.latest.revision: 222
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: e0bf785a4e7738b569a72cc4e30c7e94cbe233ac
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39456050"
---
# <a name="bcp-utility"></a>Utilitário bcp
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

 > Para obter o conteúdo relacionado a versões anteriores do SQL Server, confira [Utilitário bcp](https://msdn.microsoft.com/en-US/library/ms162802(SQL.120).aspx).

 > Para obter a versão mais recente do utilitário bcp, consulte [14.0 de utilitários de linha de comando do Microsoft para SQL Server ](http://go.microsoft.com/fwlink/?LinkID=825643)

 > Para usar o bcp no Linux, confira [instalar o sqlcmd e bcp no Linux](../linux/sql-server-linux-setup-tools.md).

 > Para obter informações detalhadas sobre como usar o bcp com o Azure SQL Data Warehouse, consulte [carregar dados com o bcp](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp).

  O utilitário **bcp** (**b**ulk **c**opy **p**rogram) copia dados em massa entre uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e um arquivo de dados em um formato especificado pelo usuário. O utilitário **bcp** pode ser usado para importar grande número de novas linhas para tabelas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou para exportar dados de tabelas para arquivos de dados. Exceto quando usado com a opção **queryout** , o utilitário não requer conhecimento de [!INCLUDE[tsql](../includes/tsql-md.md)]. Para importar dados para uma tabela, você deve usar um arquivo de formato criado para aquela tabela ou entender a estrutura da tabela e os tipos de dados válidos para suas colunas.  
  
 ![Ícone de link do tópico](../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") Para obter as convenções de sintaxe usadas para a sintaxe de **bcp**, confira [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
> [!NOTE]
> Se você usar **bcp** para fazer backup de seus dados, crie um arquivo de formato para registrar o formato dos dados. Os arquivos de dados**bcp**  **não incluem** quaisquer informações de esquema ou de formato. Portanto, se uma tabela ou exibição for descartada e você não tiver um arquivo de formato, não será possível importar os dados.  
  
<table><th>Sintaxe</th><tr><td><pre>
bcp [<a href="#db_name">database_name.</a>] <a href="#schema">schema</a>.{<a href="#tbl_name">table_name</a> | <a href="#vw_name">view_name</a> | <a href="#query">"query"</a>
    {<a href="#in">in</a> <a href="#data_file">data_file</a> | <a href="#out">out</a> <a href="#data_file">data_file</a> | <a href="#qry_out">queryout</a> <a href="#data_file">data_file</a> | <a href="#format">format</a> <a href="#format">nul</a>}
<a>                                                                                                         </a>
    [<a href="#a">-a packet_size</a>]
    [<a href="#b">-b batch_size</a>]
    [<a href="#c">-c</a>]
    [<a href="#C">-C { ACP | OEM | RAW | code_page } </a>]
    [<a href="#d">-d database_name</a>]
    [<a href="#e">-e err_file</a>]
    [<a href="#E">-E</a>]
    [<a href="#f">-f format_file</a>]
    [<a href="#F">-F first_row</a>]
    [<a href="#G">-G Azure Active Directory Authentication</a>]
    [<a href="#h">-h"hint [,...n]"</a>]
    [<a href="#i">-i input_file</a>]
    [<a href="#k">-k</a>]
    [<a href="#K">-K application_intent</a>]
    [<a href="#L">-L last_row</a>]
    [<a href="#m">-m max_errors</a>]
    [<a href="#n">-n</a>]
    [<a href="#N">-N</a>]
    [<a href="#o">-o output_file</a>]
    [<a href="#P">-P password</a>]
    [<a href="#q">-q</a>]
    [<a href="#r">-r row_term</a>]
    [<a href="#R">-R</a>]
    [<a href="#S">-S [server_name[\instance_name]</a>]
    [<a href="#t">-t field_term</a>]
    [<a href="#T">-T</a>]
    [<a href="#U">-U login_id</a>]
    [<a href="#v">-v</a>]
    [<a href="#V">-V (80 | 90 | 100 | 110 | 120 | 130 ) </a>]
    [<a href="#w">-w</a>]
    [<a href="#x">-x</a>]
</pre></td></tr></table>  
  
## <a name="arguments"></a>Argumentos  
 ***data_file***<a name="data_file"></a>  
 É o caminho completo do arquivo de dados. Quando dados são importados em massa para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o arquivo de dados contém os dados a serem copiados na tabela ou exibição especificada. Quando dados são exportados em massa do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o arquivo de dados contém os dados copiados da tabela ou exibição. O caminho pode ter de 1 a 255 caracteres. O arquivo de dados pode conter no máximo 2^63 - 1 linhas.  
  
 ***database_name***<a name="db_name"></a>  
 É o nome do banco de dados no qual a tabela ou exibição especificada reside. Se não estiver especificado, esse será o banco de dados padrão do usuário.  
  
 Você também pode especificar explicitamente o nome de banco de dados com **d-**.  
  
 **in** *data_file* | **out** *data_file* | **queryout** *data_file* | **format nul**  
 Especifica a direção da cópia em massa, do seguinte modo:  
  
-   **in**<a name="in"></a> copia de um arquivo em uma tabela ou exibição de banco de dados.  
  
-   **out**<a name="out"></a> copia da tabela ou exibição de banco de dados para um arquivo. Se você especificar um arquivo existente, o arquivo será substituído. Ao extrair dados, observe que o utilitário **bcp** representa uma cadeia de caracteres vazia como nula e uma cadeia de caracteres nula como uma cadeia de caracteres vazia.  
  
-   **queryout**<a name="qry_out"></a> copia de uma consulta e deve ser especificado somente quando você copiar dados em massa de uma consulta.  
  
-   **format**<a name="format"></a> cria um arquivo de formato com base na opção especificada (**-n**, **-c**, **-w**, ou **-N**) e nos delimitadores da tabela ou da exibição. Quando você copia dados em massa, o comando **bcp** pode recorrer a um arquivo de formato, o que libera você da necessidade de inserir novamente as informações de formato de forma interativa. A opção **format** exige a opção **-f**; a criação de um arquivo de formato XML também exige a opção **-x**. Para obter mais informações, consulte [Criar um arquivo de formato &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md). É necessário especificar **nul** como o valor (**format nul**).  
  
 ***owner***<a name="schema"></a>  
 Corresponde ao nome do proprietário da tabela ou exibição. O*owner* será opcional se o usuário que estiver executando a operação for o proprietário da tabela ou exibição especificada. Se *owner* não estiver especificado e o usuário que está executando a operação não for proprietário da tabela ou exibição especificada, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] retornará uma mensagem de erro e a operação será cancelada.  
  
**"** ***query*** **"** <a name="query"> </a> é uma consulta do [!INCLUDE[tsql](../includes/tsql-md.md)] que retorna um conjunto de resultados. Se a consulta retornar vários conjuntos de resultados, somente o primeiro conjunto de resultados será copiado no arquivo de dados; os conjuntos de resultados subsequentes serão ignorados. Coloque a consulta entre aspas duplas e qualquer coisa incorporada na consulta entre aspas simples. **queryout** também deve ser especificado quando você copiar dados em massa de uma consulta.  
  
 A consulta pode fazer referência a um procedimento armazenado desde que todas as tabelas referenciadas no procedimento armazenado existam antes da execução da instrução bcp. Por exemplo, se o procedimento armazenado gerar uma tabela temporária, ocorrerá uma falha com a instrução **bcp** , pois a tabela temporária ficará disponível somente durante o tempo de execução e não durante o tempo de execução da instrução. Nesse caso, considere a inserção do resultado do procedimento armazenado em uma tabela e, em seguida, use **bcp** para copiar os dados da tabela em um arquivo de dados.  
  
 ***table_name***<a name="tbl_name"></a>  
 Nome da tabela de destino ao importar dados para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**in**) e da tabela de origem ao exportar dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**out**).  
  
 ***view_name***<a name="vw_name"></a>   
 Nome da exibição de destino ao copiar dados no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**in**) e da exibição de origem ao copiar dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**out**). Somente as exibições nas quais todas as colunas fazem referência à mesma tabela podem ser usadas como exibições de destino. Para obter mais informações sobre as restrições para copiar dados em exibições, veja [INSERT &#40;Transact-SQL&#41;](../t-sql/statements/insert-transact-sql.md).  
  
 **-a** ***packet_size***<a name="a"></a>  
 Especifica o número de bytes por pacote de rede enviado de e para o servidor. Uma opção de configuração do servidor pode ser definida usando [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (ou o procedimento armazenado do sistema **sp_configure** ). Contudo, a opção de configuração do servidor pode ser substituída individualmente usando-se esta opção. *packet_size* pode estar entre 4096 a 65535 bytes, sendo 4096 o padrão.  
  
 Um tamanho de pacote maior pode aumentar o desempenho de operações de cópia em massa. Se um pacote maior for pedido mas não puder ser concedido, o padrão será usado. As estatísticas de desempenho geradas pelo utilitário **bcp** mostram o tamanho de pacote usado.  
  
 **-b** ***batch_size***<a name="b"></a>  
 Especifica o número de linhas por lote de dados importados. Cada lote é importado e registrado como uma transação separada que importa o lote inteiro antes de ser confirmado. Por padrão, todas as linhas no arquivo de dados são importadas como um lote. Para distribuir as linhas entre vários lotes, especifique um *batch_size* que seja menor do que o número de linhas no arquivo de dados. Se a transação apresentar falha para qualquer lote, só serão revertidas as inserções do lote atual. Lotes já importados por transações confirmadas não serão afetados por uma falha posterior.  
  
 Não use essa opção em conjunto com a opção **-h "** ROWS_PER_BATCH **=***bb***"**.  
 
 **-c**<a name="c"></a>  
 Executa a operação usando um tipo de dados de caractere. Essa opção não solicita informações para cada campo; ela usa **char** como o tipo de armazenamento, sem prefixos e com **\t** (caractere de tabulação) como separador de campos e **\r\n** (caractere de nova linha) como terminador de linha. **-c** não é compatível com **-w**.  
  
 Para obter mais informações, veja [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md).  
  
 **-C** { **ACP** | **OEM** | **RAW** | *code_page* }<a name="C"></a>   
 Especifica a página de código dos dados no arquivo de dados. *code_page* só será relevante se os dados contiverem colunas **char**, **varchar**ou **text** com valores de caractere maiores que 127 ou menores que 32.  
  
> [!NOTE]
> Recomendamos a especificação de um nome de agrupamento para cada coluna em um arquivo de formato, exceto quando você quiser que a opção 65001 tenha prioridade sobre a especificação de agrupamento/página de código.
  
|Valor da página de código|Descrição|  
|---------------------|-----------------|  
|ACP|[!INCLUDE[vcpransi](../includes/vcpransi-md.md)]/Microsoft Windows (ISO 1252).|  
|OEM|Página de código padrão usada pelo cliente. Essa é a página de código padrão usada se **-C** não for especificado.|  
|RAW|Não ocorre nenhuma conversão de uma página de código para outra. Essa é a opção mais rápida porque não acontece nenhuma conversão.|  
|*code_page*|Um número de página de código específico, por exemplo, 850.<br /><br /> As versões anteriores à versão 13 ([!INCLUDE[ssSQL15](../includes/sssql15-md.md)]) não dão suporte à página de código 65001 (codificação UTF-8). As versões a partir da 13 podem importar a codificação UTF-8 para versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
 **-d** ***database_name***<a name="d"></a>   
 Especifica o banco de dados que deve ser conectado. Por padrão, bcp.exe se conecta ao banco de dados padrão do usuário. Se **-d** *database_name* e um nome de três partes (*database_name.schema.table*, passed as the first parameter to bcp.exe) is specified, an error will occur because you cannot specify the database name twice.Se *database_name* começar com um hífen (-) ou uma barra (/), não adicione um espaço entre **-d** e o nome do banco de dados.  
  
 **-e** ***err_file***<a name="e"></a>  
 Especifica o caminho completo de um arquivo de erro usado para armazenar as linhas que o utilitário **bcp** não pode transferir do arquivo para o banco de dados. As mensagens de erro do comando **bcp** vão para a estação de trabalho do usuário. Se essa opção não for usada, o arquivo de erros não será criado.  
  
 Se *err_file* começar com um hífen (-) ou uma barra (/), não inclua um espaço entre **-e** e o valor *err_file* .  
  
 **-E**<a name="E"></a>   
 Especifica que o valor, ou valores, de identidade no arquivo de dados importado deve ser usado para a coluna de identidade. Se **-E** não for fornecido, os valores de identidade para essa coluna no arquivo de dados que está sendo importado serão ignorados e o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] atribuirá automaticamente valores exclusivos com base nos valores semente e de incremento especificados durante a criação da tabela.  
  
 Se o arquivo de dados não contiver valores para a coluna de identidade na tabela ou exibição, use um arquivo de formato para especificar que a coluna de identidade na tabela ou exibição deve ser ignorada ao importar dados. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] atribui valores exclusivos para a coluna automaticamente. Para obter mais informações, veja [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkident-transact-sql.md).  
  
 A opção **-E** tem um requisito de permissões especial. Para obter mais informações, consulte "[Comentários](#remarks)", mais adiante neste tópico.  
   
 **-f** ***format_file***<a name="f"></a>  
 Especifica o caminho completo de um arquivo de formato. O significado dessa opção depende do ambiente no qual é usada, do seguinte modo:  
  
-   Se **-f** for usado com a opção **format** , o *format_file* especificado será criado para a tabela ou exibição especificada. Para criar um arquivo de formato XML, especifique também a opção **-x**. Para obter mais informações, consulte [Criar um arquivo de formato &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md).  
  
-   Se for usado com a opção **in** ou **out**, **-f** exigirá um arquivo de formato existente.  
  
    > [!NOTE]
    > O uso de um arquivo de formato com a opção **in** ou **out** é opcional. Na ausência da opção **-f** , se **-n**, **-c**, **-w**ou **-N** não for especificado, o comando solicitará informações de formato e permitirá que você salve suas respostas em um arquivo de formato (cujo nome de arquivo padrão é Bcp.fmt).
  
 Se *format_file* começar com um hífen (-) ou uma barra (/), não inclua um espaço entre **-f** e o valor *format_file* .  
  
**-F** ***first_row***<a name="F"></a>  
 Especifica o número da primeira linha que deve ser exportada de uma tabela ou importada de um arquivo de dados. Esse parâmetro requer um valor maior do que (>) 0, mas menor do que (<) ou igual ao (=) número total de linhas. Na ausência desse parâmetro, o padrão é a primeira linha do arquivo.  
  
 *first_row* pode ser um inteiro positivo com um valor de até 2^63-1. **-F** *first_row* is 1-based.  

**-G**<a name="G"></a>  
 Essa opção é usada pelo cliente para conectar-se com o Banco de Dados SQL do Azure ou com o SQL Data Warehouse do Azure para especificar que o usuário seja autenticado usando a autenticação do Azure Active Directory. A opção -G exige [versão 14.0.3008.27 ou posterior](http://go.microsoft.com/fwlink/?LinkID=825643). Para determinar a versão, execute bcp -v. Para obter mais informações, consulte [Use autenticação do Azure Active Directory para autenticação com o banco de dados SQL ou SQL Data Warehouse](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication). 

> [!TIP]
>  Para verificar se sua versão do bcp inclui suporte para o tipo de autenticação de diretório Active Directory do Azure (AAD) **bcp--** (bcp\<espaço >\<dash >\<dash >) e verifique se que você vê - G na lista de argumentos disponíveis.

- **Nome de usuário do Azure Active Directory e senha:** 

    Quando desejar usar um nome de usuário do Azure Active Directory e uma senha, você poderá fornecer a opção **- G** e também usar o nome de usuário e a senha fornecendo as opções **-U** e **-P** . 

    O exemplo a seguir exporta dados usando o nome de usuário do Azure AD e a senha em que o usuário e a senha é uma credencial do AAD. O exemplo exporta a tabela `bcptest` do banco de dados `testdb` do servidor do Azure `aadserver.database.windows.net` e armazena os dados no arquivo `c:\last\data1.dat`:
    ``` 
    bcp bcptest out "c:\last\data1.dat" -c -t -S aadserver.database.windows.net -d testdb -G -U alice@aadtest.onmicrosoft.com -P xxxxx
    ``` 

    O exemplo a seguir importa dados usando o nome de usuário do Azure AD e a senha em que o usuário e a senha é uma credencial do AAD. O exemplo importa os dados de arquivo `c:\last\data1.dat` na tabela `bcptest` para o banco de dados `testdb` no servidor do Azure `aadserver.database.windows.net` usando usuário/senha do Azure AD:
    ```
    bcp bcptest in "c:\last\data1.dat" -c -t -S aadserver.database.windows.net -d testdb -G -U alice@aadtest.onmicrosoft.com -P xxxxx
    ```



- **Integração ao Azure Active Directory** 
 
    Para a autenticação integrada do Azure Active Directory, forneça a opção **-G** sem um nome de usuário e uma senha. Essa configuração pressupõe que a conta de usuário atual do Windows (a conta que está executando o comando bcp) é federada com o Azure AD: 

    O exemplo a seguir exporta dados usando a conta integrado do Azure AD. O exemplo exporta a tabela `bcptest` do banco de dados `testdb` usando o Azure AD integrado do servidor do Azure `aadserver.database.windows.net` e armazena os dados no arquivo `c:\last\data2.dat`:

    ```
    bcp bcptest out "c:\last\data2.dat" -S aadserver.database.windows.net -d testdb -G -c -t
    ```

    O exemplo a seguir importa dados usando a autenticação integrada do AD do Azure O exemplo importa os dados de arquivo `c:\last\data2.txt` na tabela `bcptest` para o banco de dados `testdb` no servidor do Azure `aadserver.database.windows.net` usando a autenticação integrada do Azure AD:

    ```
    bcp bcptest in "c:\last\data2.dat" -S aadserver.database.windows.net -d testdb -G -c -t
    ```

  
**-h** ***"load hints***[ ,... *n*]**"**<a name="h"></a> Specifies the hint or hints to be used during a bulk import of data into a table or view.  
  
* **ORDER**(***column*[ASC | DESC] [**,**...*n*]**)**  
A ordem de classificação dos dados no arquivo de dados. O desempenho da importação em massa será melhorado se os dados importados forem armazenados de acordo com o índice clusterizado na tabela, se houver. Se o arquivo de dados for armazenado em uma ordem diferente, ou seja, distinta da ordem de uma chave de índice clusterizado, ou se não houver nenhum índice clusterizado na tabela, a cláusula ORDER será ignorada. Os nomes das colunas fornecidos devem ser nomes de colunas válidas na tabela de destino. Por padrão, o **bcp** supõe que o arquivo de dados não está classificado. Para obter uma importação em massa otimizada, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] também valida que os dados importados sejam classificados.  
  
* **ROWS_PER_BATCH** **=** ***bb***  
Número de linhas de dados por lote (como *bb*). É usado quando **-b** não é especificado, resultando no envio de todo o arquivo de dados ao servidor como uma transação única. O servidor otimiza o carregamento em massa de acordo com o valor *bb*. Por padrão, ROWS_PER_BATCH é desconhecido.  
  
* **KILOBYTES_PER_BATCH** **=** ***cc***  
Número aproximado de kilobytes de dados por lote (como *cc*). Por padrão, KILOBYTES_PER_BATCH é desconhecido.  
  
* **TABLOCK**  
Especifica que um bloqueio no nível de tabela de atualização em massa é adquirido durante a operação de carregamento em massa, caso contrário, um bloqueio no nível de linha é adquirido. Essa dica melhora significativamente o desempenho porque manter um bloqueio durante a operação de cópia em massa reduz a contenção de bloqueios na tabela. Uma tabela pode ser carregada simultaneamente através de vários clientes se não tiver nenhum índice e **TABLOCK** for especificado. Por padrão, o comportamento de bloqueio é determinado pela opção de tabela **bloqueio de tabela em carregamento em massa**.  
  
  > [!NOTE]
  > Se a tabela de destino for um índice columnstore clusterizado, a dica TABLOCK não será necessária para carregar por vários clientes simultâneos, pois cada thread simultâneo recebe um rowgroup separado dentro do índice e carrega dados nele. Veja os tópicos conceituais sobre o índice columnstore para obter detalhes,
  
  **CHECK_CONSTRAINTS**  
  Especifica que todas as restrições na tabela ou exibição de destino devem ser verificadas durante a operação de importação em massa. Sem a dica CHECK_CONSTRAINTS, todas as restrições CHECK e FOREIGN KEY são ignoradas e, depois da operação, a restrição na tabela é marcada como não confiável.  
  
  > [!NOTE]
  > As restrições UNIQUE, PRIMARY KEY e NOT NULL são sempre impostas.
  
  Em algum momento, você precisará verificar as restrições em toda a tabela. Se a tabela não estava vazia antes da operação de importação em massa, o custo de revalidação da restrição poderá exceder o custo da aplicação de restrições CHECK aos dados incrementais. Portanto, recomendamos que normalmente você habilite a verificação de restrições durante uma importação incremental em massa.  
  
  Uma situação na qual talvez você queira desabilitar as restrições (o comportamento padrão) é quando os dados de entrada contiverem linhas que violam as restrições. Com as restrições CHECK desabilitadas, é possível importar os dados e usar instruções [!INCLUDE[tsql](../includes/tsql-md.md)] para remover os dados inválidos.  
  
  > [!NOTE]
  > Agora, o**bcp** impõe validação de dados e verificações de dados que podem provocar falhas em scripts se forem executados em dados inválidos em um arquivo de dados.
  
  > [!NOTE]
  > A opção **-m** *max_errors* não se aplica à verificação de restrição.
  
* **FIRE_TRIGGERS**  
Especificado com o argumento **in** , todos os gatilhos de inserção definidos na tabela de destino serão executados durante a operação de cópia em massa. Se FIRE_TRIGGERS não for especificado, nenhum gatilho de inserção será executado. FIRE_TRIGGERS é ignorado para os argumentos **out**, **queryout**e **format** .  
  
 **-i** ***input_file***<a name="i"></a>  
 Especifica o nome de um arquivo de resposta que contém as respostas às perguntas do prompt de comando para cada campo de dados, quando uma cópia em massa está sendo executada com o uso do modo interativo (**-n**, **-c**, **-w**ou **-N** não especificado).  
  
 Se *input_file* começar com um hífen (-) ou uma barra (/), não inclua um espaço entre **-i** e o valor *input_file* .  
  
 **-k**<a name="k"></a>  
 Especifica que colunas vazias devem reter um valor nulo durante a operação, em vez de qualquer valor padrão nas colunas inseridas. Para obter mais informações, veja [Manter valores nulos ou usar os valores padrão durante a importação em massa &#40;SQL Server&#41;](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
 **-K** ***application_intent***<a name="K"></a>   
 Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. O único valor possível é **ReadOnly**. Se **-K** não for especificado, o utilitário bcp não dará suporte à conectividade a uma réplica secundária em um grupo de disponibilidade AlwaysOn. Para obter mais informações, consulte [Secundárias ativas: réplicas secundárias legíveis &#40;Grupos de Disponibilidade AlwaysOn&#41;](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 **-L** ***last_row***<a name="L"></a>  
 Especifica o número da última linha a ser exportada de uma tabela ou importada de um arquivo de dados. Esse parâmetro exige um valor maior do que (>) 0, mas menor do que (<) ou igual ao (=) número da última linha. Na ausência desse parâmetro, o padrão é a última linha do arquivo.  
  
 *last_row* pode ser um inteiro positivo com um valor de até 2^63-1.  
  
**-m** ***max_errors***<a name="m"></a>  
Especifica o número máximo de erros de sintaxe que podem ocorrer antes que a operação **bcp** seja cancelada. Um erro de sintaxe implica em um erro de conversão de dados para o tipo de dados de destino. O total de *max_errors* exclui todos os erros que podem ser detectados apenas no servidor, como violações de restrição.  
  
 Uma linha que não possa ser copiada pelo utilitário **bcp** é ignorada e contada como um erro. Se essa opção não estiver incluída, o padrão será 10.  
  
> [!NOTE]
> A opção **-m** também não se aplica à conversão de tipos de dados **money** nem **bigint** .
  
**-n**<a name="n"></a>  
Executa a operação de cópia em massa usando os tipos de dados nativos (banco de dados) dos dados. Essa opção não solicita informações para cada campo; ela usa os valores nativos.  
  
Para obter mais informações, veja [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md).  
  
**-N**<a name="N"></a>  
Executa a operação de cópia em massa usando os tipos de dados nativos (banco de dados) dos dados para dados de não caractere e caracteres Unicode para dados de caractere. Essa opção oferece um desempenho mais elevado como alternativa à opção **-w** e destina-se a ser usada para transferir dados de uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para outra usando um arquivo de dados. Ela não solicita informações para cada campo. Use essa opção quando estiver transferindo dados que contenham caracteres ANSI estendidos e quiser aproveitar o desempenho do modo nativo.  
  
 Para obter mais informações, veja [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md).  
  
 Se você exportar e depois importar dados no mesmo esquema de tabela usando bcp.exe com **-N**, talvez seja exibido um aviso de truncamento, se houver uma coluna de caracteres não Unicode de tamanho fixo (por exemplo, **char(10)**).  
  
 O aviso pode ser ignorado. Uma maneira de resolver este aviso é usar **-n** em vez de **-N**.  
  
 **-o** ***output_file***<a name="o"></a>  
 Especifica o nome de um arquivo que recebe a saída redirecionada do prompt de comando.  
  
 Se *output_file* começar com um hífen (-) ou uma barra (/), não inclua um espaço entre **-o** e o valor *output_file* .  
  
 **-P** ***password***<a name="P"></a>  
 Especifica a senha para a ID de logon. Se essa opção não for usada, o comando **bcp** solicitará uma senha. Se essa opção for usada ao término do prompt de comando sem uma senha, o **bcp** usará a senha padrão (NULL).  
  
> [!IMPORTANT]
> [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]
  
 Para mascarar a senha, não especifique a opção **-P** juntamente com a opção **-U** . Em vez disso, depois de especificar o **bcp** junto com a opção **-U** e outras opções (não especificar **-P**), pressione ENTER e o comando solicitará uma senha. Esse método garante que sua senha será mascarada quando for inserida.  
  
 Se *password* começar com um hífen (-) ou uma barra (/), não adicione um espaço entre **-P** e o valor *password* .  
  
 **-q**<a name="q"></a>  
 Executa a instrução SET QUOTED_IDENTIFIERS ON na conexão entre o utilitário **bcp** e uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Use essa opção para especificar um nome de banco de dados, proprietário, tabela ou exibição que contenha um espaço ou aspas simples. Inclua todo o nome da tabela de três partes ou da exibição entre aspas duplas ("").  
  
 Para especificar um nome de banco de dados que contenha um espaço ou aspas simples, você deve usar a opção **-q** .  
  
 **-q** não se aplica a valores passados para **-d**.  
  
 Para obter mais informações, consulte [Comentários](#remarks), mais adiante neste tópico.  
  
 **-r** ***row_term***<a name="r"></a>  
 Especifica o terminador de linha. O padrão é **\n** (caractere de nova linha). Use esse parâmetro para substituir o terminador de linha padrão. Para obter mais informações, veja [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  
  
 Se você especificar o terminador de linha em notação hexadecimal em um comando bcp.exe, o valor será truncado em 0x00. Por exemplo, se você especificar 0x410041, 0x41 será usado.  
  
 Se *row_term* começar com um hífen (-) ou uma barra (/), não inclua um espaço entre **-r** e o valor *row_term* .  
  
 **-R**<a name="R"></a>  
 Especifica que dados de moeda, data e horário são copiados em massa no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando o formato regional definido para as configurações de localidade do computador cliente. Por padrão, as configurações regionais são ignoradas.  
  
 **-S** ***server_name*** [\\***instance_name***]<a name="S"></a> Especifica uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] à qual você deseja se conectar. Se nenhum servidor for especificado, o utilitário **bcp** se conectará à instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no computador local. Essa opção é requerida quando um comando **bcp** é executado de um computador remoto na rede ou de uma instância local nomeada. Para se conectar à instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um servidor, especifique apenas *server_name*. Para se conectar a uma instância nomeada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], especifique *server_name***\\***instance_name*.  
  
 **-t** ***field_term***<a name="t"></a>  
 Especifica o terminador de campo. O padrão é **\t** (caractere de tabulação). Use esse parâmetro para substituir o terminador de campo padrão. Para obter mais informações, consulte [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  
  
 Se você especificar o terminador de campo em notação hexadecimal em um comando bcp.exe, o valor será truncado em 0x00. Por exemplo, se você especificar 0x410041, 0x41 será usado.  
  
 Se *field_term* começar com um hífen (-) ou uma barra (/), não inclua um espaço entre **-t** e o valor *field_term* .  
  
 **-T**<a name="T"></a>  
 Especifica que o utilitário **bcp** se conecta ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com uma conexão confiável usando segurança integrada. As credenciais de segurança do usuário de rede, *login_id*e *password* não são necessárias. Se **-T** não for especificado, será necessário especificar **-U** e **-P** para o logon ser efetuado com êxito.
 
> [!IMPORTANT]
> Quando o utilitário **bcp** estiver se conectando ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com uma conexão confiável usando segurança integrada, use a opção **-T** (conexão confiável) em vez da combinação *user name* e *password* . Quando o utilitário **bcp** está se conectando ao Banco de Dados SQL ou ao SQL Data Warehouse, não há suporte para o uso da autenticação do Windows ou do Azure Active Directory. Use as opções **- U** e **-P** . 
  
 **-U** ***login_id***<a name="U"></a>  
 Especifica a ID de logon usada para conectar-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]
> Quando o utilitário **bcp** estiver se conectando ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com uma conexão confiável usando segurança integrada, use a opção **-T** (conexão confiável) em vez da combinação *user name* e *password* . Quando o utilitário **bcp** está se conectando ao Banco de Dados SQL ou ao SQL Data Warehouse, não há suporte para o uso da autenticação do Windows ou do Azure Active Directory. Use as opções **- U** e **-P** .
  
 **-v**<a name="v"></a>  
 Relata o número de versão e os direitos autorais do utilitário **bcp** .  
  
 **-V** (**80** | **90** | **100** | **110** | **120** | **130** )<a name="V"></a>  
 Executa a operação de cópia em massa usando tipos de dados de uma versão anterior do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Essa opção não solicita informações para cada campo; ela usa os valores padrão.  
  
 **80** = [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]  
  
 **90** = [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] and [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
 Por exemplo, para gerar dados para tipos sem suporte no [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)], mas que foram incorporados nas versões posteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], use a opção -V80.  
  
 Para obter mais informações, consulte [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md).  
  
 **-w**<a name="w"></a>  
 Executa a operação de cópia em massa usando caracteres Unicode. Essa opção não solicita o preenchimento de cada campo; ela usa **nchar** como tipo de armazenamento, sem prefixos, **\t** (caractere de tabulação) como separador de campos e **\n** (caractere de nova linha) como terminador de linha. **-w** não é compatível com **-c**.  
  
 Para obter mais informações, consulte [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md).  
  
 **-x**<a name="x"></a>  
 Usado com as opções **format** e **-f** *format_file* , gera um arquivo de formato baseado em XML em vez do arquivo de formato não XML padrão. O **-x** não funciona ao importar ou exportar dados. Ele gera um erro se for usado sem **format** nem **-f** *format_file*.  
  
## Comentários<a name="remarks"></a>
 O utilitário **bcp** 13.0 é instalado quando você instala as ferramentas do [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] . Se as ferramentas forem instaladas para o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e para uma versão anterior do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], dependendo do valor na variável de ambiente PATH, talvez você esteja usando o cliente **bcp** anterior em vez do cliente **bcp** 13.0. Essa variável de ambiente define o conjunto de diretórios usado pelo Windows para pesquisar por arquivos executáveis. Para descobrir qual versão você está usando, execute o comando **bcp /v** no Prompt de Comando do Windows. Para obter mais informações sobre como definir o caminho de comando na variável de ambiente PATH, consulte a Ajuda do Windows.  
 
O utilitário bcp também pode ser baixado separadamente do [Feature Pack do Microsoft SQL Server 2016](https://www.microsoft.com/en-us/download/details.aspx?id=52676).  Selecione `ENU\x64\MsSqlCmdLnUtils.msi` ou `ENU\x86\MsSqlCmdLnUtils.msi`.

  
 Os arquivos de formato XML só têm suporte quando as ferramentas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] são instaladas junto com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client.  
  
 Para obter mais informações sobre onde encontrar ou como executar o utilitário **bcp** e sobre as convenções de sintaxe dos utilitários de prompt de comando, confira [Referência de utilitário de linha de comando &#40;Mecanismo de Banco de Dados&#41;](../tools/command-prompt-utility-reference-database-engine.md).  
  
 Para obter informações sobre como preparar dados para importar ou exportar operações em massa, veja [Preparar dados para exportação ou importação em massa &#40;SQL Server&#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 Para obter informações sobre quando as operações de inserção de linhas executadas por importações em massa são registradas no log de transações, veja [Pré-requisitos para log mínimo em importação em massa](../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
## <a name="native-data-file-support"></a>Suporte de arquivos de dados nativos  
 No [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], o utilitário **bcp** oferece suporte somente a arquivos de dados nativos compatíveis com [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]e [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
## <a name="computed-columns-and-timestamp-columns"></a>Colunas computadas e colunas de carimbo de data/hora  
 Os valores no arquivo de dados sendo para colunas computadas ou **timestamp** são ignorados, e o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] atribui valores automaticamente. Se o arquivo de dados não contiver valores para as colunas computadas ou **timestamp** na tabela, use um arquivo de formato para especificar que as colunas computadas ou **timestamp** na tabela devem ser ignoradas ao importar dados; o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] automaticamente atribuirá valores para a coluna.  
  
 Colunas computadas e **timestamp** são copiadas em massa do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um arquivo de dados, como sempre.  
  
## <a name="specifying-identifiers-that-contain-spaces-or-quotation-marks"></a>Especificando identificadores que contêm espaços ou aspas  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podem incluir caracteres como espaços inseridos e aspas. Tais identificadores devem ser tratados do seguinte modo:  
  
-   Quando você especificar um identificador ou nome de arquivo que inclua um espaço ou aspas no prompt de comando, coloque o identificador entre aspas ("").  
  
     Por exemplo, o comando `bcp out` a seguir cria um arquivo de dados nomeado `Currency Types.dat`:  
  
    ```  
    bcp AdventureWorks2012.Sales.Currency out "Currency Types.dat" -T -c  
    ```  
  
-   Para especificar um nome de banco de dados que contém um espaço ou aspas, é necessário usar a opção **-q** .  
  
-   Para nomes de proprietário, tabela ou exibição que contenham espaços inseridos ou aspas, você também pode:  
  
    -   Especificar a opção **-q** ou  
  
    -   Inserir o nome de proprietário, tabela ou exibição entre colchetes ([]) dentro das aspas.  
  
## <a name="data-validation"></a>Validação de dados  
 Agora, o**bcp** impõe validação de dados e verificações de dados que podem provocar falhas em scripts se forem executados em dados inválidos em um arquivo de dados. Por exemplo, o **bcp** agora verifica se:  
  
-   A representação nativa de tipos de dados **float** ou **real** é válida.  
  
-   Dados Unicode têm um comprimento regular de byte.  
  
 Formas de dados inválidos que podiam ser importadas em massa em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podem falhar ao serem carregadas agora; enquanto em versões anteriores a falha só ocorria quando um cliente tentava acessar os dados inválidos. A validação adicional minimiza as surpresas ao consultar os dados depois do carregamento em massa.  
  
## <a name="bulk-exporting-or-importing-sqlxml-documents"></a>Exportando ou importando documentos SQLXML em massa  
 Para exportar ou importar dados SQLXML em massa, use um dos tipos de dados a seguir em seu arquivo de formato.  
  
|Tipo de dados|Efeito|  
|---------------|------------|  
|SQLCHAR ou SQLVARYCHAR|Os dados são enviados na página de código do cliente ou na página de código implicada pelo agrupamento. O efeito é o mesmo que especificar a opção **-c** sem especificar um arquivo de formato.|  
|SQLNCHAR ou SQLNVARCHAR|Os dados são enviados como Unicode. O efeito é o mesmo que especificar a opção **-w** sem especificar um arquivo de formato.|  
|SQLBINARY ou SQLVARYBIN|Os dados são enviados sem qualquer conversão.|  
  
## <a name="permissions"></a>Permissões  
 Uma operação **bcp out** exige a permissão SELECT na tabela de origem.  
  
 Uma operação **bcp in** exige no mínimo as permissões SELECT/INSERT na tabela de destino. Além disso, a permissão ALTER TABLE será necessária se qualquer das seguintes afirmações for verdadeira:  
  
-   Existem restrições e a dica CHECK_CONSTRAINTS não foi especificada.  
  
    > [!NOTE]
    > Desabilitar restrições é o comportamento padrão. Para habilitar restrições explicitamente, use a opção **-h** com a dica CHECK_CONSTRAINTS.
  
-   Existem gatilhos e a dica FIRE_TRIGGER não foi especificada.  
  
    > [!NOTE]
    > Por padrão, os gatilhos não são disparados. Para disparar gatilhos explicitamente, use a opção **-h** com a dica FIRE_TRIGGERS.
  
-   Use a opção **-E** para importar valores de identidade de um arquivo de dados.  
  
> [!NOTE]
> A exigência da permissão ALTER TABLE na tabela de destino era nova no [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]. Essa nova exigência pode provocar falha em scripts **bcp** que não impõem verificações de gatilhos e de restrições se a conta do usuário não tiver permissões ALTER TABLE para a tabela de destino.
  
## <a name="character-mode--c-and-native-mode--n-best-practices"></a>Práticas recomendadas de modo de caractere (-c) e modo nativo (-n)  
 Esta seção apresenta recomendações para modo de caractere (-c) e modo nativo (-n).  
  
-   (Administrador/Usuário) Quando possível, use o formato nativo (-n) para evitar o problema de separador. Use o formato nativo para exportar e importar com o uso do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Exporte dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com o uso da opção -c ou -w se os dados serão importados para um banco de dados do[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   (Administrador) Verifique dados ao usar BCP OUT. Por exemplo, quando você usa BCP OUT, BCP IN e, em seguida, BCP OUT, verifique se os dados são exportados corretamente e se os valores de terminador não são usados como parte de algum valor de dados. Considere substituir os terminadores padrão (com as opções -t e -r) com valores hexadecimais aleatórios para evitar conflitos entre valores de terminadores e os valores de dados.  
  
-   (Usuário) Use um terminador longo e exclusivo (qualquer sequência de bytes ou de caracteres) para minimizar a possibilidade de um conflito com o valor da cadeia de caracteres real. Isso pode ser feito com as opções -t e -r.  
  
## <a name="examples"></a>Exemplos  
 Esta seção contém os seguintes exemplos:  
 
-   A. Identificar a versão do utilitário **bcp**
  
-   B. Copiando linhas de tabela em um arquivo de dados (com uma conexão confiável)  
  
-   [C.](#c-copying-table-rows-into-a-data-file-with-mixed-mode-authentication) Copiando linhas de tabela em um arquivo de dados (com autenticação mista)  
  
-   D. Copiando dados de um arquivo em uma tabela  
  
-   E. Copiando uma coluna específica em um arquivo de dados  
  
-   F. Copiando uma linha específica em um arquivo de dados  
  
-   G. Copiando dados de uma consulta em um arquivo de dados  
  
-   H. Criando arquivos de formato
    
-   I. Usando um arquivo de formato para importação em massa com **bcp**  


### <a name="example-test-conditions"></a>**Condições de teste de exemplo**
Os exemplos abaixo utilizam o banco de dados de exemplo do `WideWorldImporters` para SQL Server (a partir de 2016) Banco de Dados SQL do Microsoft Azure.  `WideWorldImporters` pode ser baixado em [ https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0 ](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0).  Consulte [RESTORE (Transact-SQL)](../t-sql/statements/restore-statements-transact-sql.md) para obter a sintaxe para restaurar o banco de dados de exemplo.  Exceto quando especificado de outra forma, os exemplos presumem que você esteja usando a Autenticação do Windows e tenha uma conexão confiável com a instância do servidor na qual está executando o comando **bcp** .  Um diretório chamado `D:\BCP` será usado em muitos dos exemplos.

O script abaixo cria uma cópia vazia da tabela `WideWorldImporters.Warehouse.StockItemTransactions` e, em seguida, adiciona uma restrição de chave primária.  Executar a seguinte consulta de T-SQL no SSMS (SQL Server Management Studio)

```tsql  
USE WideWorldImporters;  
GO  

SET NOCOUNT ON;

IF NOT EXISTS (SELECT * FROM sys.tables WHERE name = 'Warehouse.StockItemTransactions_bcp')     
BEGIN
    SELECT * INTO WideWorldImporters.Warehouse.StockItemTransactions_bcp
    FROM WideWorldImporters.Warehouse.StockItemTransactions  
    WHERE 1 = 2;  

    ALTER TABLE Warehouse.StockItemTransactions_bcp 
    ADD CONSTRAINT PK_Warehouse_StockItemTransactions_bcp PRIMARY KEY NONCLUSTERED 
    (StockItemTransactionID ASC);
END
```

> [!NOTE]
> Trunque a tabela `StockItemTransactions_bcp` como desejar.
>
> TRUNCATE TABLE WideWorldImporters.Warehouse.StockItemTransactions_bcp;

### <a name="a--identify-bcp-utility-version"></a>A.  Identificar a versão do utilitário **bcp**
No prompt de comando, digite o seguinte comando:
```
bcp -v
```
  
### <a name="b-copying-table-rows-into-a-data-file-with-a-trusted-connection"></a>B. Copiando linhas de tabela em um arquivo de dados (com uma conexão confiável)  
Os exemplos a seguir ilustram a opção **out** na tabela `WideWorldImporters.Warehouse.StockItemTransactions` .

- **Basic**  
Este exemplo cria um arquivo de dados nomeado `StockItemTransactions_character.bcp` e copia os dados da tabela nesse arquivo usando o formato de **caractere** .

  No prompt de comando, digite o seguinte comando:
  ```
  bcp WideWorldImporters.Warehouse.StockItemTransactions out D:\BCP\StockItemTransactions_character.bcp -c -T
  ```
 
 - **Expanded**  
Este exemplo cria um arquivo de dados nomeado `StockItemTransactions_native.bcp` e copia os dados da tabela nesse arquivo usando formato **nativo** .  O exemplo também: especifica o número máximo de erros de sintaxe, um arquivo de erro e um arquivo de saída.

    No prompt de comando, digite o seguinte comando:
    ```
    bcp WideWorldImporters.Warehouse.StockItemTransactions OUT D:\BCP\StockItemTransactions_native.bcp -m 1 -n -e D:\BCP\Error_out.log -o D:\BCP\Output_out.log -S -T
    ``` 
 
Revise `Error_out.log` e `Output_out.log`.  `Error_out.log` deve ficar em branco.  Compare os tamanhos de arquivo entre `StockItemTransactions_character.bcp` e `StockItemTransactions_native.bcp`. 
   
### <a name="c-copying-table-rows-into-a-data-file-with-mixed-mode-authentication"></a>C. Copiando linhas de tabela em um arquivo de dados (com autenticação mista)  
O exemplo a seguir ilustra a opção **out** na tabela `WideWorldImporters.Warehouse.StockItemTransactions`.  Este exemplo cria um arquivo de dados nomeado `StockItemTransactions_character.bcp` e copia os dados da tabela nesse arquivo usando o formato de **caractere** .  
  
 O exemplo pressupõe que você esteja usando autenticação mista; é necessário usar a opção **-U** para especificar sua ID de logon. Além disso, a menos que você esteja se conectando à instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no computador local, use a opção **-S** para especificar o nome do sistema e, opcionalmente, um nome de instância.  

No prompt de comando, digite o seguinte comando: \(O sistema solicitará sua senha.\)
```  
bcp WideWorldImporters.Warehouse.StockItemTransactions out D:\BCP\StockItemTransactions_character.bcp -c -U<login_id> -S<server_name\instance_name>
```  
  
### <a name="d-copying-data-from-a-file-to-a-table"></a>D. Copiando dados de um arquivo em uma tabela  
Os exemplos a seguir ilustram a opção **in** na tabela `WideWorldImporters.Warehouse.StockItemTransactions_bcp` usando os arquivos criados acima.
  
- **Basic**  
Este exemplo usa o arquivo de dados `StockItemTransactions_character.bcp` criado anteriormente.

  No prompt de comando, digite o seguinte comando:
  ```  
  bcp WideWorldImporters.Warehouse.StockItemTransactions_bcp IN D:\BCP\StockItemTransactions_character.bcp -c -T  
  ```  

- **Expanded**  
Este exemplo usa o arquivo de dados `StockItemTransactions_native.bcp` criado anteriormente.  O exemplo também: usa a dica **TABLOCK**, especifica o tamanho do lote, o número máximo de erros de sintaxe, um arquivo de erro e um arquivo de saída.
  
  No prompt de comando, digite o seguinte comando:
  ```  
  bcp WideWorldImporters.Warehouse.StockItemTransactions_bcp IN D:\BCP\StockItemTransactions_native.bcp -b 5000 -h "TABLOCK" -m 1 -n -e D:\BCP\Error_in.log -o D:\BCP\Output_in.log -S -T 
  ```    
  Revise `Error_in.log` e `Output_in.log`.
   
### <a name="e-copying-a-specific-column-into-a-data-file"></a>E. Copiando uma coluna específica em um arquivo de dados  
Para copiar uma coluna específica, você pode usar a opção **queryout** .  O exemplo a seguir copia apenas a coluna `StockItemTransactionID` da tabela `Warehouse.StockItemTransactions` em um arquivo de dados. 
  
No prompt de comando, digite o seguinte comando:
  
```  
bcp "SELECT StockItemTransactionID FROM WideWorldImporters.Warehouse.StockItemTransactions WITH (NOLOCK)" queryout D:\BCP\StockItemTransactionID_c.bcp -c -T
```  
  
### <a name="f-copying-a-specific-row-into-a-data-file"></a>F. Copiando uma linha específica em um arquivo de dados  
Para copiar uma linha específica, você pode usar a opção **queryout** . O exemplo a seguir copia apenas a linha para o contato nomeado `Amy Trefl` da tabela `WideWorldImporters.Application.People` em um arquivo de dados `Amy_Trefl_c.bcp`.  Observação: a opção **-d** é usado para identificar o banco de dados.
  
No prompt de comando, digite o seguinte comando: 
```  
bcp "SELECT * from Application.People WHERE FullName = 'Amy Trefl'" queryout D:\BCP\Amy_Trefl_c.bcp -d WideWorldImporters -c -T
```  
  
### <a name="g-copying-data-from-a-query-to-a-data-file"></a>G. Copiando dados de uma consulta em um arquivo de dados  
Para copiar o conjunto de resultados de uma instrução Transact-SQL em um arquivo de dados, use a opção **queryout** .  O exemplo a seguir copia os nomes da tabela `WideWorldImporters.Application.People`, classificados pelo nome completo, no arquivo de dados `People.txt`.  Observação: a opção **-t** é usado para criar um arquivo delimitado por vírgula.
  
No prompt de comando, digite o seguinte comando:
```  
bcp "SELECT FullName, PreferredName FROM WideWorldImporters.Application.People ORDER BY FullName" queryout D:\BCP\People.txt -t, -c -T
```  
  
### <a name="h-creating-format-files"></a>H. Criando arquivos de formato  
O exemplo a seguir cria três arquivos de formato diferentes para a tabela `Warehouse.StockItemTransactions` no banco de dados do `WideWorldImporters`.  Revise o conteúdo de cada arquivo criado.
  
No prompt de comando, digite os seguintes comandos:
  
```  
REM non-XML character format
bcp WideWorldImporters.Warehouse.StockItemTransactions format nul -f D:\BCP\StockItemTransactions_c.fmt -c -T 

REM non-XML native format
bcp WideWorldImporters.Warehouse.StockItemTransactions format nul -f D:\BCP\StockItemTransactions_n.fmt -n -T

REM XML character format
bcp WideWorldImporters.Warehouse.StockItemTransactions format nul -f D:\BCP\StockItemTransactions_c.xml -x -c -T
 
```  
  
> [!NOTE]  
>  Para usar a opção **-x** , é necessário estar usando um cliente **bcp** 9.0. Para obter mais informações sobre como usar o cliente **bcp** 9.0, consulte "[Comentários](#remarks)."  
  
 Para obter mais informações, consulte [Arquivos de formato não XML &#40;SQL Server&#41;](../relational-databases/import-export/non-xml-format-files-sql-server.md) e [Arquivos de formato XML &#40;SQL Server&#41;](../relational-databases/import-export/xml-format-files-sql-server.md).  
  
### <a name="i-using-a-format-file-to-bulk-import-with-bcp"></a>I. Usando um arquivo de formato para importação em massa com bcp  
Para usar um arquivo de formato criado anteriormente ao importar dados para uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], use a opção **-f** com a opção **in** .  Por exemplo, o comando a seguir copia em massa o conteúdo de um arquivo de dados, `StockItemTransactions_character.bcp`, em uma cópia da tabela `Warehouse.StockItemTransactions_bcp` usando o arquivo de formato criado anteriormente `StockItemTransactions_c.xml`.  Observação: a opção **-L** é usado para importar apenas os 100 primeiros registros.
  
No prompt de comando, digite o seguinte comando:
```  
bcp WideWorldImporters.Warehouse.StockItemTransactions_bcp in D:\BCP\StockItemTransactions_character.bcp -L 100 -f D:\BCP\StockItemTransactions_c.xml -T 
```  
  
> [!NOTE]  
>  Os arquivos de formato são úteis quando os campos do arquivo de dados são diferentes das colunas da tabela, por exemplo, em seu número, classificação ou tipos de dados. Para obter mais informações, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
### <a name="j-specifying-a-code-page"></a>J. Especificando uma página de código  
 O exemplo de código parcial a seguir mostra a importação de bcp ao especificar uma página de código 65001:  
  
```  
bcp.exe MyTable in "D:\data.csv" -T -c -C 65001 -t , ...  
```  
  
 O exemplo de código parcial a seguir mostra a exportação de bcp ao especificar uma página de código 65001:  
  
```  
bcp.exe MyTable out "D:\data.csv" -T -c -C 65001 -t , ...  
```  
  
## <a name="additional-examples"></a>Exemplos adicionais  
|Os tópicos a seguir contêm exemplos sobre como usar o bcp: |
|---|
|Formatos de dados para importar ou exportar em massa (SQL Server)<br />&emsp;&#9679;&emsp;[Usar o formato nativo para importar ou exportar dados (SQL Server)](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar o formato de caractere para importar ou exportar dados (SQL Server)](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar o formato nativo Unicode para importar ou exportar dados (SQL Server)](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar o formato de caractere Unicode para importar ou exportar dados (SQL Server)](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)<br /><br />[Especificar terminadores de campo e linha (SQL Server)](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)<br /><br />[Manter valores nulos ou use os valores padrão durante a importação em massa (SQL Server)](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)<br /><br />[Manter valores de identidade ao importar dados em massa (SQL Server)](../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)<br /><br />Arquivos de formato para importação ou exportação de dados (SQL Server))<br />&emsp;&#9679;&emsp;[Criar um formato de arquivo (SQL Server)](../relational-databases/import-export/create-a-format-file-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar um arquivo de formato para importação em massa de dados (SQL Server)](../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar um arquivo de formato para ignorar uma coluna de tabela (SQL Server)](../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar um arquivo de formato para ignorar um campo de dados (SQL Server)](../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados (SQL Server)](../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)<br /><br />[Exemplos de importação e exportação em massa de documentos XML (SQL Server)](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)<br /><p>                                                                                                                                                                                                                  </p>|

## <a name="see-also"></a>Consulte Também  
 [Preparar dados para exportar ou importar em massa &#40;SQL Server&#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../t-sql/functions/openrowset-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_tableoption &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)   
 [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)  
  
  
