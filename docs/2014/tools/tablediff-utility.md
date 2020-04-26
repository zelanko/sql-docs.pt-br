---
title: Utilitário tablediff | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cb8b8bec38b428ca7b2eea5166867141b34a2405
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68185968"
---
# <a name="tablediff-utility"></a>utilitário tablediff
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
        -sourceserversource_server_name[\instance_name]  
        -sourcedatabasesource_database-sourcetablesource_table_name   
    [ -sourceschemasource_schema_name ]  
    [ -sourcepasswordsource_password ]  
    [ -sourceusersource_login ]  
    [ -sourcelocked ]  
        -destinationserverdestination_server_name[\instance_name]  
        -destinationdatabasesubscription_database-destinationtabledestination_table   
    [ -destinationschemadestination_schema_name ]  
    [ -destinationpassworddestination_password ]  
    [ -destinationuserdestination_login ]  
    [ -destinationlocked ]  
    [ -blarge_object_bytes ]   
    [ -bfnumber_of_statements ]   
    [ -c ]   
    [ -dt ]   
    [ -ettable_name ]   
    [ -f [ file_name ] ]   
    [ -ooutput_file_name ]   
    [ -q ]   
    [ -rcnumber_of_retries ]   
    [ -riretry_interval ]   
    [ -strict ]  
    [ -tconnection_timeouts ]   
}  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **-?** ]  
 Retorna a lista de parâmetros com suporte.  
  
 **-SourceServer** *source_server_name*[**\\**_instance_name_]  
 É o nome do servidor de origem. Especifique _o\_nome\_do servidor de origem_ para a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]instância padrão do. Especifique o**\\**_nome da instância\__ do _nome do\_\_servidor de origem_para uma instância nomeada do. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
 **-sourcedatabase** *source_database*  
 É o nome do banco de dados de origem.  
  
 **-sourcetable** *source_table_name*  
 É o nome da tabela de origem que está sendo verificada.  
  
 **-sourceschema** *source_schema_name*  
 O proprietário de esquema da tabela de origem. Por padrão, supõe-se que o proprietário de tabela seja dbo.  
  
 **-sourcepassword** *source_password*  
 É a senha para o logon usada para a conexão com o servidor de origem que usa Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Quando possível, forneça credenciais de segurança em runtime. Se você precisar armazenar credenciais em um arquivo de script, deverá proteger o arquivo para evitar acesso não autorizado.  
  
 **-sourceuser** *source_login*  
 É o logon usado para a conexão com o servidor de origem que usa Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Se *source_login* não for fornecido, então a autenticação do Windows será usada no momento da conexão com o servidor de origem. [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]  
  
 **-sourcelocked**  
 A tabela de origem é bloqueada durante a comparação que usa dicas de tabela TABLOCK e HOLDLOCK.  
  
 **-DestinationServer** *destination_server_name*[**\\**_nome\_da instância_]  
 É o nome do servidor de destino. Especifique *destination_server_name* para a instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Especifique o**\\**_nome da instância\__ do _nome do\_\_servidor de destino_para uma instância nomeada do. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
 **-destinationdatabase** *subscription_database*  
 É o nome do banco de dados de destino.  
  
 **-destinationtable** *destination_table*  
 É o nome da tabela de destino.  
  
 **-destinationschema** *destination_schema_name*  
 O proprietário de esquema da tabela de destino. Por padrão, supõe-se que o proprietário de tabela seja dbo.  
  
 **-destinationpassword** *destination_password*  
 É a senha para o logon usada para a conexão com o servidor de destino que usa Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Quando possível, forneça credenciais de segurança em runtime. Se você precisar armazenar credenciais em um arquivo de script, deverá proteger o arquivo para evitar acesso não autorizado.  
  
 **-destinationuser** *destination_login*  
 É o logon usado para a conexão com o servidor de destino que usa Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Se *destination_login* não for fornecido, então a autenticação do Windows será usada no momento da conexão com o servidor. [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]  
  
 **-destinationlocked**  
 A tabela de destino é bloqueada durante a comparação que usa dicas de tabela TABLOCK e HOLDLOCK.  
  
 **-b** *large_object_bytes*  
 É o número de bytes a comparar para colunas de tipo de dados de objetos grandes, o que inclui padrões de: `text`, `ntext`, `image`, `varchar(max)`, `nvarchar(max)` e `varbinary(max)`. *large_object_bytes* segue o padrão do tamanho da coluna. Os dados acima de *large_object_bytes* não serão comparados.  
  
 **-bf** *number_of_statements*  
 É o número de instruções [!INCLUDE[tsql](../includes/tsql-md.md)] a serem gravadas no arquivo de script [!INCLUDE[tsql](../includes/tsql-md.md)] atual quando a opção **-f** é usada. Quando o número de instruções [!INCLUDE[tsql](../includes/tsql-md.md)] exceder *number_of_statements*, um arquivo de script [!INCLUDE[tsql](../includes/tsql-md.md)] novo será criado.  
  
 **-c**  
 Compare diferenças em nível de coluna.  
  
 **- dt**  
 Descarte a tabela de resultado especificada por *table_name*, se a tabela já existir.  
  
 **-et** *table_name*  
 Especifica o nome da tabela de resultado a ser criada. Se essa tabela já existir, **-DT** deverá ser usado ou ocorrerá falha na operação.  
  
 **-f** [ *file_name* ]  
 Gera um script [!INCLUDE[tsql](../includes/tsql-md.md)] para trazer a tabela ao servidor de destino em convergência com a tabela no servidor de origem. Pode-se optar por especificar um nome e caminho para o arquivo de script [!INCLUDE[tsql](../includes/tsql-md.md)] gerado. Se *file_name* não for especificado, o arquivo de script [!INCLUDE[tsql](../includes/tsql-md.md)] será gerado no diretório no qual o utilitário é executado.  
  
 **-o** *output_file_name*  
 É o nome e caminho completo do arquivo de saída.  
  
 **-q**  
 Executa uma comparação rápida comparando apenas contagens de linha e esquema.  
  
 **-rc** *number_of_retries*  
 Número de vezes que o utilitário repete uma operação com falha.  
  
 **-ri** *retry_interval*  
 Intervalo, em segundos, a esperar entre repetições.  
  
 **-strict**  
 Esquema de destino e origem são comparados de forma rigorosa.  
  
 **-t** *connection_timeouts*  
 Define o período de tempo limite da conexão, em segundos, para conexões para o servidor de origem e servidor de destino.  
  
## <a name="return-value"></a>Valor retornado  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**0**|Sucesso|  
|**1**|Erro crítico|  
|**2**|Diferenças de tabela|  
  
## <a name="remarks"></a>Comentários  
 O utilitário **tablediff** não pode ser usado com[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] servidores não.  
  
 Não há suporte para tabelas com colunas de tipo de dados `sql_variant`.  
  
 Por padrão, o utilitário **tablediff** dá suporte aos mapeamentos de tipo de dados a seguir entre colunas de origem e de destino.  
  
|Tipo de dados de origem|Tipo de dados de destino|  
|----------------------|---------------------------|  
|`tinyint`|`smallint`, `int` ou `bigint`|  
|`smallint`|`int` ou `bigint`|  
|`int`|`bigint`|  
|`timestamp`|`varbinary`|  
|`varchar(max)`|`text`|  
|`nvarchar(max)`|`ntext`|  
|`varbinary(max)`|`image`|  
|`text`|`varchar(max)`|  
|`ntext`|`nvarchar(max)`|  
|`image`|`varbinary(max)`|  
  
 Use a opção **-strict** para desabilitar esses mapeamentos e executar uma validação rigorosa.  
  
 A tabela de origem na comparação deve conter pelo menos uma chave primária, identidade ou coluna ROWGUID. Quando você usa a opção **-strict** , a tabela de destino também deve ter uma chave primária, identidade ou coluna ROWGUID.  
  
 O script [!INCLUDE[tsql](../includes/tsql-md.md)] gerado para trazer a tabela de destino em convergência não inclui os seguintes tipos de dados:  
  
-   `varchar(max)`  
  
-   `nvarchar(max)`  
  
-   `varbinary(max)`  
  
-   `timestamp`  
  
-   **xml**  
  
-   `text`  
  
-   `ntext`  
  
-   `image`  
  
## <a name="permissions"></a>Permissões  
 Para comparar tabelas, é preciso ter permissões SELECT ALL nos objetos de tabela que são comparados.  
  
 Para usar a opção **-et** é preciso ser membro da função de banco de dados fixo db_owner ou pelo menos ter permissão CREATE TABLE no banco de dados de assinatura e permissão ALTER no esquema de proprietário de destino no servidor de destino.  
  
 Para usar a opção **-dt** é preciso ser membro da função de banco de dados fixo db_owner ou pelo menos ter permissão ALTER no esquema de proprietário do destino no servidor de destino.  
  
 Para usar as opções **-o** ou **-f** , é preciso ter permissão de gravação para o local de diretório de arquivos especificado.  
  
## <a name="see-also"></a>Consulte Também  
 [Comparar tabelas replicadas para descobrir diferenças &#40;Programação de replicação&#41;](../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)  
  
  
