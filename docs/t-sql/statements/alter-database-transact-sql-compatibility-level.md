---
title: Nível de compatibilidade de ALTER DATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COMPATIBILITY_LEVEL_TSQL
- COMPATIBILITY_LEVEL
dev_langs:
- TSQL
helpviewer_keywords:
- 80 compatibility level
- ALTER DATABASE statement, compatibility levels
- 90 compatibility level
- compatibility levels [SQL Server]
- 100 compatibility level
- db compatibility level
- db compat level
ms.assetid: ca5fd220-d5ea-4182-8950-55d4101a86f6
author: CarlRabeler
ms.author: carlrab
manager: craigg'
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 55d919cefd20ef4b139dbf30a053bbda568f6e38
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2019
ms.locfileid: "54242157"
---
# <a name="alter-database-transact-sql-compatibility-level"></a>Nível de compatibilidade de ALTER DATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Define certos comportamentos de banco de dados como sendo compatíveis com a versão especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter outras opções de ALTER DATABASE, consulte [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  

Para obter mais informações sobre as convenções de sintaxe, consulte [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER DATABASE database_name   
SET COMPATIBILITY_LEVEL = { 150 | 140 | 130 | 120 | 110 | 100 | 90 }  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 É o nome do banco de dados a ser modificado.  
  
 COMPATIBILITY_LEVEL { 150 | 140 | 130 | 120 | 110 | 100 | 90 | 80 }  
 É a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a qual o banco de dados será compatível. Os seguintes valores de nível de compatibilidade podem ser configurados (nem todas as versões dão suporte a todos os níveis de compatibilidade listados acima):  
  
|Product|Versão do Mecanismo de Banco de Dados|Designação de nível de compatibilidade|Valores do nível de compatibilidade com suporte|  
|-------------|-----------------------------|-------------------------------------|------------------------------------------|  
|[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]|15|150|150, 140, 130, 120, 110, 100| 
|[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|14|140|140, 130, 120, 110, 100|
|Servidor lógico [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|12|130|150, 140, 130, 120, 110, 100|  
|[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] Instância gerenciada|12|130|150, 140, 130, 120, 110, 100|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|13|130|130, 120, 110, 100|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|12|120|120, 110, 100|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|11|110|110, 100, 90|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|10.5|100|100, 90, 80|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|10|100|100, 90, 80|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|9|90|90, 80|  
|SQL Server 2000|8|80|80|  
  
> [!NOTE]  
> A partir de **janeiro de 2018**, no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], o nível de compatibilidade padrão é 140 para bancos de dados recém-criados. Não atualizamos o nível de compatibilidade dos bancos de dados existentes. É responsabilidade dos clientes fazer isso a seu critério. Dito isso, é altamente recomendável que os clientes planejem a migração para o último nível de compatibilidade, para aproveitar as últimas melhorias.
> 
> Se você quiser aproveitar o nível de compatibilidade do banco de dados 140 para seu banco de dados geral, mas tiver motivo para preferir o modelo de **estimativa de cardinalidade** de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], mapeando para o nível de compatibilidade do banco de dados 110, veja [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) e, em especial, sua palavra-chave `LEGACY_CARDINALITY_ESTIMATION = ON`.
>  
> Para obter detalhes sobre como avaliar as diferenças de desempenho das consultas mais importantes, entre dois níveis de compatibilidade no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], consulte [Melhor desempenho de consultas com o nível de compatibilidade 130 no Banco de Dados SQL do Azure](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/). Observe que este artigo se refere ao nível de compatibilidade 130 e ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas a mesma metodologia se aplica à migração para o nível 140 do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Execute a consulta a seguir para determinar a versão do [!INCLUDE[ssDE](../../includes/ssde-md.md)] à qual você está conectado.  
  
```sql  
SELECT SERVERPROPERTY('ProductVersion');  
```  
  
> [!NOTE]  
> Nem todos os recursos que variam de acordo com o nível de compatibilidade são compatíveis com o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  

 Para determinar o nível de compatibilidade atual, consulte a coluna **compatibility_level** de [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
```sql  
SELECT name, compatibility_level FROM sys.databases;  
```  
  
## <a name="remarks"></a>Remarks  
Para todas as instalações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o nível de compatibilidade padrão é definido com a versão do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Bancos de dados são definidos com esse nível, a não ser que o **modelo** de banco de dados tenha um nível de compatibilidade inferior. Quando um banco de dados é atualizado para qualquer versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o banco de dados retém seu nível de compatibilidade existente se ele tem permissão, no mínimo, nessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A atualização de um banco de dados com um nível de compatibilidade mais baixo do que o nível permitido define automaticamente o banco de dados para o nível de compatibilidade mais baixo permitido. Isso se aplica aos bancos de dados do sistema e de usuário.   

Os comportamentos a seguir são esperadas para [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] quando um banco de dados for anexado ou restaurado e após uma atualização in-loco: 
- Se o nível de compatibilidade de um banco de dados de usuário era 100 ou mais alto antes da atualização, ele permanecerá o mesmo depois da atualização.    
- Se o nível de compatibilidade de um banco de dados do usuário era 90 antes da atualização, no banco de dados atualizado esse nível será definido como 100, que é o mais baixo com suporte no [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)].    
- Os níveis de compatibilidade dos bancos de dados tempdb, model, msdb e Resource são definidos para o nível de compatibilidade atual após o upgrade.  
- O banco de dados do sistema mestre retém o nível de compatibilidade anterior ao upgrade.

Use `ALTER DATABASE` para alterar o nível de compatibilidade do banco de dados. A nova configuração do nível de compatibilidade de um banco de dados tem efeito quando um comando `USE <database>` é emitido ou um novo logon é processado com esse banco de dados como o contexto do banco de dados padrão.     
Para exibir o nível de compatibilidade atual de um banco de dados, consulte a coluna **compatibility_level** na exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  

> [!NOTE]  
> Um [banco de dados de distribuição](../../relational-databases/replication/distribution-database.md) criado em uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e atualizado para o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] RTM ou o Service Pack 1 tem um nível de compatibilidade 90, para o qual não há suporte em outros bancos de dados. Isso não tem um impacto sobre a funcionalidade de replicação. A atualização para service packs e versões posteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resultará no aumento do nível de compatibilidade do banco de dados de distribuição para que ele corresponda ao banco de dados **mestre**.

## <a name="compatibility-levels-and-sql-server-upgrades"></a>Níveis de compatibilidade e atualizações do SQL Server  
O nível de compatibilidade do banco de dados é uma ferramenta valiosa para ajudar na modernização de banco de dados, permitindo que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] seja atualizado, mantendo o status funcional de aplicativos conexão e o mesmo nível de compatibilidade do banco de dados antes da atualização. Desde que o aplicativo não precise aproveitar os aprimoramentos que estão disponíveis somente em um nível mais alto de compatibilidade do banco de dados, esta é uma abordagem válida para atualizar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e manter o nível de compatibilidade do banco de dados anterior. Para obter mais informações sobre como usar o nível de compatibilidade para compatibilidade com versões anteriores, veja [Uso do nível de compatibilidade para compatibilidade com versões anteriores](#using-compatibility-level-for-backward-compatibility) posteriormente neste artigo.    

Para um novo desenvolvimento ou quando um aplicativo existente exige o uso de novos recursos, bem como melhorias de desempenho feitas no espaço do otimizador de consulta, planeje atualizar o nível de compatibilidade do banco de dados para a versão mais recente disponível no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e garanta que o aplicativo funcione com esse nível de compatibilidade. Para obter mais detalhes sobre como atualizar o nível de compatibilidade do banco de dados, veja [Melhores práticas para atualizar o nível de compatibilidade do banco de dados](#best-practices-for-upgrading-database-compatibility-level) posteriormente no artigo.     

> [!TIP] 
> Se um aplicativo foi testado e certificado em determinada versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ele foi implicitamente testado e certificado naquele nível de compatibilidade do banco de dados nativo da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
> 
> Assim, o nível de compatibilidade do banco de dados fornece um caminho de certificação fácil para um aplicativo existente, ao usar o nível de compatibilidade do banco de dados correspondente com a versão testada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
>
> Para obter mais informações sobre as diferenças entre níveis de compatibilidade, veja as seções apropriadas mais adiante neste artigo. 

Para atualizar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para a versão mais recente, mantendo o nível de compatibilidade do banco de dados que existia antes da atualização e seu status de capacidade de suporte, é recomendável executar a validação de área de superfície funcional estática do código do aplicativo no banco de dados, usando a ferramenta [AMD (Assistente de Migração de Dados da Microsoft)](https://www.microsoft.com/download/details.aspx?id=53595). A ausência de erros na saída da ferramenta AMD, sobre a funcionalidade ausente ou incompatível, protege o aplicativo de qualquer regressão funcional na nova versão de destino. Para obter mais informações sobre a ferramenta AMD, veja [aqui](https://blogs.msdn.microsoft.com/datamigration/dma).

> [!NOTE] 
> O AMD é compatível com o nível de compatibilidade do banco de dados de 100 ou mais. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] como a versão de origem é excluído. 

> [!IMPORTANT] 
> A Microsoft recomenda que alguns testes mínimos sejam realizados para validar o sucesso de uma atualização, mantendo o nível de compatibilidade do banco de dados anterior. Você deve determinar quais testes mínimos são importantes para seu próprio aplicativo e cenário. 

> [!NOTE] 
> A Microsoft fornece proteção de forma do plano de consulta quando:
> - A nova versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (destino) é executada no hardware que é comparável ao hardware em que a versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (origem) estava em execução. 
> - O mesmo [nível de compatibilidade do banco de dados compatível](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#remarks) é usado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino e no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de origem. 
> 
> Qualquer regressão de forma do plano de consulta (em comparação com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de origem) que ocorre nas condições acima será tratada. Entre em contato com o atendimento ao cliente da Microsoft se esse for o caso.

## <a name="using-compatibility-level-for-backward-compatibility"></a>Usando o nível de compatibilidade para compatibilidade com versões anteriores  
A configuração do *nível de compatibilidade do banco de dados* afeta os comportamentos apenas do banco de dados especificado, e não do servidor inteiro. O nível de compatibilidade do banco de dados oferece apenas compatibilidade parcial com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].   

> [!TIP]
> Como o *nível de compatibilidade do banco de dados* é um nível de banco de dados de configuração, de um aplicativo em execução em uma versão mais recente do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ao usar um nível de compatibilidade de banco de dados mais antigo ainda pode aproveitar os aprimoramentos de nível de servidor sem requisitos para alterações de aplicativo.
>
> Eles incluem monitoramento avançado e melhorias de solução de problemas, com novas [Exibições de Gerenciamento Dinâmico do Sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) e [Eventos Estendidos](../../relational-databases/extended-events/extended-events.md). E também escalabilidade aprimorada, por exemplo, com [Soft NUMA Automático ](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa).

Começando com o modo de compatibilidade 130, qualquer plano de consulta novo que afete recursos foi adicionado intencionalmente apenas ao novo nível de compatibilidade. Isso foi feito para minimizar o risco durante as atualizações que surge da degradação do desempenho devido a alterações no plano de consulta.   
Da perspectiva do aplicativo, a meta é ainda deve ser atualizar para o último nível de compatibilidade em algum ponto no tempo, para herdar alguns dos novos recursos, bem como melhorias de desempenho feitas no espaço do otimizador de consulta, mas fazer isso de maneira controlada. Use o nível de compatibilidade mais baixo como um auxílio de migração mais seguro ao trabalhar com diferenças de versões nos comportamentos controlados pela configuração de nível de compatibilidade relevante. Para obter mais detalhes, incluindo o fluxo de trabalho recomendado para atualizar o nível de compatibilidade do banco de dados, veja [Melhores práticas para atualizar o nível de compatibilidade do banco de dados](#best-practices-for-upgrading-database-compatibility-level) posteriormente no artigo.  
  
> [!IMPORTANT]
> A funcionalidade descontinuada introduzida em uma versão específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é protegida pelo nível de compatibilidade. Refere-se à funcionalidade removida do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].
> 
> Por exemplo, a dica `FASTFIRSTROW` foi descontinuada no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e substituída pela dica `OPTION (FAST n )`. A definição do nível de compatibilidade do banco de dados como 110 não restaurará a dica descontinuada.
> Para obter mais informações sobre a funcionalidade descontinuada, consulte [Funcionalidade descontinuada do Mecanismo de Banco de Dados no SQL Server 2016](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md), [Funcionalidade descontinuada do Mecanismo de Banco de Dados no SQL Server 2014](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)), [Funcionalidade descontinuada do Mecanismo de Banco de Dados no SQL Server 2012](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)) e [Funcionalidade descontinuada do Mecanismo de Banco de Dados no SQL Server 2008](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)).

> [!IMPORTANT]
> As alterações recentes introduzidas em determinada versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **podem** não estar protegidas pelo nível de compatibilidade. Refere-se às alterações de comportamento entre versões do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Geralmente, o comportamento do [!INCLUDE[tsql](../../includes/tsql-md.md)] é protegido pelo nível de compatibilidade. No entanto, os objetos do sistema alterados ou removidos **não** são protegidos pelo nível de compatibilidade.
>
> Um exemplo de uma alteração recente **protegida** pelo nível de compatibilidade é uma conversão implícita dos tipos de dados datetime em datetime2. No nível de compatibilidade do banco de dados 130, eles mostram uma precisão aprimorada, levando em conta os milissegundos fracionários, resultando em diferentes valores convertidos. Para restaurar o comportamento de conversão anterior, defina o nível de compatibilidade do banco de dados como 120 ou inferior.
>
> Exemplos de alterações recentes **não protegidas** pelo nível de compatibilidade são:
> -  Alterações de nomes de coluna em objetos do sistema. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], a coluna *single_pages_kb* no sys.dm_os_sys_info foi renomeada para *pages_kb*. Seja qual for o nível de compatibilidade, a consulta `SELECT single_pages_kb FROM sys.dm_os_sys_info` gerará o erro 207 (Nome de coluna inválido).
> -  Objetos do sistema removidos. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o `sp_dboption` foi removido. Seja qual for o nível de compatibilidade, a instrução `EXEC sp_dboption 'AdventureWorks2016CTP3', 'autoshrink', 'FALSE';` gerará o erro 2812 (Não foi possível encontrar o procedimento armazenado 'sp_dboption').
>
> Para obter mais informações sobre alterações recentes, consulte [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2017](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2017.md), [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2016](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md), [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2014](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)), [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2012](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)) e [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2008](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)).
  
## <a name="best-practices-for-upgrading-database-compatibility-level"></a>Melhores práticas para atualizar o nível de compatibilidade do banco de dados 
Para obter o fluxo de trabalho recomendado para atualizar o nível de compatibilidade, consulte [Alterar o modo de compatibilidade do banco de dados e usar o Repositório de Consultas](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md).  

## <a name="compatibility-levels-and-stored-procedures"></a>Níveis de compatibilidade e procedimentos armazenados  
 Quando um procedimento armazenado é executado, ele usa o nível de compatibilidade atual do banco de dados no qual está definido. Quando a configuração de compatibilidade de um banco de dados é alterada, todos os seus procedimentos armazenados são recompilados automaticamente conforme necessário.  

## <a name="differences-between-compatibility-level-140-and-level-150"></a>Diferenças entre os níveis de compatibilidade 140 e 150  
Esta seção descreve os novos comportamentos introduzidos com o nível de compatibilidade 150.

No momento, o nível 150 de compatibilidade do banco de dados está em Visualização Pública para [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]. Esse nível de compatibilidade do banco de dados será associado à próxima geração de aprimoramentos de processamento de consulta, além do que foi introduzido no nível de compatibilidade 140 do banco de dados.     

Confira mais informações sobre os recursos de processamento de consulta habilitados no nível 150 de compatibilidade do banco de dados em [Novidades no SQL Server 2019](../../sql-server/what-s-new-in-sql-server-ver15.md) e em [Processamento inteligente de consultas em bancos de dados SQL](https://docs.microsoft.com/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017).

## <a name="differences-between-compatibility-level-130-and-level-140"></a>Diferenças entre os níveis de compatibilidade 130 e 140  
Esta seção descreve os novos comportamentos introduzidos com o nível de compatibilidade 140.

|Configuração de nível de compatibilidade 130 ou inferior|Configuração de nível de compatibilidade 140|  
|--------------------------------------------------|-----------------------------------------|  
|As estimativas de cardinalidade para instruções que referenciam funções com valor de tabela de várias instruções usam uma estimativa de linha fixa.|As estimativas de cardinalidade para instruções qualificadas que referenciam funções com valor de tabela de várias instruções usarão a cardinalidade real da saída da função.  Isso é habilitado por meio da **execução intercalada** para funções com valor de tabela de várias instruções.|
|Consultas de modo de lote que solicitam tamanhos insuficientes de concessão de memória que resultam em despejos em disco podem continuar apresentando problemas em execuções consecutivas.|Consultas de modo de lote que solicitam tamanhos insuficientes de concessão de memória que resultam em despejos em disco podem ter um melhor desempenho em execuções consecutivas. Isso é habilitado por meio de **comentários de concessão de memória do modo de lote** que atualizarão o tamanho da concessão de memória de um plano armazenado em cache se ocorreram despejos para operadores de modo de lote. |
|Consultas de modo de lote que solicitam um tamanho excessivo de concessão de memória que resulta em problemas de simultaneidade podem continuar apresentando problemas em execuções consecutivas.|Consultas de modo de lote que solicitam um tamanho excessivo de concessão de memória que resulta em problemas de simultaneidade podem ter uma melhor simultaneidade em execuções consecutivas. Isso é habilitado por meio de **comentários de concessão de memória do modo de lote** que atualizarão o tamanho de concessão de memória de um plano armazenado em cache se uma quantidade excessiva foi originalmente solicitada.|
|As consultas de modo de lote que contém operadores de junção são qualificadas para três algoritmos de junção física, incluindo loop aninhado, junção hash e junção de mesclagem. Se as estimativas de cardinalidade estiverem incorretas para entradas de junção, um algoritmo de junção inadequado poderá ser selecionado. Se isso ocorrer, o desempenho será afetado e o algoritmo de junção inadequado permanecerá em uso até que o plano armazenado em cache seja recompilado.|Há um operador de junção adicional chamado **junção adaptável**. Se as estimativas de cardinalidade estiverem incorretas para a entrada de junção de build externa, um algoritmo de junção inadequado poderá ser selecionado. Se isso ocorrer e a instrução for qualificada para uma junção adaptável, um loop aninhado será usado para entradas de junção menores e uma junção hash será usada para entradas de junção maiores dinamicamente sem a necessidade de recompilação. |
|Planos triviais que referenciam índices Columnstore não são qualificados para a execução em modo de lote. |Um plano trivial que referencia índices Columnstore será descartado em favor de um plano que é qualificado para a execução em modo de lote.|
|O operador `sp_execute_external_script` UDX apenas pode ser executado no modo de linha.|O operador `sp_execute_external_script` UDX é qualificado para a execução em modo de lote.|  
|As TVFs (funções com valor de tabela) de várias instruções não tem a execução intercalada |Execução intercalada de TVFs de várias instruções para melhorar a qualidade do plano.|

As correções que estavam sob o sinalizador de rastreamento 4199 em versões anteriores do SQL Server anteriores ao SQL Server 2017 agora estão habilitadas por padrão. Com o modo de compatibilidade 140. O sinalizador de rastreamento 4199 ainda será aplicável a novas correções do otimizador de consulta que são liberadas após o SQL Server 2017. Para obter informações sobre o Sinalizador de Rastreamento 4199, consulte [Sinalizador de rastreamento 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199).  
  
## <a name="differences-between-compatibility-level-120-and-level-130"></a>Diferenças entre os níveis de compatibilidade 120 e 130  
Esta seção descreve os novos comportamentos introduzidos com o nível de compatibilidade 130.   

|Configuração de nível de compatibilidade 120 ou inferior|Configuração de nível de compatibilidade 130|  
|--------------------------------------------------|-----------------------------------------|  
|O INSERT em uma instrução INSERT-SELECT é single-thread.|O INSERT em uma instrução INSERT-SELECT tem vários threads ou pode ter um plano paralelo.|  
|As consultas em uma tabela com otimização de memória são executadas no modo single-thread.|As consultas em uma tabela com otimização de memória agora podem ter planos paralelos.|  
|Introdução do avaliador de Cardinalidade do SQL 2014 **CardinalityEstimationModelVersion="120"**|Outras melhorias de CE (estimativa de cardinalidade) com o Modelo de Estimativa de Cardinalidade 130 que é visível em um Plano de consulta. **CardinalityEstimationModelVersion="130"**| 
|Alterações do modo de lote versus modo de linha com índices columnstore:<br /><ul><li>As classificações em uma tabela com índice Columnstore estão no modo de Linha <li>As agregações de função em janela operam no modo de linha, como `LAG` ou `LEAD` <li>Consultas em tabelas Columnstore com várias cláusulas distintas operadas no modo de Linha <li>Consultas em execução em MAXDOP 1 ou com um plano serial executadas no modo de Linha</li></ul>| Alterações do modo de lote versus modo de linha com índices columnstore:<br /><ul><li>As classificações em uma tabela com um índice Columnstore agora estão no modo de lote <li>As agregações em janela agora funcionam no modo de lote, como `LAG` ou `LEAD` <li>Consultas em tabelas Columnstore com várias cláusulas distintas operadas no modo de Lote <li>As consultas em execução em MAXDOP 1 ou com um plano serial são executadas no Modo de lote</li></ul>|  
|As estatísticas podem ser atualizadas automaticamente. | A lógica que atualiza automaticamente as estatísticas é mais agressiva em tabelas grandes.  Na prática, isso deve reduzir casos em que os clientes observaram problemas de desempenho de consultas nas quais as linhas recém-inseridas são consultadas com frequência, mas nas quais as estatísticas não foram atualizadas para incluir esses valores. |  
|O rastreamento 2371 é OFF por padrão no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. | O [Rastreamento 2371](https://blogs.msdn.microsoft.com/psssql/2016/10/04/default-auto-statistics-update-threshold-change-for-sql-server-2016/) é ON por padrão no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. O sinalizador de rastreamento 2371 instrui o atualizador automático de estatísticas a coletar uma amostra de um subconjunto menor, porém, mais inteligente, de linhas em uma tabela que tem um grande número de linhas. <br/> <br/> Uma melhoria é incluir na amostra mais linhas que foram inseridas recentemente. <br/> <br/> Outra melhoria é permitir que as consultas sejam executadas enquanto o processo de atualização de estatísticas está em execução, em vez de bloquear a consulta. |  
|Para o nível 120, são coletadas amostras das estatísticas por um processo *single*-thread.|Para o nível 130, são coletadas amostras das estatísticas por um processo de *vários* threads. |  
|253 chaves estrangeiras de entrada é o limite.| Uma tabela especificada pode ser referenciada por até 10.000 chaves estrangeiras de entrada ou referências semelhantes. Para restrições, consulte [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md). |  
|Os algoritmos de hash MD2, MD4, MD5, SHA e SHA1 preteridos são permitidos.|Apenas os algoritmos de hash SHA2_256 e SHA2_512 são permitidos.|
||O [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] inclui melhorias em algumas conversões de tipos de dados e outras operações (normalmente incomuns). Para obter detalhes, consulte [Melhorias do SQL Server 2016 no tratamento de alguns tipos de dados e operações incomuns](https://support.microsoft.com/help/4010261/sql-server-2016-improvements-in-handling-some-data-types-and-uncommon).|
|A função STRING_SPLIT não está disponível.|A função STRING_SPLIT está disponível somente no nível de compatibilidade 130 ou superior. Se o nível de compatibilidade do banco de dados for inferior a 130, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não poderá localizar nem executar a função STRING_SPLIT.|
  
As correções que estavam sob o sinalizador de rastreamento 4199 em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] agora estão habilitadas por padrão. Com o modo de compatibilidade 130. O sinalizador de rastreamento 4199 ainda será aplicável para novas correções do otimizador de consulta que são liberadas após [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Para usar o otimizador de consulta mais antigo no [!INCLUDE[ssSDS](../../includes/sssds-md.md)], é necessário selecionar o nível de compatibilidade 110. Para obter informações sobre o Sinalizador de Rastreamento 4199, consulte [Sinalizador de rastreamento 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199).  
  
## <a name="differences-between-lower-compatibility-levels-and-level-120"></a>Diferenças entre níveis de compatibilidade inferiores e o nível 120  
 Esta seção descreve os novos comportamentos apresentados com o nível de compatibilidade 120.  
  
|Configuração de nível de compatibilidade 110 ou inferior|Configuração de nível de compatibilidade 120|  
|--------------------------------------------------|-----------------------------------------|  
|O otimizador de consulta mais antigo é usado.|O [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] inclui melhorias significativas no componente que cria e otimiza planos de consulta. Esse novo recurso do otimizador de consulta depende do uso do nível de compatibilidade de banco de dados 120. Novos aplicativos de banco de dados devem ser desenvolvidos usando o nível de compatibilidade de banco de dados 120 para tirar proveito dessas melhorias. Os aplicativos migrados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem ser cuidadosamente testados para confirmar que o bom desempenho será mantido ou melhorado. Se o desempenho diminuir, você poderá definir o nível de compatibilidade de banco de dados como 110 ou menos, a fim de usar a metodologia de otimizador de consulta mais antiga.<br /><br /> A compatibilidade do banco de dados nível 120 usa um novo avaliador de cardinalidade que é ajustado para moderno data warehouse e cargas de trabalho OLTP. Antes de definir o nível de compatibilidade do banco de dados como 110 devido a problemas de desempenho, consulte as recomendações na seção Planos de consulta do tópico [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][Novidades do Mecanismo de Banco de Dados](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md).|  
|Em níveis de compatibilidade abaixo de 120, a configuração de idioma é ignorada durante a conversão de um valor de **date** em um valor de cadeia de caracteres. Observe que esse comportamento é específico apenas ao tipo **date**. Veja o exemplo B na seção Exemplos abaixo.|A configuração de idioma não é ignorada durante a conversão de um valor de **date** em um valor de cadeia de caracteres.|  
|As referências recursivas no lado direito de uma cláusula `EXCEPT` criam um loop infinito. O exemplo C na seção Exemplos abaixo demonstra esse comportamento.|As referências recursivas em uma cláusula `EXCEPT` geram um erro em conformidade com o padrão ANSI SQL.|  
|A CTE (expressão de tabela comum) recursiva permite nomes de coluna duplicados.|Uma CTE recursiva não permite nomes de coluna duplicados.|  
|Os gatilhos desabilitados serão habilitados se os gatilhos forem alterados.|A alteração de um gatilho não altera o estado (habilitado ou desabilitado) do gatilho.|  
|A cláusula de tabela OUTPUT INTO ignora o `IDENTITY_INSERT SETTING = OFF` e permite a inserção de valores explícitos.|Não é possível inserir valores explícitos para uma coluna de identidade em uma tabela quando `IDENTITY_INSERT` é definido como OFF.|  
|Quando a contenção do banco de dados é definida como parcial, a validação do campo `$action` na cláusula `OUTPUT` de uma instrução `MERGE` pode retornar um erro de ordenação.|A ordenação dos valores retornados pela cláusula `$action` de uma instrução `MERGE` é a ordenação de banco de dados, em vez da ordenação do servidor, e um erro de conflito de ordenação não é retornado.|  
|Uma instrução `SELECT INTO` sempre criará uma operação de inserção de thread único.|Uma instrução `SELECT INTO` pode criar uma operação de inserção paralela. Ao inserir um número grande de linhas, a operação paralela pode melhorar o desempenho.|  
  
## <a name="differences-between-lower-compatibility-levels-and-levels-110-and-120"></a>Diferenças entre níveis de compatibilidade inferiores e os níveis 110 e 120  
 Esta seção descreve os novos comportamentos apresentados com o nível de compatibilidade 110.   Esta seção também se aplica ao nível 120.  
  
|Configuração de nível de compatibilidade 100 ou inferior|Configuração de nível de compatibilidade 110, no mínimo|  
|--------------------------------------------------|--------------------------------------------------|  
|São executados objetos de banco de dados de CLR (Common Language Runtime) com a versão 4 do CLR. Porém, são evitadas algumas alterações de comportamento apresentadas na versão 4 do CLR. Para obter mais informações, consulte [Novidades da integração CLR](../../relational-databases/clr-integration/clr-integration-what-s-new.md).|São executados objetos de banco de dados de CLR com a versão 4 do CLR.|  
|As funções XQuery **string-length** e **substring** contam cada par alternativo como dois caracteres.|As funções XQuery **string-length** e **substring** contam cada par alternativo como um caractere.|  
|`PIVOT` é permitido em uma consulta CTE (expressão de tabela comum) recursiva. No entanto, a consulta retorna resultados incorretos quando há várias linhas por agrupamento.|`PIVOT` não é permitido em uma consulta CTE (expressão de tabela comum) recursiva. Um erro é retornado.|  
|O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.|Novo material não pode ser criptografado com RC4 ou RC4_128. Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.|  
|O estilo padrão de operações `CAST` e `CONVERT` nos tipos de dados **time** e **datetime2** é 121, exceto quando um dos tipos é usado em uma expressão de coluna computada. Para colunas computadas, o estilo padrão é 0. Esse comportamento afeta as colunas computadas quando são criadas, usadas em consultas que envolvam parametrização automática ou usadas em definições de restrição.<br /><br /> O exemplo D na seção Exemplos abaixo mostra a diferença entre os estilos 0 e 121. Não demonstra o comportamento descrito acima. Para obter mais informações sobre estilos de data e hora, consulte [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).|No nível de compatibilidade 110, o estilo padrão das operações `CAST` e `CONVERT` nos tipos de dados **time** e **datetime2** é sempre 121. Se a sua consulta depender do comportamento antigo, use um nível de compatibilidade inferior a 110 ou especifique explicitamente o estilo 0 na consulta afetada.<br /><br /> A atualização do banco de dados para o nível de compatibilidade 110 não alterará os dados de usuário que foram armazenados em disco. Você deve corrigir esses dados manualmente conforme apropriado. Por exemplo, se você usou `SELECT INTO` para criar uma tabela com base em uma fonte que continha uma expressão de coluna computada descrita acima, os dados (usando o estilo 0) serão armazenados, em vez da própria definição de coluna computada. Você precisará atualizar manualmente esses dados para que coincidam com o estilo 121.|  
|As colunas em tabelas remotas do tipo **smalldatetime** referenciadas em uma exibição particionada são mapeadas como **datetime**. As colunas correspondentes em tabelas locais (na mesma posição ordinal na lista de seleção) devem ser do tipo **datetime**.|As colunas em tabelas remotas do tipo **smalldatetime** referenciadas em uma exibição particionada são mapeadas como **smalldatetime**. As colunas correspondentes em tabelas locais (na mesma posição ordinal na lista de seleção) devem ser do tipo **smalldatetime**.<br /><br /> Depois de atualizar para 110, a exibição particionada distribuída falhará devido à incompatibilidade de tipo de dados. Resolva isso alterando o tipo de dados na tabela remota para **datetime** ou definindo o nível de compatibilidade do banco de dados local como 100 ou inferior.|  
|A função `SOUNDEX` implementa as seguintes regras:<br /><br /> 1) Um H ou W maiúsculo é ignorado durante a separação de duas consoantes que têm o mesmo número no código `SOUNDEX`.<br /><br /> 2) Se os primeiros dois caracteres de *character_expression* tiverem o mesmo número no código `SOUNDEX`, ambos os caracteres serão incluídos. Caso contrário, se um conjunto de consoantes lado a lado tiver o mesmo número no código `SOUNDEX`, todas as consoantes serão excluídas, exceto a primeira.|A função `SOUNDEX` implementa as seguintes regras:<br /><br /> 1) Se um H ou W maiúsculo separar duas consoantes que têm o mesmo número no código `SOUNDEX`, a consoante à direita será ignorada<br /><br /> 2) Se um conjunto de consoantes lado a lado tiver o mesmo número no código `SOUNDEX`, todas as consoantes serão excluídas, exceto a primeira.<br /><br /> <br /><br /> As regras adicionais podem fazer com que os valores calculados pela função `SOUNDEX` sejam diferentes dos valores calculados em níveis de compatibilidade anteriores. Após a atualização para o nível de compatibilidade 110, talvez seja necessário recriar os índices, os heaps ou as restrições CHECK que usam a função `SOUNDEX`. Para obter mais informações, veja [SOUNDEX &#40;Transact-SQL&#41;](../../t-sql/functions/soundex-transact-sql.md).|  
  
## <a name="differences-between-compatibility-level-90-and-level-100"></a>Diferenças entre os níveis de compatibilidade 90 e 100  
 Esta seção descreve os novos comportamentos apresentados com o nível de compatibilidade 100.  
  
|Configuração de nível de compatibilidade 90|Configuração de nível de compatibilidade 100|Possibilidade de impacto|  
|----------------------------------------|-----------------------------------------|---------------------------|  
|A configuração QUOTED_IDENTIFER sempre é definida como ON para funções com valor de tabela de várias instruções ao serem criadas, sem considerar a configuração do nível de sessão.|A configuração de sessão QUOTED IDENTIFIER é atendida quando funções com valor de tabela de várias instruções são criadas.|Média|  
|Ao criar ou alterar uma função de partição, os literais **datetime** e **smalldatetime** na função são avaliados, considerando US_English como a configuração de idioma.|A configuração atual de idioma é usada para avaliar **datetime** e literais de **smalldatetime** na função de partição.|Média|  
|A cláusula `FOR BROWSE` é permitida (e ignorada) em instruções `INSERT` e `SELECT INTO`.|A cláusula `FOR BROWSE` não é permitida em instruções `INSERT` e `SELECT INTO`.|Média|  
|Predicados de texto completo são permitidos na cláusula `OUTPUT`.|Predicados de texto completo não são permitidos na cláusula `OUTPUT`.|Baixa|  
|`CREATE FULLTEXT STOPLIST`, `ALTER FULLTEXT STOPLIST` e `DROP FULLTEXT STOPLIST` não são compatíveis. A lista de palavras irrelevantes do sistema é associada automaticamente a novos índices de texto completo.|`CREATE FULLTEXT STOPLIST`, `ALTER FULLTEXT STOPLIST` e `DROP FULLTEXT STOPLIST` são compatíveis.|Baixa|  
|`MERGE` não é imposto como uma palavra-chave reservada.|MERGE é uma palavra-chave completamente reservada. A instrução `MERGE` é compatível com os níveis de compatibilidade 100 e 90.|Baixa|  
|O uso do argumento \<dml_table_source> da instrução INSERT gera um erro de sintaxe.|Além disso, você pode capturar os resultados de uma cláusula OUTPUT em uma instrução INSERT, UPDATE, DELETE ou MERGE aninhada e inserir esses resultados em uma tabela ou exibição de destino. Isto é feito com o argumento \<dml_table_source> da instrução INSERT.|Baixa|
|A menos que `NOINDEX` seja especificado, `DBCC CHECKDB` ou `DBCC CHECKTABLE` executará verificações de consistência física e lógica em uma única tabela ou exibição indexada e em todos os seus índices não clusterizados e XML. Não há suporte para índices espaciais.|A menos que `NOINDEX` seja especificado, `DBCC CHECKDB` ou `DBCC CHECKTABLE` executará verificações de consistência física e lógica em uma única tabela e em todos os seus índices não clusterizados. Entretanto, em índices XML, índices espaciais e exibições indexadas, por padrão são executadas somente as verificações de consistência física.<br /><br /> Se `WITH EXTENDED_LOGICAL_CHECKS` for especificado, verificações lógicas serão executadas em exibições indexadas, índices XML e índices espaciais, quando presentes. Por padrão, as verificações de consistência física são executadas antes das verificações de consistência lógica. Se `NOINDEX` também estiver especificado, apenas as verificações lógicas serão executadas.|Baixa|  
|Quando uma cláusula OUTPUT é usada com uma instrução DML que causa um erro de tempo de execução durante sua execução, a transação inteira é encerrada e revertida.|Quando uma cláusula `OUTPUT` é usada com uma instrução DML (linguagem de manipulação de dados) e ocorre um erro em tempo de execução durante sua execução, o comportamento depende da configuração de `SET XACT_ABORT`. Se `SET XACT_ABORT` for OFF, um erro de anulação de instrução gerado pela instrução DML que usa a cláusula `OUTPUT` terminará a instrução, mas a execução do lote continuará e a transação não será revertida. Se `SET XACT_ABORT` for ON, todos os erros em tempo de execução gerados pela instrução DML que usam a cláusula OUTPUT terminarão o lote e a transação será revertida.|Baixa|  
|CUBE e ROLLUP não são impostos como palavras-chave reservadas.|`CUBE` e `ROLLUP` são palavras-chave reservadas dentro da cláusula GROUP BY.|Baixa|  
|A validação restrita é aplicada a elementos do tipo **anyType** XML.|A validação incerta é aplicada a elementos do tipo **anyType**. Para obter mais informações, consulte [Componentes curinga e validação de conteúdo](../../relational-databases/xml/wildcard-components-and-content-validation.md).|Baixa|  
|Não é possível consultar ou modificar os atributos especiais **xsi:nil** e **xsi:type** por instruções de linguagem de manipulação de dados.<br /><br /> Isso significa que `/e/@xsi:nil` falha, enquanto `/e/@*` ignora os atributos **xsi:nil** e **xsi:type**. No entanto, `/e` retorna os atributos **xsi:nil** e **xsi:type** para manter a consistência com `SELECT xmlCol`, mesmo se `xsi:nil = "false"`.|Os atributos especiais **xsi:nil** e **xsi:type** são armazenados como atributos normais e podem ser consultados e modificados.<br /><br /> Por exemplo, a execução da consulta `SELECT x.query('a/b/@*')` retorna todos os atributos, incluindo **xsi:nil** e **xsi:type**. Para excluir estes tipos da consulta, substitua `@*` por `@*[namespace-uri(.) != "`*insert xsi namespace uri*`"` e não `(local-name(.) = "type"` nem `local-name(.) ="nil".`|Baixa|  
|Uma função definida pelo usuário que converte um valor constante da cadeia de caracteres XML para um tipo de datetime do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é marcada como determinista.|Uma função definida pelo usuário que converte um valor constante de cadeia de caracteres XML em um tipo datetime do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é marcado como não determinista.|Baixa|  
|Os tipos de listas e união de XML não são totalmente suportados.|Os tipos de lista e união são totalmente suportados, inclusive as seguintes funcionalidades:<br /><br /> União de lista<br /><br /> União de união<br /><br /> Lista de tipos atômicos<br /><br /> Lista de união|Baixa|  
|As opções SET requeridas para um método xQuery não são validadas quando o método é contido em uma exibição ou função com valor de tabela embutida.|As opções SET requeridas para um método xQuery são validadas quando o método é contido em uma exibição ou função com valor de tabela embutida. Um erro ocorrerá se as opções SET do método forem definidas incorretamente.|Baixa|  
|Os valores do atributo XML que contém caracteres de final de linha (retorno de carro e alimentação de linha) não são normalizados de acordo com o padrão XML. Isto é, ambos os caracteres são retornados, em vez de um único caractere de alimentação de linha.|Os valores do atributo XML que contém caracteres de final de linha (retorno de carro e alimentação de linha) são normalizados de acordo com o padrão XML. Isto é, todas as quebras de linha em entidades externas de análise (incluindo a entidade do documento) são normalizadas na entrada pela tradução da sequência de dois caracteres #xD #xA e de qualquer #xD que não seja seguido por #xA em um único caractere #xA.<br /><br /> Aplicativos que usam atributos para transportar valores da cadeia de caracteres que contêm caracteres de final de linha não receberão de volta estes caracteres, já que eles foram submetidos. Para evitar o processo de normalização, use as entidades de caractere numérico XML para codificar todos os caracteres de final de linha.|Baixa|  
|As propriedades `ROWGUIDCOL` e `IDENTITY` da coluna podem ser nomeadas incorretamente como uma restrição. Por exemplo, a instrução `CREATE TABLE T (C1 int CONSTRAINT MyConstraint IDENTITY)` executa, mas o nome da restrição não é preservado e não fica acessível ao usuário.|As propriedades `ROWGUIDCOL` e `IDENTITY` da coluna não podem ser nomeadas como uma restrição. O erro 156 é retornado.|Baixa|  
|A atualização de colunas usando atribuição bidirecional, como `UPDATE T1 SET @v = column_name = <expression>`, pode produzir resultados inesperados porque o valor de tempo de vida da variável pode ser usado em outras cláusulas, como nas cláusulas `WHERE` e `ON`, durante a execução da instrução, em vez do valor inicial da instrução. Isto pode causar a alteração imprevisível dos significados dos predicados em uma base por linha.<br /><br /> Este comportamento só é aplicável quando o nível de compatibilidade é definido em 90.|A atualização de colunas usando uma atribuição bidirecional gera resultados esperados porque só o valor inicial da instrução é acessado durante a execução da instrução.|Baixa|  
|Veja o exemplo E na seção Exemplos abaixo.|Veja o exemplo F na seção Exemplos abaixo.|Baixa|  
|A função ODBC {fn CONVERT()} usa o formato de data padrão do idioma. Em alguns idiomas, o formato padrão é YDM, o que pode resultar em erros de conversão quando CONVERT() é combinado com outras funções, como `{fn CURDATE()}`, que espera um formato YMD.|A função ODBC `{fn CONVERT()}` usa o estilo 121 (um formato YMD independente de linguagem) ao converter os tipos de dados ODBC SQL_TIMESTAMP, SQL_DATE, SQL_TIME, SQLDATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP.|Baixa|  
|Datetime intrínseco, como DATEPART, não exige que os valores de entrada de cadeia de caracteres sejam literais válidas de datetime. Por exemplo, `SELECT DATEPART (year, '2007/05-30')` é compilado com êxito.|Partes intrínsecas de datetime, como `DATEPART`, exigem que os valores de entrada de cadeia de caracteres sejam literais de datetime válidos. Erro 241 é retornado quando um datetime literal inválido é usado.|Baixa|  
  
## <a name="reserved-keywords"></a>Palavras-chave reservadas  
 A configuração de compatibilidade também determina as palavras-chave que são reservadas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)]. A tabela a seguir mostra as palavras-chave reservadas que são introduzidas em cada nível de compatibilidade.  
  
|Configuração de nível de compatibilidade|Palavras-chave reservadas|  
|----------------------------------|-----------------------|  
|130|A ser determinado.|  
|120|Nenhum.|  
|110|WITHIN GROUP, TRY_CONVERT, SEMANTICKEYPHRASETABLE, SEMANTICSIMILARITYDETAILSTABLE, SEMANTICSIMILARITYTABLE|  
|100|CUBE, MERGE, ROLLUP|  
|90|EXTERNAL, PIVOT, UNPIVOT, REVERT, TABLESAMPLE|  
  
 Em um determinado nível de compatibilidade, as palavras-chave reservadas incluem todas as palavras-chave introduzidas naquele nível ou abaixo dele. Por exemplo, para aplicativos no nível 110, todas as palavras-chave listadas na tabela anterior são reservadas. Nos níveis de compatibilidade inferiores, as palavras-chave de nível 100 permanecem nomes de objeto válidos, mas os recursos de idioma de nível 110 correspondentes a essas palavras-chave não estão disponíveis.  
  
 Uma vez introduzida, uma palavra-chave permanece reservada. Por exemplo, a palavra-chave reservada PIVOT, que foi incorporada no nível de compatibilidade 90, também é reservada nos níveis 100, 110 e 120.  
  
 Se um aplicativo usar um identificador que é reservado como uma palavra-chave no seu nível de compatibilidade, o aplicativo falhará. Para solucionar esse problema, inclua o identificador entre colchetes (**[]**) ou aspas (**""**); por exemplo, para atualizar um aplicativo que usa o identificador **EXTERNAL** com o nível de compatibilidade 90, você pode alterar o identificador para **[EXTERNAL]** ou **"EXTERNAL"**.  
  
 Para obter mais informações, consulte [Palavras-chave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-compatibility-level"></a>A. Alterando o nível de compatibilidade  
 O exemplo a seguir altera o nível de compatibilidade do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] para `110,`[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET COMPATIBILITY_LEVEL = 110;  
GO  
```  
  
 O exemplo a seguir retorna o nível de compatibilidade do banco de dados atual.  
  
```sql  
SELECT name, compatibility_level   
FROM sys.databases   
WHERE name = db_name();  
```  
  
### <a name="b-ignoring--the-set-language-statement-except-under-compatibility-level-120"></a>b. Ignorando a instrução SET LANGUAGE, exceto no nível de compatibilidade 120  
 A consulta a seguir ignora a instrução SET LANGUAGE, exceto no nível de compatibilidade 120.  
  
```sql  
SET DATEFORMAT dmy;   
DECLARE @t2 date = '12/5/2011' ;  
SET LANGUAGE dutch;   
SELECT CONVERT(varchar(11), @t2, 106);   
  
-- Results when the compatibility level is less than 120.   
12 May 2011   
  
-- Results when the compatibility level is set to 120).  
12 mei 2011  
```  
  
### <a name="c"></a>C.  
 Para a configuração do nível de compatibilidade 110 ou inferior, as referências recursivas no lado direito de uma cláusula EXCEPT criam um loop infinito.  
  
```sql  
WITH   
cte AS (SELECT * FROM (VALUES (1),(2),(3)) v (a)),  
r   
AS (SELECT a FROM Table1  
UNION ALL  
(SELECT a FROM Table1 EXCEPT SELECT a FROM r) )   
SELECT a   
FROM r;  
  
```  
  
### <a name="d"></a>D.  
 Este exemplo mostra a diferença entre os estilos 0 e 121. Para obter mais informações sobre estilos de data e hora, consulte [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
```sql  
CREATE TABLE t1 (c1 time(7), c2 datetime2);   
  
INSERT t1 (c1,c2) VALUES (GETDATE(), GETDATE());  
  
SELECT CONVERT(nvarchar(16),c1,0) AS TimeStyle0  
       ,CONVERT(nvarchar(16),c1,121)AS TimeStyle121  
       ,CONVERT(nvarchar(32),c2,0) AS Datetime2Style0  
       ,CONVERT(nvarchar(32),c2,121)AS Datetime2Style121  
FROM t1;  
  
-- Returns values such as the following.  
TimeStyle0       TimeStyle121       
Datetime2Style0      Datetime2Style121  
---------------- ----------------   
-------------------- --------------------------  
3:15PM           15:15:35.8100000   
Jun  7 2011  3:15PM  2011-06-07 15:15:35.8130000  
```  
  
### <a name="e"></a>E.  
 A atribuição de variável é permitida em uma instrução que contém um operador UNION de nível superior, mas retorna resultados inesperados. Por exemplo, nas instruções a seguir, o valor da coluna `@v` da união de duas tabelas é atribuído ao `BusinessEntityID` da variável local. Por definição, quando a instrução SELECT retorna mais de um valor, a variável é atribuída ao último valor retornado. Neste caso, a variável é atribuída corretamente ao último valor, porém, o conjunto de resultados da instrução SELECT UNION também é retornado.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET compatibility_level = 110;  
GO  
USE AdventureWorks2012;  
GO  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM HumanResources.Employee  
UNION ALL  
SELECT @v = BusinessEntityID FROM HumanResources.EmployeeAddress;  
SELECT @v;  
```  
  
### <a name="f"></a>F.  
 A atribuição da variável não é permitida em uma instrução que contenha um operador UNION de nível superior. O erro 10734 é retornado. Para resolver o erro, reescreva a consulta como demonstrado no exemplo a seguir.  
  
```sql  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM   
    (SELECT BusinessEntityID FROM HumanResources.Employee  
     UNION ALL  
     SELECT BusinessEntityID FROM HumanResources.EmployeeAddress) AS Test;  
SELECT @v;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Palavras-chave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlserver)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
 [Exibir ou alterar o nível de compatibilidade de um banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) 
  
