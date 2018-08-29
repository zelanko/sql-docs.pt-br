---
title: Configuração de visibilidade de metadados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subcomponents visibility [SQL Server]
- metadata [SQL Server], visibility
- permissions [SQL Server], metadata access
- viewing metadata
- objects [SQL Server], metadata
- displaying metadata
- database metadata [SQL Server]
- metadata [SQL Server], permissions
ms.assetid: 50d2e015-05ae-4014-a1cd-4de7866ad651
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 1cd39b93b761bd6466f3c0627df40aa9b67bbb2b
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43024115"
---
# <a name="metadata-visibility-configuration"></a>Configuração de visibilidade de metadados
  A visibilidade de metadados é limitada aos protegíveis que pertencem a um usuário ou sobre os quais recebeu alguma permissão. Por exemplo, a consulta a seguir retornará uma linha se o usuário recebeu uma permissão SELECT ou INSERT na tabela `myTable`.  
  
```  
SELECT name, object_id  
FROM sys.tables  
WHERE name = 'myTable';  
GO  
```  
  
 Entretanto, se o usuário não possuir nenhuma permissão em `myTable`, a consulta retornará um conjunto de resultados vazio.  
  
## <a name="scope-and-impact-of-metadata-visibility-configuration"></a>Escopo e impacto da configuração de visibilidade de metadados  
 A configuração de visibilidade de metadados apenas se aplica aos seguintes protegíveis.  
  
|||  
|-|-|  
|Exibições do catálogo|[!INCLUDE[ssDE](../../includes/ssde-md.md)] **sp_help** stored procedures|  
|Metadados com exposição de funções internas|Exibições do esquema de informações|  
|Exibições de compatibilidade|Propriedades estendidas|  
  
 A configuração de visibilidade de metadados não se aplica aos seguintes protegíveis.  
  
|||  
|-|-|  
|Tabelas do sistema de envio de logs|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelas do sistema do Agent|  
|Tabelas do sistema de plano de manutenção do banco de dados|Tabelas do sistema de backup|  
|Tabelas do sistema de replicação|Replicação e procedimento armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent **sp_help**|  
  
 Acessibilidade de metadados limitada significa o seguinte:  
  
-   Aplicativos que assumem que o acesso de metadados **público** será interrompido.  
  
-   Consultas nas exibições de sistema podem retornar apenas um subconjunto de linhas, ou às vezes um conjunto de resultados vazio.  
  
-   Funções internas, que emitem metadados como em OBJECTPROPERTYEX podem retornar NULO.  
  
-   Os procedimentos armazenados de [!INCLUDE[ssDE](../../includes/ssde-md.md)] **sp_help** podem retornar apenas um subconjunto de linhas ou NULL.  
  
 Os módulos SQL, como os procedimentos armazenados e os gatilhos, são executados no contexto de segurança do chamador e, em consequência, têm acessibilidade limitada aos metadados. Por exemplo, no código a seguir, quando o procedimento armazenado tentar acessar os metadados para a tabela `myTable` na qual o visitante não tem nenhum direito, há retorno de um conjunto de resultados vazio. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é retornada uma linha.  
  
```  
CREATE PROCEDURE assumes_caller_can_access_metadata  
BEGIN  
SELECT name, id   
FROM sysobjects   
WHERE name = 'myTable';  
END;  
GO  
```  
  
 Você pode conceder aos visitantes uma permissão VIEW DEFINITION, que permita aos visitantes exibir os metadados no escopo apropriado: nível de objeto, nível de banco de dados ou nível de servidor. Assim, no exemplo prévio, se o visitante tiver uma permissão VIEW DEFINITION em `myTable`, o procedimento armazenado retornará uma linha. Para obter mais informações, veja [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql) e [Permissões de banco de dados GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-permissions-transact-sql).  
  
 Você também pode modificar o procedimento armazenado de forma a executar com as credenciais do proprietário. Quando o proprietário do procedimento e o da tabela forem o mesmo proprietário, o encadeamento de propriedade é aplicável e o contexto de segurança do proprietário do procedimento ativa o acesso aos metadados para `myTable`. Nesse cenário, o seguinte código retorna uma linha de metadados ao chamador.  
  
> [!NOTE]  
>  O exemplo a seguir utiliza a exibição do catálogo [sys.objects](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql) , em vez da exibição de compatibilidade [sys.sysobjects](/sql/relational-databases/system-compatibility-views/sys-sysobjects-transact-sql) .  
  
```  
CREATE PROCEDURE does_not_assume_caller_can_access_metadata  
WITH EXECUTE AS OWNER  
AS  
BEGIN  
SELECT name, id  
FROM sys.objects   
WHERE name = 'myTable'   
END;  
GO  
```  
  
> [!NOTE]  
>  Você pode usar EXECUTE AS para alternar temporariamente para o contexto de segurança do chamador. Para obter mais informações, veja [EXECUTE AS &#40;Transact-SQL&#41;](/sql/t-sql/statements/execute-as-transact-sql).  
  
## <a name="benefits-and-limits-of-metadata-visibility-configuration"></a>Benefícios e limites da configuração de visibilidade de metadados  
 A configuração de visibilidade de metadados pode ter uma função importante em seu plano de segurança global. Entretanto, há casos nos quais um usuário habilidoso e determinado pode forçar a divulgação de alguns metadados. Recomendamos que você implante permissões para metadados como um dos muitos detalhes de defesa.  
  
 É teoricamente possível forçar a emissão de metadados em mensagens de erro manipulando a ordem de avaliação do predicado nas consultas. A possibilidade de tais *ataques por tentativa e erro* não é específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Está implícita nas transformações associativas e comutativas permitidas pela álgebra relacional. Você pode reduzir esse risco limitando as informações retornadas nas mensagens de erro. Para restringir ainda mais a visibilidade de metadados desse modo, você pode iniciar o servidor com o sinalizador de rastreamento 3625. Este sinalizador de rastreamento limita a quantidade de informações mostradas nas mensagens de erro. Por sua vez, isso ajuda a impedir divulgações forçadas. Em compensação as mensagens de erro serão concisas e será difícil usar para propósitos de depuração. Para obter mais informações, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md) e [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).  
  
 Os metadados a seguir não estão sujeitos a divulgação forçada:  
  
-   O valor armazenado na coluna **provider_string** de **sys.servers**. Um usuário que não tem permissão ALTER ANY LINKED SERVER verá um valor NULL nessa coluna.  
  
-   Definição de fonte de um objeto definido pelo usuário como um procedimento armazenado ou gatilho. O código de origem só é visível quando um destes for verdadeiro:  
  
    -   O usuário tem permissão VIEW DEFINITION no objeto.  
  
    -   Não foi negada permissão ao usuário em VIEW DEFINITION no objeto e possui permissões em CONTROL, ALTER ou em TAKE OWNERSHIP no objeto. Todos os outros usuários verão NULL.  
  
-   As colunas de definição encontradas nas exibições do catálogo a seguir:  
  
    |||  
    |-|-|  
    |**sys.all_sql_modules**|**sys.sql_modules**|  
    |**sys.server_sql_modules**|**sys.check_constraints**|  
    |**sys.default_constraints**|**sys.computed_columns**|  
    |**sys.numbered_procedures**||  
  
-   A coluna **ctext** na exibição de compatibilidade **syscomments** .  
  
-   A saída do procedimento **sp_helptext** .  
  
-   As seguintes colunas nas exibições do esquema de informações:  
  
    |||  
    |-|-|  
    |INFORMATION_SCHEMA.CHECK_CONSTRAINTS.CHECK_CLAUSE|INFORMATION_SCHEMA.COLUMNS.COLUMN_DEFAULT|  
    |INFORMATION_SCHEMA.DOMAINS.DOMAIN_DEFAULT|INFORMATION_SCHEMA.ROUTINE_COLUMNS.COLUMN_DEFAULT|  
    |INFORMATION_SCHEMA.ROUTINES.ROUTINE_DEFINITION|INFORMATION_SCHEMA.VIEWS.VIEW_DEFINITION|  
  
-   Função OBJECT_DEFINITION()  
  
-   O valor armazenado na coluna password_hash em **sys.sql_logins**.  Um usuário que não tenha a permissão CONTROL SERVER verá um valor NULL nessa coluna.  
  
> [!NOTE]  
>  As definições de SQL de procedimentos e funções de sistema internos são publicamente visíveis na exibição do catálogo **sys.system_sql_modules** , no procedimento armazenado **sp_helptext** e na função OBJECT_DEFINITION().  
  
## <a name="general-principles-of-metadata-visibility"></a>Princípios gerais de visibilidade de metadados  
 A seguir, alguns princípios gerais para serem considerados relativos à visibilidade de metadados:  
  
-   Permissões implícitas de funções fixas  
  
-   Escopo das permissões  
  
-   Precedência em DENY  
  
-   Visibilidade de metadados de subcomponente  
  
### <a name="fixed-roles-and-implicit-permissions"></a>Funções fixas e permissões implícitas  
 Os metadados que podem ser acessados através de funções fixas dependem de suas permissões implícitas correspondentes.  
  
### <a name="scope-of-permissions"></a>Escopo das permissões  
 Permissões em um escopo implicam na capacidade de ver os metadados nesse escopo e em todos os escopos inclusos. Por exemplo, a permissão SELECT dentro de um esquema implica que o beneficiado tem permissão SELECT em todos os protegíveis contidos nesse esquema. A concessão de permissão SELECT em um esquema permite que usuário veja então os metadados do esquema e também todas as tabelas, exibições, funções, procedimentos, filas, sinônimos, tipos e coleções de esquema XML inclusos. Para obter mais informações sobre escopos, veja [Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](permissions-hierarchy-database-engine.md).  
  
### <a name="precedence-of-deny"></a>Precedência em DENY  
 DENY normalmente tem precedência sobre outras permissões. Por exemplo, se um usuário de banco de dados recebeu permissão EXECUTE em um esquema, mas teve a permissão EXECUTE negada em um procedimento armazenado nesse esquema, o usuário não pode exibir os metadados para esse procedimento armazenado.  
  
 Além disso, se um usuário teve a permissão EXECUTE negada em um esquema, mas recebeu a permissão EXECUTE em um procedimento armazenado nesse esquema, o usuário não pode exibir os metadados para esse procedimento armazenado.  
  
 Outro exemplo, se um usuário teve permissão EXECUTE concedida e negada em um procedimento armazenado, o que é possível através de suas diversas associações à funções, DENY terá precedência e o usuário não poderá exibir os metadados do procedimento armazenado.  
  
### <a name="visibility-of-subcomponent-metadata"></a>Visibilidade de metadados de subcomponente  
 A visibilidade de subcomponentes, como índices, restrições de verificação e gatilhos são determinados através de permissões no pai. Esses subcomponentes não têm permissões que possam ser concedidas. Por exemplo, se um usuário recebeu alguma permissão em uma tabela, o usuário poderá exibir os metadados para as tabelas, colunas, índices, restrições de verificações, gatilhos e outros subcomponentes similares.  
  
#### <a name="metadata-that-is-accessible-to-all-database-users"></a>Metadados acessíveis a todos os usuários do banco de dados  
 Algum metadados devem ser acessíveis a todos os usuários em um banco de dados específico. Por exemplo, grupos de arquivos não têm permissões que possam ser conferidas; consequentemente, um usuário não pode receber permissão para exibir os metadados de um grupo de arquivos. Entretanto, qualquer usuário que possa criar uma tabela deve poder acessar os metadados de grupo de arquivos para usar *filegroup* ON ou as cláusulas TEXTIMAGE_ON *filegroup* da instrução CREATE TABLE.  
  
 Os metadados retornados pelas funções DB_ID() e DB_NAME() são visíveis para todos os usuários.  
  
 A tabela a seguir lista aos exibições do catálogo que são visíveis na função **pública** .  
  
|||  
|-|-|  
|**sys.partition_functions**|**sys.partition_range_values**|  
|**sys.partition_schemes**|**sys.data_spaces**|  
|**sys.filegroups**|**sys.destination_data_spaces**|  
|**sys.database_files**|**sys.allocation_units**|  
|**sys.partitions**|**sys.messages**|  
|**sys.schemas**|**sys.configurations**|  
|**sys.sql_dependencies**|**sys.type_assembly_usages**|  
|**sys.parameter_type_usages**|**sys.column_type_usages**|  
  
## <a name="see-also"></a>Consulte também  
 [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)   
 [DENY &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-transact-sql)   
 [REVOKE &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql)   
 [Cláusula EXECUTE AS &#40;Transact-SQL&#41;](/sql/t-sql/statements/execute-as-clause-transact-sql)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql)  
  
  
