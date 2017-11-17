---
title: "ALTERAR o nível de compatibilidade do banco de dados (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
ms.assetid: ca5fd220-d5ea-4182-8950-55d4101a86f6
caps.latest.revision: 89
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7b65511b09f2a94d30c39c1f97ed88cfbfab855b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-transact-sql-compatibility-level"></a>ALTERAR o nível de compatibilidade do banco de dados (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  
Define certos comportamentos de banco de dados como sendo compatíveis com a versão especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter outras opções de ALTER DATABASE, consulte [ALTER DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER DATABASE database_name   
SET COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 | 90 }  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 É o nome do banco de dados a ser modificado.  
  
 COMPATIBILITY_LEVEL {140 | 130 | 120 | 110 | 100 | 90 | 80}  
 É a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a qual o banco de dados será compatível. Os seguintes valores de nível de compatibilidade podem ser configurados:  
  
|Product|Versão do mecanismo de banco de dados|Designação de nível de compatibilidade|Valores de nível de compatibilidade com suporte|  
|-------------|-----------------------------|-------------------------------------|------------------------------------------|  
|[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]|14|140|140, 130, 120, 110, 100|
|[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|12|130|140, 130, 120, 110, 100|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|13|130|130, 120, 110, 100|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|12|120|120, 110, 100|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|11|110|110, 100, 90|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|10.5|100|100, 90, 80|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|10|100|100, 90, 80|  
|SQL Server 2005|9|90|90, 80|  
|SQL Server 2000|8|80|80|  
  
> [!NOTE]  
>  **Banco de dados do SQL Azure** V12 foi lançado em dezembro de 2014. Um aspecto da versão era que bancos de dados recém-criados tinham seu nível de compatibilidade definido como 120. No 2015 banco de dados SQL passou a oferecer suporte para nível 130, embora o padrão permanece como 120.  
> 
> A partir do **meados de junho de 2016**, no banco de dados SQL Azure, o nível de compatibilidade padrão são 130 em vez de 120 para **recém-criado** bancos de dados. Bancos de dados existentes criados antes de meados de junho de 2016 não são afetados e mantenham seu nível de compatibilidade atual (100, 110 e 120). 
> 
> Se você geralmente deseja nível 130 para seu banco de dados, mas você tiver motivo preferir o nível 110 **estimativa de cardinalidade** algoritmo, consulte [ALTER DATABASE SCOPED CONFIGURATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)e em particular sua palavra-chave LEGACY_CARDINALITY_ESTIMATION = ON.  
>  
>  Para obter detalhes sobre como avaliar as diferenças de desempenho das consultas mais importantes, entre dois níveis de compatibilidade no banco de dados SQL Azure, consulte [melhor desempenho de consultas com compatibilidade nível 130 no banco de dados do SQL Azure](http://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/).


 Execute a consulta a seguir para determinar a versão do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que você está conectado.  
  
```tsql  
SELECT SERVERPROPERTY('ProductVersion');  
```  
  
> [!NOTE]  
>  Nem todos os recursos que variam de acordo com o nível de compatibilidade são suportados em [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  

 Para determinar o nível de compatibilidade atual, consulte o **compatibility_level** coluna [sys. Databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
```tsql  
SELECT name, compatibility_level FROM sys.databases;  
```  
  
## <a name="remarks"></a>Comentários  
 Para todas as instalações de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o nível de compatibilidade padrão é definido para a versão de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Bancos de dados são definidos para esse nível, a menos que o **modelo** banco de dados tem um nível de compatibilidade inferior. Quando um banco de dados é atualizado de qualquer versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o banco de dados retém seu nível de compatibilidade se for pelo menos mínimo permitido para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Atualizando um banco de dados com um nível de compatibilidade menor do que o nível permitido, define o banco de dados para a compatibilidade mais baixa nível permitida. Isso se aplica aos bancos de dados do sistema e de usuário. Use **ALTER DATABASE** para alterar o nível de compatibilidade do banco de dados. Para exibir o nível de compatibilidade atual de um banco de dados, consulte o **compatibility_level** coluna o **sys. Databases** exibição do catálogo.  

  
## <a name="using-compatibility-level-for-backward-compatibility"></a>Usando o nível de compatibilidade para compatibilidade com versões anteriores  
 O nível de compatibilidade afeta os comportamentos apenas do banco de dados especificado e não do servidor inteiro. O nível de compatibilidade oferece apenas compatibilidade parcial com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Começando com o modo de compatibilidade 130, os novos recursos que afetam de plano de consulta foram adicionados apenas para o novo modo de compatibilidade. Isso foi feito para minimizar o risco durante as atualizações que são provenientes de degradação de desempenho devido a alterações nos planos de consulta. Da perspectiva do aplicativo, a meta é ainda estar no nível de compatibilidade mais recente para herdar alguns dos novos recursos, bem como melhorias de desempenho feitas no espaço de Otimizador de consulta, mas fazer isso de maneira controlada. Use o nível de compatibilidade como um auxílio de migração provisório ao trabalhar com diferenças de versões nos comportamentos que são controlados pela definição de nível de compatibilidade relevante. Para obter mais detalhes, consulte as práticas recomendadas atualização posteriormente neste artigo.  
  
 Se existirem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicativos são afetados pelas diferenças de comportamento na sua versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], converta o aplicativo para trabalhar diretamente com o novo modo de compatibilidade. Em seguida, use **ALTER DATABASE** para alterar o nível de compatibilidade para 130. A nova configuração de compatibilidade de banco de dados tem efeito quando um **banco de dados de uso** é emitido ou um novo logon é processado com esse banco de dados do banco de dados padrão.  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Alterar o nível de compatibilidade enquanto os usuários estão conectados ao banco de dados pode gerar conjuntos de resultados incorretos para consultas ativas. Por exemplo, se o nível de compatibilidade for alterado enquanto um plano de consulta estiver sendo compilado, o plano compilado poderá basear-se nos níveis de compatibilidade antigos e novos, gerando um plano incorreto e, provavelmente, resultados imprecisos. Além disso, o problema pode ser maior se o plano for colocado no cache de planos e reutilizado em consultas subsequentes. Para evitar resultados de consulta imprecisos, recomendamos o seguinte procedimento ao alterar o nível de compatibilidade de um banco de dados:  
  
1.  Defina o banco de dados para o modo de acesso de usuário único, usando ALTER DATABASE SET SINGLE_USER.  
  
2.  Altere o nível de compatibilidade do banco de dados.  
  
3.  Coloque o banco de dados no modo de acesso multiusuário usando ALTER DATABASE SET MULTI_USER.  
  
4.  Para obter mais informações sobre como definir o modo de acesso de um banco de dados, consulte [ALTER DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="compatibility-levels-and-stored-procedures"></a>Níveis de compatibilidade e procedimentos armazenados  
 Quando um procedimento armazenado é executado, ele usa o nível de compatibilidade atual do banco de dados no qual está definido. Quando a configuração de compatibilidade de um banco de dados é alterada, todos os seus procedimentos armazenados são recompilados automaticamente conforme necessário.  

## <a name="differences-between-compatibility-level-130-and-level-140"></a>Diferenças entre o nível de compatibilidade 130 e nível de 140  
Esta seção descreve os novos comportamentos apresentados com o nível de compatibilidade 140.

|Configuração de nível de compatibilidade 130 ou inferior|Configuração de nível de compatibilidade de 140|  
|--------------------------------------------------|-----------------------------------------|  
|Estimativas de cardinalidade para instruções que referenciam com valor de tabela de várias instruções funções usam uma estimativa de linha fixa.|Estimativas de cardinalidade para instruções qualificadas referenciando o valor de tabela de várias instruções funções usará a cardinalidade real da saída da função.  Isso é habilitado por meio de **intercaladas execução** para funções com valor de tabela de várias instruções.|
|Consultas em modo de lote que solicitam a memória insuficiente concessão tamanhos que resultam em derramamentos disco pode continuar a ter problemas em execuções consecutivas.|Consultas em modo de lote que solicitam tamanhos de concessão de memória insuficiente que resultam em derramamentos em disco pode ter melhor desempenho em execuções consecutivos.  Isso é habilitado por meio de **comentários de concessão de memória do modo de lote** que atualizará o tamanho da concessão de memória de um plano armazenado em cache se derramamentos ocorreram para operadores de modo de lote. |
|Consultas em modo de lote que solicitam uma memória excessiva conceder tamanho que resulta em problemas de simultaneidade pode continuar a ter problemas em execuções consecutivas.|Consultas em modo de lote que solicitam uma memória excessiva concedem tamanho que resulta em problemas de simultaneidade pode ter melhor simultaneidade em execuções consecutivas.  Isso é habilitado por meio de **comentários de concessão de memória do modo de lote** que atualizará o tamanho da concessão de memória de um plano armazenado em cache se uma quantidade excessiva foi originalmente solicitada.|
|Consultas em modo de lote que contém operadores de junção são elegíveis para três algoritmos de junção física, incluindo o loop aninhado, junção de hash e junção de mesclagem.  Se as estimativas de cardinalidade estiverem incorretas para entradas de junção, um algoritmo de junção inadequada pode ser selecionado.  Se isso ocorrer, o desempenho será afetado e o algoritmo de junção inadequado permanecerá em uso até que o plano armazenado em cache é recompilado.|Há um operador de junção adicional chamado **junção adaptável**. Se as estimativas de cardinalidade estiverem incorretas para a entrada de junção de compilação externo, um algoritmo de junção inadequada pode ser selecionado.  Se isso ocorre e a instrução é qualificada para uma junção adaptável, um loop aninhado será usado para entradas de junção menores e uma junção de hash será usada para entradas de junção maior dinamicamente sem a necessidade de recompilação. |
|Triviais planos referenciar índices Columnstore não são qualificados para execução em modo de lote. |Um plano trivial referenciando índices Columnstore será descartado em favor de um plano que é qualificado para execução em modo de lote.|
|O operador UDX sp_execute_external_script só pode executar no modo de linha.|O operador UDX sp_execute_external_script está qualificado para execução em modo de lote.|  
|TVF com várias instruções não tem execução intercalada |Execução intercalada de várias instruções TVFs melhorar a qualidade do plano. |

Correções sob o sinalizador de rastreamento 4199 em versões anteriores do SQL Server anterior ao SQL Server 2017 agora estão habilitadas por padrão. Com o modo de compatibilidade 140. Sinalizador de rastreamento 4199 ainda será aplicável para novas correções do otimizador de consulta que são liberadas após 2017 do SQL Server. Para obter informações sobre o sinalizador de rastreamento 4199, consulte [sinalizador de rastreamento 4199](https://support.microsoft.com/en-us/kb/974006).  
  
## <a name="differences-between-compatibility-level-120-and-level-130"></a>Diferenças entre o nível de compatibilidade 120 e 130 nível  
Esta seção descreve os novos comportamentos apresentados com o nível de compatibilidade 130.   

  
|Configuração de nível de compatibilidade de 120 ou inferior|Configuração de nível de compatibilidade de 130|  
|--------------------------------------------------|-----------------------------------------|  
|A inserção em uma instrução Insert select é de thread único.|A inserção em uma instrução Insert select é multi-threaded ou pode ter um plano paralelo.|  
|Consultas em uma tabela com otimização de memória executam single-threaded.|Consultas em uma tabela com otimização de memória agora podem ter planos paralelos.|  
|Introduziu o avaliador de cardinalidade do SQL 2014 **CardinalityEstimationModelVersion = "120"**|Planejar a cardinalidade mais melhorias de CE (estimativa) com a 130 de modelo de estimativa de cardinalidade que é visível de uma consulta. **CardinalityEstimationModelVersion = "130"**|  
|Modo de lote em relação a alterações de modo de linha com índices Columnstore<br /><br /> Classifica em uma tabela com índice Columnstore está no modo de linha<br /><br /> Agregações de função em janela operam no modo de linha, como LATÊNCIA ou avanço<br /><br /> Consultas em tabelas Columnstore com várias cláusulas distintas operavam no modo de linha<br /><br /> Consultas em execução no MAXDOP 1 ou com um plano serial executado no modo de linha | Modo de lote em relação a alterações de modo de linha com índices Columnstore<br /><br /> Classifica em uma tabela com um índice Columnstore agora está em modo de lote<br /><br /> Agregações em janela agora operam em modo de lote, como LATÊNCIA ou avanço<br /><br /> Consultas em tabelas Columnstore com várias cláusulas distintas operam em modo de lote<br /><br /> Executam consultas em execução em Maxdop1 ou com um plano serial em modo de lote|  
| As estatísticas podem ser atualizadas automaticamente. | A lógica que atualiza automaticamente estatísticas é mais agressiva em tabelas grandes.  Na prática, isso deve reduzir casos em que os clientes observados problemas de desempenho de consultas onde as linhas recentemente inseridas são consultadas com frequência, mas em que as estatísticas não tiveram sido atualizadas para incluir os valores. |  
| Rastreamento 2371 é desativado por padrão em [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. | [Rastreamento 2371](https://blogs.msdn.microsoft.com/psssql/2016/10/04/default-auto-statistics-update-threshold-change-for-sql-server-2016/) está ON por padrão em [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Sinalizador de rastreamento 2371 informa o atualizador de estatísticas automática para um subconjunto menor ainda mais sensato de linhas em uma tabela que tem um grande número de linhas de exemplo. <br/> <br/> É uma melhoria incluir o exemplo mais linhas que foram inseridas recentemente. <br/> <br/> Outro aprimoramento é permitir que consultas executado enquanto o processo de atualização de estatísticas está em execução, em vez de bloquear a consulta. |  
| Para o nível 120, as estatísticas são amostradas por um *único*-processo de thread. | Para nível 130, as estatísticas são amostradas por um *várias*-processo de thread. |  
| 253 chaves estrangeiras entradas é o limite. | Uma determinada tabela pode ser referenciada por chaves estrangeiras de entrada até 10.000 ou referências semelhantes. Para restrições, consulte [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md). |  
|Os algoritmos de hash MD2, MD4, MD5, SHA e SHA1 preteridos são permitidos.|Algoritmos de hash SHA2_256 e SHA2_512 só são permitidos.|  
  
  
Sinalizador de correções que estavam abaixo de rastreamento 4199 em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] agora estão habilitadas por padrão. Com o modo de compatibilidade 130. Sinalizador de rastreamento 4199 ainda será aplicável para novas correções do otimizador de consulta que são liberadas após [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Para usar o otimizador de consulta mais antigo no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] você deve selecionar o nível de compatibilidade 110. Para obter informações sobre o sinalizador de rastreamento 4199, consulte [sinalizador de rastreamento 4199](https://support.microsoft.com/en-us/kb/974006).  
  
## <a name="differences-between-lower-compatibility-levels-and-level-120"></a>Diferenças entre níveis de compatibilidade inferiores e o nível 120  
 Esta seção descreve os novos comportamentos apresentados com o nível de compatibilidade 120.  
  
|Configuração de nível de compatibilidade 110 ou inferior|Configuração de nível de compatibilidade 120|  
|--------------------------------------------------|-----------------------------------------|  
|O otimizador de consulta mais antigo é usado.|O [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] inclui melhorias significativas no componente criado por ele e planos de consulta otimizados. Esse novo recurso do otimizador de consulta depende do uso do nível de compatibilidade de banco de dados 120. Novos aplicativos de banco de dados devem ser desenvolvidos usando o nível de compatibilidade de banco de dados 120 para tirar proveito dessas melhorias. Os aplicativos migrados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem ser cuidadosamente testados para confirmar que o bom desempenho será mantido ou melhorado. Se o desempenho diminuir, você poderá definir o nível de compatibilidade de banco de dados como 110 ou menos, a fim de usar a metodologia de otimizador de consulta mais antiga.<br /><br /> A compatibilidade do banco de dados nível 120 usa um novo avaliador de cardinalidade que é ajustado para moderno data warehouse e cargas de trabalho OLTP. Antes de definir o nível de compatibilidade do banco de dados como 110 devido a problemas de desempenho, consulte as recomendações na seção de planos de consulta o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [o que há de novo no mecanismo de banco de dados](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md) tópico.|  
|Em níveis de compatibilidade inferiores a 120, a configuração de idioma é ignorada ao converter uma **data** valor para um valor de cadeia de caracteres. Observe que esse comportamento é específico apenas o **data** tipo. Veja o exemplo B na seção exemplos abaixo.|A configuração de idioma não é ignorada ao converter uma **data** valor para um valor de cadeia de caracteres.|  
|As referências recursivas no lado direito de uma cláusula EXCEPT criam um loop infinito. Exemplo C na seção exemplos abaixo demonstra esse comportamento.|As referências recursivas em uma cláusula EXCEPT gerencia um erro em conformidade com o padrão ANSI SQL.|  
|Uma CTE recursiva permite nomes de coluna duplicados.|Uma CTE recursiva não permite nomes de coluna duplicados.|  
|Os gatilhos desabilitados serão habilitados se os gatilhos forem alterados.|A alteração de um gatilho não altera o estado (habilitado ou desabilitado) do gatilho.|  
|A cláusula de tabela OUTPUT INTO ignora IDENTITY_INSERT SETTING = OFF e permite que os valores explícitos sejam inseridos.|Você não pode inserir valores explícitos de uma coluna de identidade em uma tabela quando IDENTITY_INSERT for definido como OFF.|  
|Quando a contenção do banco de dados for definida como parcial, a validação do campo $action na cláusula OUTPUT de uma instrução MERGE poderá retornar um erro de agrupamento.|O agrupamento dos valores retornados pela cláusula $action de uma instrução MERGE é o agrupamento de banco de dados, e não o agrupamento do servidor, e um erro de conflito de agrupamento não será retornado.|  
|Um **SELECT INTO** instrução sempre cria uma operação de inserção de thread único.|Um **SELECT INTO** instrução pode criar uma operação de inserção paralela. Ao inserir um número grande de linhas, a operação paralela pode melhorar o desempenho.|  
  
## <a name="differences-between-lower-compatibility-levels-and-levels-110-and-120"></a>Diferenças entre níveis de compatibilidade inferiores e os níveis 110 e 120  
 Esta seção descreve os novos comportamentos apresentados com o nível de compatibilidade 110.   Esta seção também se aplica ao nível 120.  
  
|Configuração de nível de compatibilidade 100 ou inferior|Configuração de nível de compatibilidade 110, no mínimo|  
|--------------------------------------------------|--------------------------------------------------|  
|São executados objetos de banco de dados de CLR (Common Language Runtime) com a versão 4 do CLR. Porém, são evitadas algumas alterações de comportamento apresentadas na versão 4 do CLR. Para obter mais informações, consulte [Novidades da integração CLR](../../relational-databases/clr-integration/clr-integration-what-s-new.md).|São executados objetos de banco de dados de CLR com a versão 4 do CLR.|  
|As funções XQuery **comprimento de cadeia de caracteres** e **subcadeia de caracteres** contam cada substituto como dois caracteres.|As funções XQuery **comprimento de cadeia de caracteres** e **subcadeia de caracteres** contam cada substituto como um caractere.|  
|PIVOT é permitido em uma consulta CTE (common table expression, expressão de tabela comum) recursiva. No entanto, a consulta retorna resultados incorretos quando há várias linhas por agrupamento.|PIVOT não é permitido em uma consulta CTE recursiva. Um erro é retornado.|  
|O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Em [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], material criptografado com RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.|Novo material não pode ser criptografado com RC4 ou RC4_128. Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. Em [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], material criptografado com RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.|  
|O estilo padrão de operações CAST e CONVERT nos **tempo** e **datetime2** tipos de dados é 121, exceto quando o tipo é usado em uma expressão de coluna computada. Para colunas computadas, o estilo padrão é 0. Esse comportamento afeta as colunas computadas quando são criadas, usadas em consultas que envolvam parametrização automática ou usadas em definições de restrição.<br /><br /> O exemplo D na seção exemplos abaixo mostra a diferença entre os estilos 0 e 121. Não demonstra o comportamento descrito acima. Para obter mais informações sobre estilos de data e hora, consulte [CAST e CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).|No nível de compatibilidade 110, o estilo padrão de operações CAST e CONVERT em **tempo** e **datetime2** tipos de dados sempre é 121. Se a sua consulta depender do comportamento antigo, use um nível de compatibilidade inferior a 110 ou especifique explicitamente o estilo 0 na consulta afetada.<br /><br /> A atualização do banco de dados para o nível de compatibilidade 110 não alterará os dados de usuário que foram armazenados em disco. Você deve corrigir esses dados manualmente conforme apropriado. Por exemplo, se você usou SELECT INTO para criar uma tabela com base em uma fonte que continha uma expressão de coluna computada descrita acima, os dados (usando o estilo 0) serão armazenados, em vez da própria definição de coluna computada. Você precisará atualizar manualmente esses dados para que coincidam com o estilo 121.|  
|As colunas em tabelas remotas do tipo **smalldatetime** referenciadas em uma exibição particionada são mapeadas como **datetime**. Colunas correspondentes nas tabelas locais (na mesma posição ordinal na lista de seleção) devem ser do tipo **datetime**.|As colunas em tabelas remotas do tipo **smalldatetime** referenciadas em uma exibição particionada são mapeadas como **smalldatetime**. Colunas correspondentes nas tabelas locais (na mesma posição ordinal na lista de seleção) devem ser do tipo **smalldatetime**.<br /><br /> Depois de atualizar para 110, a exibição particionada distribuída falhará devido à incompatibilidade de tipo de dados. Você pode resolver isso alterando o tipo de dados na tabela remota para **datetime** ou definindo a compatibilidade de nível de banco de dados local para 100 ou inferior.|  
|A função SOUNDEX implementa as seguintes regras:<br /><br /> 1)-maiuscula H ou W maiusculo são ignorados ao separar duas consoantes que tenham o mesmo número no código SOUNDEX.<br /><br /> 2) se os 2 primeiros caracteres do *character_expression* têm o mesmo número no código SOUNDEX, ambos os caracteres são incluídos. Além de isso, se um conjunto de consoantes lado a lado tiver o mesmo número no código SOUNDEX, todas as consoantes serão excluídas, exceto a primeira.|A função SOUNDEX implementa as seguintes regras:<br /><br /> 1) se maiusculas H ou W maiusculo separar duas consoantes que tenham o mesmo número no código SOUNDEX, a consoante à direita será ignorada<br /><br /> 2) se um conjunto de consoantes lado a lado tiver o mesmo número no código SOUNDEX, todas elas serão excluídas, exceto o primeiro.<br /><br /> <br /><br /> As regras adicionais podem fazer com que os valores computados pela função SOUNDEX sejam diferentes dos valores computados sob os níveis de compatibilidade anteriores. Após a atualização para o nível de compatibilidade 110, talvez seja necessário recriar os índices, os heaps ou as restrições CHECK que usam a função SOUNDEX. Para obter mais informações, consulte [SOUNDEX &#40; Transact-SQL &#41;](../../t-sql/functions/soundex-transact-sql.md)|  
  
## <a name="differences-between-compatibility-level-90-and-level-100"></a>Diferenças entre os níveis de compatibilidade 90 e 100  
 Esta seção descreve os novos comportamentos apresentados com o nível de compatibilidade 100.  
  
|Configuração de nível de compatibilidade 90|Configuração de nível de compatibilidade 100|Possibilidade de impacto|  
|----------------------------------------|-----------------------------------------|---------------------------|  
|A configuração QUOTED_IDENTIFER sempre é definida como ON para funções com valor de tabela de várias instruções ao serem criadas, sem considerar a configuração do nível de sessão.|A configuração de sessão QUOTED IDENTIFIER é atendida quando funções com valor de tabela de várias instruções são criadas.|Média|  
|Quando você cria ou altera uma função de partição, **datetime** e **smalldatetime** literais na função são avaliados assumindo US_English como a configuração de idioma.|A configuração de idioma atual é usada para avaliar **datetime** e **smalldatetime** literais na função de partição.|Média|  
|A cláusula FOR BROWSE é permitida (e ignorada) nas instruções INSERT e SELECT INTO.|A cláusula FOR BROWSE não é permitida em instruções INSERT SELECT INTO.|Média|  
|Predicados de texto completo são permitidos na cláusula OUTPUT.|Predicados de texto completo não são permitidos na cláusula OUTPUT.|Baixa|  
|CREATE FULLTEXT STOPLIST, ALTER FULLTEXT STOPLIST e DROP FULLTEXT STOPLIST não recebem suporte. A lista de palavras irrelevantes do sistema é associada automaticamente a novos índices de texto completo.|CREATE FULLTEXT STOPLIST, ALTER FULLTEXT STOPLIST e DROP FULLTEXT STOPLIST recebem suporte.|Baixa|  
|MERGE não é imposto como uma palavra-chave reservada.|MERGE é uma palavra-chave completamente reservada. A instrução MERGE é suportadas nos níveis de compatibilidade 100 e 90.|Baixa|  
|Usando o \<dml_table_source > argumento da instrução INSERT gera um erro de sintaxe.|Além disso, você pode capturar os resultados de uma cláusula OUTPUT em uma instrução INSERT, UPDATE, DELETE ou MERGE aninhada e inserir esses resultados em uma tabela ou exibição de destino. Isso é feito usando o \<dml_table_source > argumento da instrução INSERT.|Baixa|
|A menos que NOINDEX esteja especificado, DBCC CHECKDB ou DBCC CHECKTABLE executará verificações de consistência física e lógica em uma única tabela ou exibição indexada e em todos os índices não clusterizados e XML. Não há suporte para índices espaciais.|A menos que NOINDEX esteja especificado, DBCC CHECKDB ou DBCC CHECKTABLE executará verificações de consistência física e lógica em uma única tabela e em todos os índices não clusterizados. Entretanto, em índices XML, índices espaciais e exibições indexadas, por padrão são executadas somente as verificações de consistência física.<br /><br /> Se WITH EXTENDED_LOGICAL_CHECKS estiver especificado, verificações lógicas serão executadas em exibições indexadas, em índices XML e em índices espaciais, quando presentes. Por padrão, as verificações de consistência física são executadas antes das verificações de consistência lógica. Se NOINDEX também estiver especificado, apenas as verificações lógicas serão executadas.|Baixa|  
|Quando uma cláusula OUTPUT é usada com uma instrução DML que causa um erro de tempo de execução durante sua execução, a transação inteira é encerrada e revertida.|Quando uma cláusula OUTPUT é usada com uma instrução DML que causa um erro de tempo de execução durante sua execução, o comportamento depende da configuração em SET XACT_ABORT. Se SET XACT_ABORT estiver OFF, um erro de cancelamento de instrução gerado pela instrução DML usando a cláusula OUTPUT encerrará a instrução, mas a execução do lote continuará e a transação não será revertida. Se SET XACT_ABORT estiver como ON, todos os erros de tempo de execução gerados pela instrução DML usando a cláusula OUTPUT encerrarão o lote e a transação será revertida.|Baixa|  
|CUBE e ROLLUP não são impostos como palavras-chave reservadas.|CUBE e ROLLUP são palavras-chave reservadas dentro da cláusula GROUP BY.|Baixa|  
|A validação estrita é aplicada a elementos do XML **anyType** tipo.|Validação incerta é aplicada a elementos do **anyType** tipo. Para obter mais informações, consulte [componentes curinga e validação de conteúdo](../../relational-databases/xml/wildcard-components-and-content-validation.md).|Baixa|  
|Os atributos especiais **xsi: nil** e **xsi: Type** não pode ser consultada ou modificado por instruções de linguagem de manipulação de dados.<br /><br /> Isso significa que `/e/@xsi:nil` falhar ao `/e/@*` ignora o **xsi: nil** e **xsi: Type** atributos. No entanto, `/e` retorna o **xsi: nil** e **xsi: Type** atributos para manter a consistência com `SELECT xmlCol`, mesmo se `xsi:nil = "false"`.|Os atributos especiais **xsi: nil** e **xsi: Type** são armazenados como atributos normais e podem ser consultados e modificados.<br /><br /> Por exemplo, ao executar a consulta `SELECT x.query('a/b/@*')` retorna todos os atributos, incluindo **xsi: nil** e **xsi: Type**. Para excluir estes tipos de consulta, substitua `@*` com `@*[namespace-uri(.) != "` *insert xsi namespace uri* `"` e não `(local-name(.) = "type"` ou`local-name(.) ="nil".`|Baixa|  
|Uma função definida pelo usuário que converte um valor constante da cadeia de caracteres XML para um tipo de datetime do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é marcada como determinista.|Uma função definida pelo usuário que converte um valor constante de cadeia de caracteres XML em um tipo datetime do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é marcado como não determinista.|Baixa|  
|Os tipos de listas e união de XML não são totalmente suportados.|Os tipos de lista e união são totalmente suportados, inclusive as seguintes funcionalidades:<br /><br /> União de lista<br /><br /> União de união<br /><br /> Lista de tipos atômicos<br /><br /> Lista de união|Baixa|  
|As opções SET requeridas para um método xQuery não são validadas quando o método é contido em uma exibição ou função com valor de tabela embutida.|As opções SET requeridas para um método xQuery são validadas quando o método é contido em uma exibição ou função com valor de tabela embutida. Um erro ocorrerá se as opções SET do método forem definidas incorretamente.|Baixa|  
|Os valores do atributo XML que contém caracteres de final de linha (retorno de carro e alimentação de linha) não são normalizados de acordo com o padrão XML. Isto é, ambos os caracteres são retornados, em vez de um único caractere de alimentação de linha.|Os valores do atributo XML que contém caracteres de final de linha (retorno de carro e alimentação de linha) são normalizados de acordo com o padrão XML. Isto é, todas as quebras de linha em entidades externas de análise (incluindo a entidade do documento) são normalizadas na entrada pela tradução da sequência de dois caracteres #xD #xA e de qualquer #xD que não seja seguido por #xA em um único caractere #xA.<br /><br /> Aplicativos que usam atributos para transportar valores da cadeia de caracteres que contêm caracteres de final de linha não receberão de volta estes caracteres, já que eles foram submetidos. Para evitar o processo de normalização, use as entidades de caractere numérico XML para codificar todos os caracteres de final de linha.|Baixa|  
|As propriedades das colunas ROWGUIDCOL e IDENTITY podem ser nomeadas incorretamente como restrições. Por exemplo, a instrução `CREATE TABLE T (C1 int CONSTRAINT MyConstraint IDENTITY)` executa, mas o nome da restrição não é preservado e não fica acessível ao usuário.|As propriedades das colunas ROWGUIDCOL e IDENTITY não podem ser nomeadas como uma restrição. O erro 156 é retornado.|Baixa|  
|A atualização de colunas usando atribuição bidirecional, tal qual `UPDATE T1 SET @v = column_name = <expression>`, pode produzir resultados inesperados porque o valor de tempo de vida da variável pode ser usado em outras cláusulas, como nas cláusulas WHERE e ON, durante a execução de instruções, em vez do valor de início da instrução. Isto pode causar a alteração imprevisível dos significados dos predicados em uma base por linha.<br /><br /> Este comportamento só é aplicável quando o nível de compatibilidade é definido em 90.|A atualização de colunas usando uma atribuição bidirecional gera resultados esperados porque só o valor inicial da instrução é acessado durante a execução da instrução.|Baixa|  
|Consulte o exemplo E, na seção exemplos abaixo.|Consulte o exemplo F na seção exemplos abaixo.|Baixa|  
|A função ODBC {fn CONVERT()} usa o formato de data padrão do idioma. Em algumas linguagens, o formato padrão é YDM, que pode resultar em erros de conversão quando CONVERT() é combinado com outras funções, como {fn CURDATE()}, que espera um formato YMD.|A função ODBC {fn CONVERT()} usa o estilo 121 (um formato YMD independente de linguagem) ao converter os tipos de dados ODBC SQL_TIMESTAMP, SQL_DATE, SQL_TIME, SQLDATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP.|Baixa|  
|Datetime intrínseco, como DATEPART, não exige que os valores de entrada de cadeia de caracteres sejam literais válidas de datetime. Por exemplo, SELECT DATEPART (ano, ‘2007/05-30') compila com sucesso.|Datetime intrínseco, como DATEPART, exige que os valores de entrada de cadeia de caracteres sejam literais válidas de datetime. Erro 241 é retornado quando um datetime literal inválido é usado.|Baixa|  
  
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
  
 Se um aplicativo usar um identificador que é reservado como uma palavra-chave no seu nível de compatibilidade, o aplicativo falhará. Para resolver esse problema, coloque o identificador entre qualquer um dos colchetes (**[]**) ou aspas (**""**); por exemplo, para atualizar um aplicativo que usa o identificador **externo** para o nível de compatibilidade 90, você pode alterar o identificador para o **[EXTERNAL]** ou **"Externo"**.  
  
 Para obter mais informações, consulte [Palavras-chave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-compatibility-level"></a>A. Alterando o nível de compatibilidade  
 O exemplo a seguir altera o nível de compatibilidade de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] banco de dados `110,` [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
```tsql  
ALTER DATABASE AdventureWorks2012  
SET COMPATIBILITY_LEVEL = 110;  
GO  
```  
  
 O exemplo a seguir retorna o nível de compatibilidade do banco de dados atual.  
  
```tsql  
SELECT name, compatibility_level   
FROM sys.databases   
WHERE name = db_name();  
```  
  
### <a name="b-ignoring--the-set-language-statement-except-under-compatibility-level-120"></a>B. Ignorando a instrução SET LANGUAGE exceto no nível de compatibilidade 120  
 A consulta a seguir ignora a instrução SET LANGUAGE exceto no nível de compatibilidade 120.  
  
```tsql  
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
 Para a configuração de nível de compatibilidade de 110 ou inferior, as referências recursivas no lado direito de uma cláusula EXCEPT criam um loop infinito.  
  
```tsql  
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
 Este exemplo mostra a diferença entre os estilos 0 e 121. Para obter mais informações sobre estilos de data e hora, consulte [CAST e CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
```tsql  
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
  
```tsql  
ALTER DATABASE AdventureWorks2012  
SET compatibility_level = 90;  
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
  
```tsql  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM   
    (SELECT BusinessEntityID FROM HumanResources.Employee  
     UNION ALL  
     SELECT BusinessEntityID FROM HumanResources.EmployeeAddress) AS Test;  
SELECT @v;  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Palavras-chave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
  
  

