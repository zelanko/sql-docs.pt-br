---
title: utilitário tablediff
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- comparing data
- tablediff utility
- tables [SQL Server replication]
- table comparisons [SQL Server]
- command prompt utilities [SQL Server], tablediff
- troubleshooting [SQL Server replication], non-convergence
- non-convergence [SQL Server]
ms.assetid: 3c3cb865-7a4d-4d66-98f2-5935e28929fc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: cb12cc164490e249dae13ef22cdd5279a0427102
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75304803"
---
# <a name="tablediff-utility"></a>utilitário tablediff
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  O utilitário **tablediff** é usado para comparar dados em duas tabelas para não convergência e é particularmente útil para solução de problemas de não convergência em uma topologia de replicação. Esse utilitário pode ser usado no prompt de comando ou em um arquivo em lotes para executar as seguintes tarefas:  
  
-   Uma comparação linha por linha entre uma tabela de origem em uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] agindo como um Publicador de replicação e a tabela de destino em uma ou mais instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] agindo como Assinantes de replicação.  
  
-   Executa uma comparação rápida comparando apenas contagens de linha e esquema.  
  
-   Executar comparações em nível de coluna.  
  
-   Gerar um script [!INCLUDE[tsql](../includes/tsql-md.md)] para corrigir discrepâncias no servidor de destino a fim de que haja convergência entre as tabelas de origem e de destino.  
  
-   Registrar resultados em um arquivo de saída ou em uma tabela no banco de dados de destino.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
tablediff   
[ -? ] |   
{  
        -sourceserver source_server_name[\instance_name]  
        -sourcedatabase source_database  
        -sourcetable source_table_name   
    [ -sourceschema source_schema_name ]  
    [ -sourcepassword source_password ]  
    [ -sourceuser source_login ]  
    [ -sourcelocked ]  
        -destinationserver destination_server_name[\instance_name]  
        -destinationdatabase subscription_database   
        -destinationtable destination_table   
    [ -destinationschema destination_schema_name ]  
    [ -destinationpassword destination_password ]  
    [ -destinationuser destination_login ]  
    [ -destinationlocked ]  
    [ -b large_object_bytes ]   
    [ -bf number_of_statements ]   
    [ -c ]   
    [ -dt ]   
    [ -et table_name ]   
    [ -f [ file_name ] ]   
    [ -o output_file_name ]   
    [ -q ]   
    [ -rc number_of_retries ]   
    [ -ri retry_interval ]   
    [ -strict ]  
    [ -t connection_timeouts ]   
}  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **-?** ]  
 Retorna a lista de parâmetros com suporte.  
  
 **-sourceserver** _source_server_name_[ **\\** _instance\_name_]  
 É o nome do servidor de origem. Especifique *source_server_name* para a instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Especifique _source_server_name_ **\\** _instance_name_ para uma instância nomeada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **-sourcedatabase** _source_database_  
 É o nome do banco de dados de origem.  
  
 **-sourcetable** _source_table_name_  
 É o nome da tabela de origem que está sendo verificada.  
  
 **-sourceschema** _source_schema_name_  
 O proprietário de esquema da tabela de origem. Por padrão, supõe-se que o proprietário de tabela seja dbo.  
  
 **-sourcepassword** _source_password_  
 É a senha para o logon usada para a conexão com o servidor de origem que usa Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Quando possível, forneça credenciais de segurança em runtime. Se você precisar armazenar credenciais em um arquivo de script, deverá proteger o arquivo para evitar acesso não autorizado.  
  
 **-sourceuser** _source_login_  
 É o logon usado para a conexão com o servidor de origem que usa Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Se *source_login* não for fornecido, então a autenticação do Windows será usada no momento da conexão com o servidor de origem. [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]  
  
 **-sourcelocked**  
 A tabela de origem é bloqueada durante a comparação que usa dicas de tabela TABLOCK e HOLDLOCK.  
  
 **-DestinationServer** _destination_server_name_[ **\\** _instance_name_]  
 É o nome do servidor de destino. Especifique *destination_server_name* para a instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Especifique _destination_server_name_ **\\** _instance_name_ para uma instância nomeada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **-destinationdatabase** _subscription_database_  
 É o nome do banco de dados de destino.  
  
 **-destinationtable** _destination_table_  
 É o nome da tabela de destino.  
  
 **-destinationschema** _destination_schema_name_  
 O proprietário de esquema da tabela de destino. Por padrão, supõe-se que o proprietário de tabela seja dbo.  
  
 **-destinationpassword** _destination_password_  
 É a senha para o logon usada para a conexão com o servidor de destino que usa Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Quando possível, forneça credenciais de segurança em runtime. Se você precisar armazenar credenciais em um arquivo de script, deverá proteger o arquivo para evitar acesso não autorizado.  
  
 **-destinationuser** _destination_login_  
 É o logon usado para a conexão com o servidor de destino que usa Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Se *destination_login* não for fornecido, então a autenticação do Windows será usada no momento da conexão com o servidor. [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]  
  
 **-destinationlocked**  
 A tabela de destino é bloqueada durante a comparação que usa dicas de tabela TABLOCK e HOLDLOCK.  
  
 **-b** _large_object_bytes_  
 É o número de bytes a comparar para colunas do tipo de dados de objeto grande, que inclui: **text**, **ntext**, **image**, **varchar(max)** , **nvarchar(max)** e **varbinary(max)** . *large_object_bytes* segue o padrão do tamanho da coluna. Os dados acima de *large_object_bytes* não serão comparados.  
  
 **-bf** _number_of_statements_  
 É o número de instruções [!INCLUDE[tsql](../includes/tsql-md.md)] a serem gravadas no arquivo de script [!INCLUDE[tsql](../includes/tsql-md.md)] atual quando a opção **-f** é usada. Quando o número de instruções [!INCLUDE[tsql](../includes/tsql-md.md)] exceder *number_of_statements*, um arquivo de script [!INCLUDE[tsql](../includes/tsql-md.md)] novo será criado.  
  
 **-c**  
 Compare diferenças em nível de coluna.  
  
 **- dt**  
 Descarte a tabela de resultado especificada por *table_name*, se a tabela já existir.  
  
 **-et** _table_name_  
 Especifica o nome da tabela de resultado a ser criada. Se essa tabela já existir, **-DT** deverá ser usado ou ocorrerá falha na operação.  
  
 **-f** [ *file_name* ]  
 Gera um script [!INCLUDE[tsql](../includes/tsql-md.md)] para trazer a tabela ao servidor de destino em convergência com a tabela no servidor de origem. Pode-se optar por especificar um nome e caminho para o arquivo de script [!INCLUDE[tsql](../includes/tsql-md.md)] gerado. Se *file_name* não for especificado, o arquivo de script [!INCLUDE[tsql](../includes/tsql-md.md)] será gerado no diretório no qual o utilitário é executado.  
  
 **-o** _output_file_name_  
 É o nome e caminho completo do arquivo de saída.  
  
 **-q**  
 Executa uma comparação rápida comparando apenas contagens de linha e esquema.  
  
 **-rc** _number_of_retries_  
 Número de vezes que o utilitário repete uma operação com falha.  
  
 **-ri** _retry_interval_  
 Intervalo, em segundos, a esperar entre repetições.  
  
 **-strict**  
 Esquema de destino e origem são comparados de forma rigorosa.  
  
 **-t** _connection_timeouts_  
 Define o período de tempo limite da conexão, em segundos, para conexões para o servidor de origem e servidor de destino.  
  
## <a name="return-value"></a>Valor retornado  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Sucesso|  
|**1**|Erro crítico|  
|**2**|Diferenças de tabela|  
  
## <a name="remarks"></a>Comentários  
 O utilitário **tablediff** não pode ser usado com servidores não [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Não há suporte para tabelas com colunas de tipo de dados **sql_variant** .  
  
 Por padrão, o utilitário **tablediff** dá suporte aos mapeamentos de tipo de dados a seguir entre colunas de origem e de destino.  
  
|Tipo de dados de origem|Tipo de dados de destino|  
|----------------------|---------------------------|  
|**tinyint**|**smallint**, **int**ou **bigint**|  
|**smallint**|**int** ou **bigint**|  
|**int**|**bigint**|  
|**timestamp**|**varbinary**|  
|**varchar(max)**|**text**|  
|**nvarchar(max)**|**ntext**|  
|**varbinary(max)**|**imagem**|  
|**text**|**varchar(max)**|  
|**ntext**|**nvarchar(max)**|  
|**imagem**|**varbinary(max)**|  
  
 Use a opção **-strict** para desabilitar esses mapeamentos e executar uma validação rigorosa.  
  
 A tabela de origem na comparação deve conter pelo menos uma chave primária, identidade ou coluna ROWGUID. Quando você usa a opção **-strict** , a tabela de destino também deve ter uma chave primária, identidade ou coluna ROWGUID.  
  
 O script [!INCLUDE[tsql](../includes/tsql-md.md)] gerado para trazer a tabela de destino em convergência não inclui os seguintes tipos de dados:  
  
-   **varchar(max)**  
  
-   **nvarchar(max)**  
  
-   **varbinary(max)**  
  
-   **timestamp**  
  
-   **xml**  
  
-   **text**  
  
-   **ntext**  
  
-   **imagem**  
  
## <a name="permissions"></a>Permissões  
 Para comparar tabelas, é preciso ter permissões SELECT ALL nos objetos de tabela que são comparados.  
  
 Para usar a opção **-et** é preciso ser membro da função de banco de dados fixo db_owner ou pelo menos ter permissão CREATE TABLE no banco de dados de assinatura e permissão ALTER no esquema de proprietário de destino no servidor de destino.  
  
 Para usar a opção **-dt** é preciso ser membro da função de banco de dados fixo db_owner ou pelo menos ter permissão ALTER no esquema de proprietário do destino no servidor de destino.  
  
 Para usar as opções **-o** ou **-f** , é preciso ter permissão de gravação para o local de diretório de arquivos especificado.  
  
## <a name="see-also"></a>Consulte Também  
 [Comparar tabelas replicadas para descobrir diferenças &#40;Programação de replicação&#41;](../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)  
  
  
