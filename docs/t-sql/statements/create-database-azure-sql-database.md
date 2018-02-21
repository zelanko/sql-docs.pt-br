---
title: CREATE DATABASE (Banco de Dados SQL do Azure) | Microsoft Docs
ms.custom: 
ms.date: 02/13/2018
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: t-sql|statements
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c61660015eb2f613148ad58b72386e42eb797db9
ms.sourcegitcommit: aebbfe029badadfd18c46d5cd6456ea861a4e86d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2018
---
# <a name="create-database-azure-sql-database"></a>CREATE DATABASE (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

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
    | ( EDITION = {  'basic' | 'standard' | 'premium' }   
    | SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' | 
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'  
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
            | { ELASTIC_POOL(name = <elastic_pool_name>) } } )  
    ]  
 [;] 
 
```  
  
## <a name="arguments"></a>Argumentos  
 Este diagrama de sintaxe demonstra os argumentos com suporte no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 *database_name*  
 O nome do novo banco de dados. Esse nome deve ser exclusivo no servidor SQL, que pode hospedar os bancos de dados [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], e ser compatível com as regras [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para identificadores. Para obter mais informações, consulte [Identificadores](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
 *Collation_name*  
 Especifica o agrupamento padrão do banco de dados. O nome do agrupamento pode ser um nome de agrupamento do Windows ou um nome de agrupamento SQL. Se não for especificado, o banco de dados será atribuído o agrupamento padrão, que é SQL_Latin1_General_CP1_CI_AS.  
  
 Para obter mais informações sobre os nomes de agrupamento do Windows e do SQL, [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx).  
  
 *CATALOG_COLLATION*  
Especifica o agrupamento padrão do catálogo de metadados. *DATABASE_DEFAULT* especifica que o catálogo de metadados usado para exibições do sistema e tabelas do sistema seja agrupado para corresponder ao agrupamento padrão do banco de dados.  Esse é o comportamento encontrado no SQL Server. 

*SQL_Latin1_General_CP1_CI_AS* especifica que o catálogo de metadados usado para exibições do sistema e tabelas seja agrupado em um agrupamento SQL_Latin1_General_CP1_CI_AS fixo.  Essa será a configuração padrão no Banco de Dados SQL do Azure, se não for especificado.

 *EDITION*  
 Especifica a camada de serviço do banco de dados. Os valores disponíveis são: 'basic', 'standard' e 'premium'. O suporte para 'premiumrs' foi removido. Em caso de dúvidas, use este alias de email: premium-rs@microsoft.com.
  
 Quando EDITION for especificado, mas MAXSIZE não for especificado, MAXSIZE será definido como o tamanho mais restritivo com suporte na edição.  
  
 *MAXSIZE*  
 Especifica o tamanho máximo do banco de dados. MAXSIZE deve ser válido para a EDIÇÃO especificada (camada de serviço) A seguir, estão os valores com suporte para MAXSIZE e os padrões (D) para as camadas de serviço.  
  
|**MAXSIZE**|**Basic**|**S0-S2**|**S3-S12**|**P1-P6**| **P11-P15** 
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
|De 1024 GB até 4096 GB em incrementos de 256 GB* |N/A|N/A|N/A|N/A|√|√|  
  
 \* P11 e P15 permitem MAXSIZE até 4 TB com 1024 GB sendo o tamanho padrão.  P11 e P15 podem usar até 4 TB de armazenamento incluído sem custos adicionais. Na camada Premium, MAXSIZE maior do que 1 TB está disponível no momento nas seguintes regiões: Leste dos EUA2, Oeste dos EUA, Gov. EUA – Virgínia, Europa Ocidental, Alemanha Central, Sudeste Asiático, Leste do Japão, Leste da Austrália, Canadá Central e Leste do Canadá. Para ver as limitações atuais, consulte [Single databases](https://docs.microsoft.com/azure/sql-database-single-database-resources) (Bancos de dados únicos).  
  
 As regras a seguir se aplicam aos argumentos MAXSIZE e EDITION:  
  
-   O valor MAXSIZE, se especificado, precisa ser um valor válido exibido na tabela acima.  
  
-   Se EDITION for especificado, mas MAXSIZE não for especificado, o valor padrão da edição será usado. Por exemplo, se EDITION for definido como Standard e MAXSIZE não for especificado, então MAXSIZE será automaticamente definido como 250 MB.  
  
-   Se nem MAXSIZE nem EDITION forem especificados, EDITION será definido como Standard (S0) e MAXZISE será definido como 250 GB.  
  
 SERVICE_OBJECTIVE  
 Especifica o nível de desempenho. Para obter descrições objetivas do serviço e mais informações sobre o tamanho, edições e as combinações objetivas de serviço, consulte [Azure SQL Database Service Tiers and Performance Levels](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) (Camada de Serviço do Banco de Dados SQL do Azure e Níveis de Desempenho) e [SQL Database resource limits](https://azure.microsoft.com/documentation/articles/sql-database-resource-limits) (Limites de recurso do Banco de Dados SQL). Se o SERVICE_OBJECTIVE especificado não tiver suporte pela EDITION, você receberá um erro.  
  
 ELASTIC_POOL (name = \<elastic_pool_name>) Para criar um novo banco de dados em um pool de banco de dados elástico, defina o SERVICE_OBJECTIVE do banco de dados como ELASTIC_POOL e forneça o nome do pool. Para obter mais informações, consulte [Create and manage a SQL Database elastic database pool (preview)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/) (Criar e gerenciar um pool de banco de dados elástico do Banco de Dados SQL (versão prévia)).  
  
 *AS COPY OF [source_server_name.]source_database_name*  
 Para copiar um banco de dados para o mesmo servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ou um servidor diferente.  
  
 *source_server_name*  
 O nome do servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] onde o banco de dados de origem está localizado. Esse parâmetro é opcional quando o banco de dados de origem e o banco de dados de destino devem estar localizados no mesmo servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Observação: o argumento `AS COPY OF` não oferece suporte aos nomes de domínio exclusivos totalmente qualificados. Em outras palavras, se o nome de domínio totalmente qualificado do seu servidor for `serverName.database.windows.net`, use somente `serverName` durante a cópia do banco de dados.  
  
 *source_database_name*  
 O nome do banco de dados que deve ser copiado.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] não dá suporte aos seguintes argumentos e opções ao usar a instrução `CREATE DATABASE`:  
  
-   Parâmetros relacionados ao posicionamento físico do arquivo, como \<filespec> e \<filegroup>  
  
-   Opções de acesso externo, como DB_CHAINING e TRUSTWORTHY  
  
-   Anexando um banco de dados  
  
-   Opções do service broker, como ENABLE_BROKER, NEW_BROKER e ERROR_BROKER_CONVERSATIONS  
  
-   Instantâneo do banco de dados  
  
 Para obter mais informações sobre os argumentos e sobre a instrução `CREATE DATABASE`, consulte [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 Os bancos de dados no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] tem várias configurações padrão que são definidas quando o banco de dados é criado. Para obter mais informações sobre essas configurações padrão, consulte a lista de valores em [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md).  
  
 MAXSIZE fornece a capacidade de limitar o tamanho do banco de dados. Se o tamanho do banco de dados atingir seu MAXSIZE, você receberá o código de erro 40544. Quando isso ocorre, você não pode inserir ou atualizar dados nem criar novos objetos (como tabelas, procedimentos armazenados, exibições e funções). No entanto, você ainda pode ler e excluir dados, truncar tabelas, descartar tabelas e índices e reconstruir índices. Você pode atualizar MAXSIZE para um valor maior que o tamanho atual do banco de dados ou excluir alguns dados para liberar espaço de armazenamento. Pode haver um atraso máximo de quinze minutos para que você possa inserir novos dados.  
  
> [!IMPORTANT]  
>  A instrução `CREATE DATABASE` deve ser a única instrução em um lote do [!INCLUDE[tsql](../../includes/tsql-md.md)]. 
  
 Para alterar o tamanho, edição ou valores objetivos de serviço posteriormente, use [ALTER DATABASE &#40;Banco de Dados SQL do Azure&#41;](../../t-sql/statements/alter-database-azure-sql-database.md).  

O argumento CATALOG_COLLATION só está disponível durante a criação do banco de dados. 
  
## <a name="database-copies"></a>Cópias de banco de dados  
 Copiar um banco de dados que usa a instrução `CREATE DATABASE` é uma operação assíncrona. Portanto, uma conexão com o servidor de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] não é necessária para a duração completa do processo de cópia. A instrução `CREATE DATABASE` retornará o controle para o usuário depois que a entrada no sys.databases for criada, mas antes que a operação de cópia de banco de dados seja concluída. Em outras palavras, a instrução `CREATE DATABASE` é retornada com êxito quando a cópia do banco de dados ainda está em andamento.  
  
-   Monitorando o processo de cópia em um servidor [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]: consulte as colunas `percentage_complete` ou `replication_state_desc` no [dm_database_copies](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md) ou a coluna `state` na exibição **sys.databases**. A exibição [sys.dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) pode ser usada e retornará o status das operações de banco de dados, incluindo a cópia do banco de dados.  
  
 Quando o processo de cópia é concluído com êxito, o banco de dados de destino fica transacionalmente consistente com o banco de dados de origem.  
  
 A seguinte sintaxe e as regras semânticas aplicam-se ao uso do argumento `AS COPY OF`:  
  
-   Os nomes do servidor de origem e do servidor para o destino de impressão podem ser iguais ou diferentes. Quando são o mesmo, esse parâmetro é opcional e o contexto do servidor da sessão atual é usado por padrão.  
  
-   Os nomes do banco de dados de origem e destino devem ser especificados, exclusivo e estarem em conformidade com as regras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para identificadores. Para obter mais informações, consulte [Identificadores](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
-   A instrução `CREATE DATABASE` deve ser executada dentro do contexto do banco de dados mestre do servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] em que o novo banco de dados será criado.  
  
-   Depois de a cópia ser concluída, o banco de dados de destino deve ser gerenciado como um banco de dados independente. Você pode executar as instruções `ALTER DATABASE` e `DROP DATABASE` no novo banco de dados independentemente do banco de dados de origem. Você também pode copiar o novo banco de dados para outro novo banco de dados.  
  
-   O banco de dados de origem pode continuar a ser acessado enquanto a cópia do banco de dados está em andamento.  
  
 Para obter mais informações, consulte [Criar uma cópia de um Banco de Dados SQL do Azure usando o Transact-SQL](https://azure.microsoft.com/documentation/articles/sql-database-copy-transact-sql/).  
  
## <a name="permissions"></a>Permissões  
 Para criar um banco de dados, um logon deve ser um dos seguintes:  
  
-   O logon da entidade de segurança no nível do servidor  
  
-   O administrador do Azure AD do SQL Server do Azure local  
  
-   Um logon que é um membro da função de banco de dados `dbmanager`  
  
 **Requisitos adicionais para usar a sintaxe `CREATE DATABASE ... AS COPY OF`:** o logon que executa a instrução no servidor local também deve ter pelo menos o `db_owner` no servidor de origem. Se o logon for baseado na autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o logon que está executando a instrução no servidor local deverá ter um logon correspondente no servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] de origem, com um nome idêntico e senha idênticos.  
  
## <a name="examples"></a>Exemplos  
Para obter um tutorial de início rápido que mostra como conectar-se a um banco de dados SQL do Azure usando o SQL Server Management Studio, consulte [Azure SQL Database: Use SQL Server Management Studio to connect and query data](/azure/sql-database/sql-database-connect-query-ssms) (Banco de Dados SQL do Azure: use o SQL Server Management Studio para conectar e consultar dados).  
  
### <a name="simple-example"></a>Exemplo simples  
 Um exemplo simples para criar um banco de dados.  
  
```sql  
CREATE DATABASE TestDB1;  
```  
  
### <a name="simple-example-with-edition"></a>Exemplo simples com Edição  
 Um exemplo simples para criar um banco de dados padrão.  
  
```sql  
CREATE DATABASE TestDB2  
( EDITION = 'standard' );  
```  
  
### <a name="example-with-additional-options"></a>Exemplo com opções adicionais  
 Um exemplo que usa várias opções.  
  
```sql  
CREATE DATABASE hito   
COLLATE Japanese_Bushu_Kakusu_100_CS_AS_KS_WS   
( MAXSIZE = 500 MB, EDITION = 'standard', SERVICE_OBJECTIVE = 'S1' ) ;  
```  
  
### <a name="creating-a-copy"></a>Criando uma cópia  
 Um exemplo da criação de uma cópia de um banco de dados.  
  
```sql  
CREATE DATABASE escuela   
AS COPY OF school;  
```  
  
### <a name="creating-a-database-in-an-elastic-pool"></a>Criando um banco de dados em um pool elástico  
 Cria um novo banco de dados no pool chamado S3M100:  
  
```sql  
CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = S3M100 ) ) ;  
```  
  
### <a name="creating-a-copy-of-a-database-on-another-server"></a>Criando uma cópia de um banco de dados em outro servidor  
 O exemplo a seguir cria uma cópia do banco de dados db_original, chamada db_copy no nível de desempenho P2 para um único banco de dados.  Isso será verdadeiro independentemente se db_original for um pool elástico ou um nível de desempenho para um único banco de dados.  
  
```sql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original ( SERVICE_OBJECTIVE = 'P2' )  ;  
```  
  
 O exemplo a seguir cria uma cópia do banco de dados db_original, chamada db_copy em um pool elástico chamado ep1.  Isso será verdadeiro independentemente se db_original for um pool elástico ou um nível de desempenho para um único banco de dados.  Se db_original estiver em um pool elástico com um nome diferente, então db_copy ainda será criado em ep1.  
  
```sql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original   
    (SERVICE_OBJECTIVE = ELASTIC_POOL( name = ep1 ) ) ;  
```  

### <a name="create-database-with-specified-catalog-collation-value"></a>Criar banco de dados com um valor de agrupamento de catálogo especificado

O exemplo a seguir define o agrupamento de catálogo como DATABASE_DEFAULT durante a criação do banco de dados, que define o agrupamento de catálogo como sendo o mesmo que o agrupamento de banco de dados.

```sql
CREATE DATABASE TestDB3 COLLATE Japanese_XJIS_140  (MAXSIZE = 100 MB, EDITION = ‘basic’)  
      WITH CATALOG_COLLATION = DATABASE_DEFAULT 
```
  
## <a name="see-also"></a>Consulte também  

-  [sys.dm_database_copies &#40;Banco de Dados SQL do Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)

-   [ALTER DATABASE &#40;Banco de Dados SQL do Azure&#41;](alter-database-azure-sql-database.md)   
    
  

