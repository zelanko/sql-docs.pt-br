---
title: sp_fulltext_catalog (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_catalog_TSQL
- sp_fulltext_catalog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_catalog
ms.assetid: e49b98e4-d1f1-42b2-b16f-eb2fc7aa1cf5
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4b51e4e38b7587074a39f850c2e56dbd8c09ed6f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72005966"
---
# <a name="sp_fulltext_catalog-transact-sql"></a>sp_fulltext_catalog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cria e remove um catálogo de texto completo, e inicia e interrompe a ação de indexação de um catálogo. Catálogos de texto completo podem ser criados para cada banco de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use [criar catálogo de texto completo](../../t-sql/statements/create-fulltext-catalog-transact-sql.md), [alterar catálogo de texto](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)completo e [remover catálogo de texto completo](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_fulltext_catalog [ @ftcat= ] 'fulltext_catalog_name' ,   
     [ @action= ] 'action'   
     [ , [ @path= ] 'root_directory' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @ftcat = ] 'fulltext_catalog_name'`É o nome do catálogo de texto completo. Nomes de catálogo devem ser exclusivos para cada banco de dados. *fulltext_catalog_name* é **sysname**.  
  
`[ @action = ] 'action'`É a ação a ser executada. a *ação* é **varchar (20)** e pode ser um desses valores.  
  
> [!NOTE]  
>  Os catálogos de texto completo podem ser criados, descartados e modificados conforme necessário. Entretanto, evite fazer alterações de esquema em vários catálogos ao mesmo tempo. Essas ações podem ser executadas usando o procedimento armazenado **sp_fulltext_table** , que é a maneira recomendada.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Criar**|Cria um novo catálogo de texto completo vazio no sistema de arquivos e adiciona uma linha associada em **sysfulltextcatalogs** com o *fulltext_catalog_name* e *root_directory*, se estiverem presentes, valores. *fulltext_catalog_name* deve ser exclusivo no banco de dados.|  
|**Suspensa**|Descarta *fulltext_catalog_name* removendo-o do sistema de arquivos e excluindo a linha associada em **sysfulltextcatalogs**. Haverá falha nessa ação se esse catálogo contiver índices para uma ou mais tabelas. **sp_fulltext_table** '*table_name*', ' drop ' deve ser executado para descartar as tabelas do catálogo.<br /><br /> Um erro será exibido se o catálogo não existir.|  
|**start_incremental**|Inicia uma população incremental para *fulltext_catalog_name*. Um erro será exibido se o catálogo não existir. Se uma população de índice de texto completo já estiver ativa, um aviso será exibido, mas nenhuma ação de população ocorrerá. Com a população incremental, somente as linhas alteradas são recuperadas para indexação de texto completo, desde que haja uma coluna de **carimbo de data/hora** presente na tabela sendo indexada com texto completo.|  
|**start_full**|Inicia uma população completa para *fulltext_catalog_name*. Todas as linhas de todas as tabelas associadas a esse catálogo de texto completo são recuperadas para a indexação de texto completo, mesmo que já tenham sido indexadas.|  
|**Parar**|Interrompe uma população de índice para *fulltext_catalog_name*. Um erro será exibido se o catálogo não existir. Nenhum aviso será exibido se a população já estiver parada.|  
|**Constitui**|Recria *fulltext_catalog_name*. Quando um catálogo é recriado, o catálogo existente é excluído e um novo catálogo é criado em seu lugar. Todas as tabelas que têm referências de indexação de texto completo são associadas ao novo catálogo. A recriação redefine os metadados de texto completo nas tabelas do sistema de banco de dados.<br /><br /> Se o controle de alterações estiver definido como OFF, a recriação não fará com que ocorra um novo preenchimento do catálogo de texto completo recém-criado. Nesse caso, para repopular, execute **sp_fulltext_catalog** com a ação **start_full** ou **start_incremental** .|  
  
`[ @path = ] 'root_directory'`É o diretório raiz (não o caminho físico completo) para uma ação de **criação** . *root_directory* é **nvarchar (100)** e tem um valor padrão de NULL, que indica o uso do local padrão especificado na instalação. Esse é o subdiretório FTDATA no diretório MSSQL; por exemplo, C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\MSSQL\FTData. O diretório raiz especificado deve residir em uma unidade no mesmo computador, deve consistir em mais informações além da letra da unidade e não pode ser um caminho relativo. Unidades de rede, unidades removíveis, discos flexíveis e caminhos UNC não têm suporte. Os catálogos de texto completo devem ser criados em um disco rígido local associado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 o caminho é válido somente quando a *ação* é **criada**. ** \@** Para ações diferentes de **criar** (**parar**, **Recompilar**e assim por diante) ** \@** , o caminho deve ser nulo ou omitido.  
  
 Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for um servidor virtual em um cluster, o diretório de catálogo especificado precisará estar em uma unidade de disco compartilhada da qual o recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja dependente. Se @path não for especificado, o local do diretório de catálogo padrão estará na unidade de disco compartilhada, no diretório que foi especificado quando o servidor virtual foi instalado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 A ação **start_full** é usada para criar um instantâneo completo dos dados de texto completo no *fulltext_catalog_name*. A ação **start_incremental** é usada para reindexar apenas as linhas alteradas no banco de dados. A população incremental só poderá ser aplicada se a tabela tiver uma coluna do tipo **timestamp**. Se uma tabela no catálogo de texto completo não contiver uma coluna do tipo **timestamp**, a tabela passará por uma população completa.  
  
 Os dados do catálogo de texto completo e do índice são armazenados em arquivos criados em um diretório de catálogo de texto completo. O diretório de catálogo de texto completo é criado como um subdiretório do diretório especificado em ** \@Path** ou no diretório de catálogo de texto completo padrão do servidor se ** \@o caminho** não for especificado. O nome do diretório de catálogo de texto completo é criado de uma forma que garante que ele será exclusivo no servidor. Portanto, todos os diretórios de catálogo de texto completo em um servidor podem compartilhar o mesmo caminho.  
  
## <a name="permissions"></a>Permissões  
 O chamador deve ser membro da função de **db_owner** . Dependendo da ação solicitada, o chamador não deve ser negado às permissões ALTER ou CONTROL (que **db_owner** tem) no catálogo de texto completo de destino.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-create-a-full-text-catalog"></a>a. Criar um catálogo de texto completo  
 Este exemplo cria um catálogo de texto completo vazio, **Cat_Desc**, no banco de dados **AdventureWorks2012** .  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'create';  
GO  
```  
  
### <a name="b-to-rebuild-a-full-text-catalog"></a>B. Para recriar um catálogo de texto completo  
 Este exemplo recria um catálogo de texto completo existente, **Cat_Desc**, no banco de dados **AdventureWorks2012** .  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'rebuild';  
GO  
```  
  
### <a name="c-start-the-population-of-a-full-text-catalog"></a>C. Iniciar a população de um catálogo de texto completo  
 Este exemplo inicia uma população completa do catálogo de **Cat_Desc** .  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'start_full';  
GO  
```  
  
### <a name="d-stop-the-population-of-a-full-text-catalog"></a>D. Interromper a população de um catálogo de texto completo  
 Este exemplo interrompe a população do catálogo de **Cat_Desc** .  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'stop';  
GO  
```  
  
### <a name="e-to-remove-a-full-text-catalog"></a>E. Para remover um catálogo de texto completo  
 Este exemplo remove o catálogo **Cat_Desc** .  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'drop';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;FULLTEXTCATALOGPROPERTY &#40;Transact-SQL](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_fulltext_database](../../relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_fulltext_catalogs](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_fulltext_catalogs_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Pesquisa de texto completo](../../relational-databases/search/full-text-search.md)  
  
  
