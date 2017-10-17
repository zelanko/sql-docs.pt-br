---
title: Criar banco de dados (banco de dados do SQL Azure) | Microsoft Docs
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 08/28/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SERVICE_OBJECTIVE
- SERVICE_OBJECTIVE_TSQL
- ELASTIC_POOL
- ELASTIC_POOL_TSQL
- EDITION
- EDITION_TSQL
- MAXSIZE
- MAXSIZE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVICE_OBJECTIVE
- ELASTIC_POOL
- EDITION SQL Database
- MAXSIZE SQL Database
ms.assetid: 22b167f7-ae86-490b-adb3-ec02ca1c1508
caps.latest.revision: 62
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: e9781bd657f094c7be57ae513cc2c4a026ad4746
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="create-database-azure-sql-database"></a>CREATE DATABASE (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Cria um novo banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
``` 
  
CREATE DATABASE database_name [ COLLATE collation_name ]  
{  
   (<edition_options> [, ...n])   
}  

[ WITH CATALOG_COLLATION = { DATABASE_DEFAULT | SQL_Latin1_General_CP1_CI_AS }  ]
  
<edition_options> ::=   
{  

      MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 … 1024 … 4096 GB }    
    | ( EDITION = {  'basic' | 'standard' | 'premium' | 'premiumrs'}   
    | SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' | 
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'  
            | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' 
            | { ELASTIC_POOL(name = <elastic_pool_name>) } }  ) 
}  

 [;]  
  

```  

```
To copy a database:  
CREATE DATABASE database_name  
    AS COPY OF [source_server_name.] source_database_name  
    [ ( SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |  
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'  
            | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' 
            | { ELASTIC_POOL(name = <elastic_pool_name>) } } )  
    ]  
 [;] 
 
```  
  
## <a name="arguments"></a>Argumentos  
 Este diagrama de sintaxe demonstra os argumentos com suporte no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 *database_name*  
 O nome do novo banco de dados. Esse nome deve ser exclusivo no SQL server, que pode hospedar ambos [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] bancos de dados e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] bancos de dados e estar de acordo com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] regras para identificadores. Para obter mais informações, consulte [identificadores](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
 *Collation_name*  
 Especifica o agrupamento padrão do banco de dados. O nome do agrupamento pode ser um nome de agrupamento do Windows ou um nome de agrupamento SQL. Se não for especificado, o banco de dados será atribuído o agrupamento padrão, que é SQL_Latin1_General_CP1_CI_AS.  
  
 Para obter mais informações sobre os nomes de agrupamentos do Windows e do SQL, [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx).  
  
 *CATALOG_COLLATION*  
Especifica o agrupamento padrão para o catálogo de metadados. *DATABASE_DEFAULT* Especifica que o catálogo de metadados usado para exibições do sistema e tabelas do sistema ser agrupadas para corresponder ao agrupamento padrão do banco de dados.  Esse é o comportamento encontrado no SQL Server. 

*SQL_Latin1_General_CP1_CI_AS* Especifica que o catálogo de metadados usado para tabelas e exibições do sistema ser agrupadas em um agrupamento SQL_Latin1_General_CP1_CI_AS fixado.  Essa é a configuração padrão no banco de dados do SQL Azure se não for especificado.

 *EDIÇÃO*  
 Especifica a camada de serviço do banco de dados. Os valores disponíveis são: 'basic', 'padrão', 'premium' e 'premiumrs'.  
  
 Quando EDITION for especificado, mas MAXSIZE não for especificado, MAXSIZE será definido como o tamanho mais restritivo com suporte na edição.  
  
 *MAXSIZE*  
 Especifica o tamanho máximo do banco de dados. MAXSIZE deve ser válido para a EDIÇÃO especificada (camada de serviço) A seguir, estão os valores com suporte para MAXSIZE e os padrões (D) para as camadas de serviço.  
  
|**MAXSIZE**|**Basic**|**S2 S0**|**/S12 S3**|**P1 P6 e PRS1 PRS6**| **P11 P15** 
|-----------------|---------------|------------------|-----------------|-----------------|-----------------|-----------------|  
|100 MB|√|√|√|√|√|  
|250 MB|√|√|√|√|√|  
|500 MB|√|√|√|√|√|  
|1 GB|√|√|√|√|√|  
|2 GB|√ (D)|√|√|√|√|  
|5 GB|N/A|√|√|√|√|  
|10 GB|N/A|√|√|√|√|  
|20 GB|N/A|√|√|√|√|  
|30 GB|N/A|√|√|√|√|  
|40 GB|N/A|√|√|√|√|  
|50 GB|N/A|√|√|√|√|  
|100 GB|N/A|√|√|√|√|  
|150 GB|N/A|√|√|√|√|  
|200 GB|N/A|√|√|√|√|  
|250 GB|N/A|√ (D)|√ (D)|√|√|  
|300 GB|N/A|N/A|√|√|√|  
|400 GB|N/A|N/A|√|√|√|
|500 GB|N/A|N/A|√|√ (D)|√|
|750 GB|N/A|N/A|√|√|√|
|1024 GB|N/A|N/A|√|√|√ (D)|
|De 1024 GB até 4096 GB em incrementos de 256 GB * |N/A|N/A|N/A|N/A|√|√|  
  
 \*P11 e P15 permitem MAXSIZE até 4 TB com 1024 GB, sendo o tamanho padrão.  P11 e P15 podem usar até 4 TB de armazenamento incluído sem custos adicionais. Na camada Premium, MAXSIZE maior que 1 TB está atualmente disponível nas seguintes regiões: US East2, oeste dos EUA, nos Gov Virgínia, Europa Ocidental, Alemanha Central, Sul Leste da Ásia, Leste do Japão, Leste da Austrália, Canadá Central e Leste do Canadá. Para limitações atuais, consulte [único bancos de dados](https://docs.microsoft.com/azure/sql-database-single-database-resources).  
  
 As regras a seguir se aplicam aos argumentos MAXSIZE e EDITION:  
  
-   O valor MAXSIZE, se especificado, precisa ser um valor válido exibido na tabela acima.  
  
-   Se EDITION for especificado, mas MAXSIZE não for especificado, o valor padrão da edição será usado. Por exemplo, se EDITION for definido para Standard e MAXSIZE não for especificado, em seguida, o MAXSIZE é automaticamente definido como 250 MB.  
  
-   Se MAXSIZE nem EDITION for especificado, a edição é definida como padrão (S0) e MAXSIZE for definido como 250 GB.  
  
 SERVICE_OBJECTIVE  
 Especifica o nível de desempenho. Para descrições de objetivo de serviço e obter mais informações sobre o tamanho, as edições e as combinações de objetivos de serviço, consulte [camadas de serviço de banco de dados SQL do Azure e níveis de desempenho](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) e [recursos de banco de dados SQL limites de](https://azure.microsoft.com/documentation/articles/sql-database-resource-limits). Se o SERVICE_OBJECTIVE especificado não tiver suporte pela EDITION, você receberá um erro.  
  
 ELASTIC_POOL (nome = \<elastic_pool_name >) para criar um novo banco de dados em um pool Elástico de banco de dados, definir SERVICE_OBJECTIVE do banco de dados para ELASTIC_POOL e forneça o nome do pool. Para obter mais informações, consulte [criar e gerenciar um pool de banco de dados Elástico de banco de dados SQL (visualização)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/).  
  
 *COMO a cópia de [source_server_name]. source_database_name*  
 Para copiar um banco de dados para o mesmo servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ou um servidor diferente.  
  
 *source_server_name*  
 O nome do servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] onde o banco de dados de origem está localizado. Esse parâmetro é opcional quando o banco de dados de origem e o banco de dados de destino devem estar localizados no mesmo servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Observação: o argumento `AS COPY OF` não oferece suporte aos nomes de domínio exclusivos totalmente qualificados. Em outras palavras, se o nome de domínio totalmente qualificado do seu servidor for `serverName.database.windows.net`, use somente `serverName` durante a cópia do banco de dados.  
  
 *source_database_name*  
 O nome do banco de dados que deve ser copiado.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]não dá suporte aos seguintes argumentos e opções ao usar o `CREATE DATABASE` instrução:  
  
-   Os parâmetros relacionados ao posicionamento físico do arquivo, como \<filespec > e \<filegroup >  
  
-   Opções de acesso externo, como DB_CHAINING e TRUSTWORTHY  
  
-   Anexando um banco de dados  
  
-   Opções do service broker, como ENABLE_BROKER, NEW_BROKER e ERROR_BROKER_CONVERSATIONS  
  
-   Instantâneo do banco de dados  
  
 Para obter mais informações sobre os argumentos e a `CREATE DATABASE` instrução, consulte [CREATE DATABASE &#40; Servidor SQL Transact-SQL &#41; ](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
 Os bancos de dados no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] tem várias configurações padrão que são definidas quando o banco de dados é criado. Para obter mais informações sobre essas configurações padrão, consulte a lista de valores em [DATABASEPROPERTYEX &#40; Transact-SQL &#41; ](../../t-sql/functions/databasepropertyex-transact-sql.md).  
  
 MAXSIZE fornece a capacidade de limitar o tamanho do banco de dados. Se o tamanho do banco de dados atingir seu MAXSIZE, você receberá o código de erro 40544. Quando isso ocorre, você não pode inserir ou atualizar dados nem criar novos objetos (como tabelas, procedimentos armazenados, exibições e funções). No entanto, você ainda pode ler e excluir dados, truncar tabelas, descartar tabelas e índices e reconstruir índices. Você pode atualizar MAXSIZE para um valor maior que o tamanho atual do banco de dados ou excluir alguns dados para liberar espaço de armazenamento. Pode haver um atraso máximo de quinze minutos para que você possa inserir novos dados.  
  
> [!IMPORTANT]  
>  A instrução `CREATE DATABASE` deve ser a única instrução em um lote do [!INCLUDE[tsql](../../includes/tsql-md.md)]. 
  
 Para alterar o tamanho, edição ou valores de objetivo de serviço posteriormente, use [ALTER DATABASE &#40; Banco de dados SQL do Azure &#41; ](../../t-sql/statements/alter-database-azure-sql-database.md).  

O argumento CATALOG_COLLATION só está disponível durante a criação do banco de dados. 
  
## <a name="database-copies"></a>Cópias de banco de dados  
 Copiar um banco de dados usando o `CREATE DATABASE` instrução é uma operação assíncrona. Portanto, uma conexão com o servidor de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] não é necessária para a duração completa do processo de cópia. O `CREATE DATABASE` instrução retorna o controle para o usuário depois que a entrada em sys. Databases é criada, mas antes da cópia de banco de dados a operação for concluída. Em outras palavras, a instrução `CREATE DATABASE` é retornada com êxito quando a cópia do banco de dados ainda está em andamento.  
  
-   Monitorando o processo de cópia em um [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] server: consulta o `percentage_complete` ou `replication_state_desc` colunas no [dm_database_copies](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md) ou o `state` coluna o **sys. Databases** modo de exibição. O [sys.DM operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) exibição também retorna o status das operações de banco de dados, incluindo a cópia do banco de dados pode ser usada.  
  
 Quando o processo de cópia é concluído com êxito, o banco de dados de destino fica transacionalmente consistente com o banco de dados de origem.  
  
 A seguinte sintaxe e as regras semânticas aplicam-se ao uso do argumento `AS COPY OF`:  
  
-   Os nomes do servidor de origem e do servidor para o destino de impressão podem ser iguais ou diferentes. Quando eles forem iguais, esse parâmetro é opcional e o contexto do servidor da sessão atual é usado por padrão.  
  
-   Os nomes do banco de dados de origem e destino devem ser especificados, exclusivo e estarem em conformidade com as regras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para identificadores. Para obter mais informações, consulte [identificadores](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
-   A instrução `CREATE DATABASE` deve ser executada dentro do contexto do banco de dados mestre do servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] em que o novo banco de dados será criado.  
  
-   Depois de a cópia ser concluída, o banco de dados de destino deve ser gerenciado como um banco de dados independente. Você pode executar as instruções `ALTER DATABASE` e `DROP DATABASE` no novo banco de dados independentemente do banco de dados de origem. Você também pode copiar o novo banco de dados para outro novo banco de dados.  
  
-   O banco de dados de origem pode continuar a ser acessado enquanto a cópia do banco de dados está em andamento.  
  
 Para obter mais informações, consulte [criar uma cópia de um banco de dados do SQL Azure usando o Transact-SQL](https://azure.microsoft.com/documentation/articles/sql-database-copy-transact-sql/).  
  
## <a name="permissions"></a>Permissões  
 Para criar um logon de um banco de dados deve ser um dos seguintes:  
  
-   O logon principal no nível de servidor  
  
-   O administrador do AD do Azure para o servidor local do SQL Azure  
  
-   Um logon que é membro de `dbmanager` função de banco de dados  
  
 **Requisitos adicionais para uso `CREATE DATABASE ... AS COPY OF` sintaxe:** o logon que está executando a instrução no servidor local também deve ser pelo menos o `db_owner` no servidor de origem. Se o logon for baseado em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação, o logon que está executando a instrução no servidor local deve ter um logon correspondente na fonte de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server, com um nome idêntico e uma senha.  
  
## <a name="examples"></a>Exemplos  
Para obter um tutorial de início rápido mostrando como se conectar a um banco de dados do SQL Azure usando o SQL Server Management Studio, consulte [banco de dados do SQL Azure: Use SQL Server Management Studio para se conectar e consultar dados](/azure/sql-database/sql-database-connect-query-ssms).  
  
### <a name="simple-example"></a>Exemplo simples  
 Um exemplo simples para a criação de um banco de dados.  
  
```tsql  
CREATE DATABASE TestDB1;  
```  
  
### <a name="simple-example-with-edition"></a>Exemplo simples com edição  
 Um exemplo simples para a criação de um banco de dados padrão.  
  
```tsql  
CREATE DATABASE TestDB2  
( EDITION = 'standard' );  
```  
  
### <a name="example-with-additional-options"></a>Exemplo com opções adicionais  
 Um exemplo de uso de várias opções.  
  
```tsql  
CREATE DATABASE hito   
COLLATE Japanese_Bushu_Kakusu_100_CS_AS_KS_WS   
( MAXSIZE = 500 MB, EDITION = 'standard', SERVICE_OBJECTIVE = 'S1' ) ;  
```  
  
### <a name="creating-a-copy"></a>Criando uma cópia  
 Um exemplo de criação de uma cópia de um banco de dados.  
  
```tsql  
CREATE DATABASE escuela   
AS COPY OF school;  
```  
  
### <a name="creating-a-database-in-an-elastic-pool"></a>Criando um banco de dados em um Pool Elástico  
 Cria um novo banco de dados no pool chamado S3M100:  
  
```tsql  
CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = S3M100 ) ) ;  
```  
  
### <a name="creating-a-copy-of-a-database-on-another-server"></a>Criando uma cópia de um banco de dados em outro servidor  
 O exemplo a seguir cria uma cópia do banco de dados db_original, denominado db_copy no nível de desempenho P2 para um único banco de dados.  Isso é verdadeiro independentemente de ser db_original em um nível de desempenho para um único banco de dados ou de um pool Elástico.  
  
```tsql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original ( SERVICE_OBJECTIVE = 'P2' )  ;  
```  
  
 O exemplo a seguir cria uma cópia do banco de dados db_original, denominado db_copy em um pool Elástico denominado ep1.  Isso é verdadeiro independentemente de ser db_original em um nível de desempenho para um único banco de dados ou de um pool Elástico.  Se db_original estiver em um pool Elástico com um nome diferente, db_copy ainda é criado no ep1.  
  
```tsql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original   
    (SERVICE_OBJECTIVE = ELASTIC_POOL( name = ep1 ) ) ;  
```  

### <a name="create-database-with-specified-catalog-collation-value"></a>Criar banco de dados com valor de agrupamento de catálogo especificado

O exemplo a seguir define o agrupamento de catálogo para DATABASE_DEFAULT durante a criação do banco de dados, que define o agrupamento de catálogo a ser o mesmo que o agrupamento de banco de dados.

```tsql
CREATE DATABASE TestDB3 COLLATE Japanese_XJIS_140  (MAXSIZE = 100 MB, EDITION = ‘basic’)  
      WITH CATALOG_COLLATION = DATABASE_DEFAULT 
```
  
## <a name="see-also"></a>Consulte também  

-  [sys.DM database_copies &#40; Banco de dados SQL do Azure &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)

-   [ALTER DATABASE &#40; Banco de dados SQL do Azure &#41;](alter-database-azure-sql-database.md)   
    
  


