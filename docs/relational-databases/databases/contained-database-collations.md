---
title: Agrupamentos de banco de dados independentes | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: contained database, collations
ms.assetid: 4b44f6b9-2359-452f-8bb1-5520f2528483
caps.latest.revision: "12"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00a724d305e55a58b257b699f298cbd5044a3510
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="contained-database-collations"></a>Agrupamentos de banco de dados contidos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Várias propriedades afetam a ordem de classificação e a semântica de igualdade dos dados textuais, incluindo diferenciação de maiúsculas e minúsculas, a distinção de acentos e o idioma base sendo usado. Essas qualidades são demonstradas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pela escolha do agrupamento dos dados. Para obter uma discussão mais detalhada sobre os agrupamentos, consulte [Suporte a agrupamentos e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
 Os agrupamentos se aplicam não apenas aos dados armazenados nas tabelas de usuário, mas também a todo o texto tratado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluindo metadados, objetos temporários, nomes de variável etc. O tratamento deles varia nos bancos de dados dependentes e independentes. Essa alteração não afetará muitos usuários, mas ajuda a fornecer independência de instância e uniformidade. Mas isso também pode causar alguma confusão, bem como problemas em sessões que acessam bancos de dados contidos e não contidos.  
  
 Este tópico esclarece o conteúdo da alteração e examina algumas áreas onde a alteração pode causar problemas.  
  
## <a name="non-contained-databases"></a>Bancos de dados dependentes  
 Todos os bancos de dados têm um agrupamento padrão (que pode ser definido durante a criação ou alteração de um banco de dados. Esse agrupamento é usado para todos os metadados do banco de dados, bem como para o padrão de todas as colunas de cadeias de caracteres no banco de dados. Os usuários podem escolher um agrupamento diferente para qualquer coluna específica usando a cláusula **COLLATE** .  
  
### <a name="example-1"></a>Exemplo 1  
 Por exemplo, se estivéssemos trabalhando em Beijing, nós poderíamos usar um agrupamento chinês:  
  
```sql  
ALTER DATABASE MyDB COLLATE Chinese_Simplified_Pinyin_100_CI_AS;  
```  
  
 Agora, se criarmos uma coluna, seu agrupamento padrão será esse agrupamento chinês, mas podemos escolher outro se quisermos:  
  
```sql  
CREATE TABLE MyTable  
      (mycolumn1 nvarchar,  
      mycolumn2 nvarchar COLLATE Frisian_100_CS_AS);  
GO  
SELECT name, collation_name  
FROM sys.columns  
WHERE name LIKE 'mycolumn%' ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```sql  
name            collation_name  
--------------- ----------------------------------  
mycolumn1       Chinese_Simplified_Pinyin_100_CI_AS  
mycolumn2       Frisian_100_CS_AS  
```  
  
 Isso parece relativamente simples, mas vários problemas ocorrem. Como o agrupamento para uma coluna depende do banco de dados em que a tabela foi criada, surgem problemas com o uso de tabelas temporárias que são armazenadas em **tempdb**. O agrupamento de **tempdb** geralmente corresponde ao agrupamento da instância, que não precisa corresponder ao agrupamento de banco de dados.  
  
### <a name="example-2"></a>Exemplo 2  
 Por exemplo, considere o banco de dados (chinês) acima quando usado em uma instância com um agrupamento **Latin1_General** :  
  
```sql  
CREATE TABLE T1 (T1_txt nvarchar(max)) ;  
GO  
CREATE TABLE #T2 (T2_txt nvarchar(max)) ;  
GO  
```  
  
 À primeira vista, essas duas tabelas parecem ter o mesmo esquema, mas como os agrupamentos dos bancos de dados são diferentes, na verdade, os valores são incompatíveis:  
  
```  
SELECT T1_txt, T2_txt  
FROM T1   
JOIN #T2   
    ON T1.T1_txt = #T2.T2_txt  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 Msg 468, Nível 16, Estado 9, Linha 2  
  
 Não é possível resolver o conflito de agrupamento entre "Latin1_General_100_CI_AS_KS_WS_SC" e Chinese_Simplified_Pinyin_100_CI_AS" na operação de igualdade.  
  
 Podemos corrigir isso agrupando explicitamente a tabela temporária. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] torna isso um pouco mais fácil ao fornecer a palavra-chave **DATABASE_DEFAULT** para a cláusula **COLLATE** .  
  
```sql  
CREATE TABLE T1 (T1_txt nvarchar(max)) ;  
GO  
CREATE TABLE #T2 (T2_txt nvarchar(max) COLLATE DATABASE_DEFAULT);  
GO  
SELECT T1_txt, T2_txt  
FROM T1   
JOIN #T2   
    ON T1.T1_txt = #T2.T2_txt ;  
```  
  
 Agora, o processo é executado sem erros.  
  
 Também é possível observar o comportamento dependente de agrupamento com variáveis. Considere a seguinte função:  
  
```  
CREATE FUNCTION f(@x INT) RETURNS INT  
AS BEGIN   
      DECLARE @I INT = 1  
      DECLARE @İ INT = 2  
      RETURN @x * @i  
END;  
```  
  
 Essa é uma função bastante peculiar. Em um agrupamento com diferenciação de maiúsculas e minúsculas, o @i na cláusula de retorno não pode ser associado a @I ou @İ. Em um agrupamento Latin1_General sem diferenciação de maiúsculas e minúsculas, @i é associado a @I e a função retorna 1. Mas em um agrupamento turco sem diferenciação de maiúsculas e minúsculas, @i é associado a @i e a função retorna 2. Isso pode causar confusão em um banco de dados que se move entre instâncias com agrupamentos diferentes.  
  
## <a name="contained-databases"></a>Bancos de dados independentes  
 Como um objetivo de design dos bancos de dados independentes é torná-los autocontidos, a dependência na instância e nos agrupamentos **tempdb** deve ser removida. Para isso, os bancos de dados independentes apresentam o conceito de agrupamento de catálogo. O agrupamento de catálogo é usado para metadados de sistema e objetos transitórios. Os detalhes são fornecidos abaixo.  
  
 Em um banco de dados independente, o agrupamento de catálogo **Latin1_General_100_CI_AS_WS_KS_SC**. Esse agrupamento é o mesmo para todos os bancos de dados independentes em todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e não pode ser alterado.  
  
 O agrupamento de banco de dados é mantido, mas é usado somente como o agrupamento padrão para dados de usuário. Por padrão, o agrupamento de banco de dados é igual ao agrupamento de modelo de banco de dados, mas pode ser alterado pelo usuário por meio de um comando **CREATE** ou **ALTER DATABASE** , como com bancos de dados dependentes.  
  
 Uma nova palavra-chave, **CATALOG_DEFAULT**, está disponível na cláusula **COLLATE** . Ela é usada como um atalho para o agrupamento atual de metadados em bancos de dados contidos e não contidos. Isto é, em um banco de dados não contido, **CATALOG_DEFAULT** retornará o agrupamento de banco de dados atual, pois os metadados são agrupados no agrupamento de banco de dados. Em um banco de dados contido, esses valores podem ser diferentes, pois o usuário pode alterar o agrupamento do banco de dados para que ele não corresponda ao agrupamento de catálogo.  
  
 O comportamento de vários objetos nos bancos de dados contidos e não contidos é resumido nesta tabela:  
  
||||  
|-|-|-|  
|**Item**|**Banco de dados não contido**|**Banco de dados contido**|  
|Dados de usuário (padrão)|DATABASE_DEFAULT|DATABASE_DEFAULT|  
|Dados temp (padrão)|Agrupamento TempDB|DATABASE_DEFAULT|  
|Metadados|DATABASE_DEFAULT / CATALOG_DEFAULT|CATALOG_DEFAULT|  
|Metadados temporários|Agrupamento TempDB|CATALOG_DEFAULT|  
|Variáveis|Agrupamento de instância|CATALOG_DEFAULT|  
|Rótulos Goto|Agrupamento de instância|CATALOG_DEFAULT|  
|Nomes de cursor|Agrupamento de instância|CATALOG_DEFAULT|  
  
 No exemplo de tabela temp descrito anteriormente, podemos ver que esse comportamento de agrupamento elimina a necessidade de uma cláusula **COLLATE** explícita na maioria dos usos da tabela temp. Em um banco de dados contido, esse código agora é executado sem erro, mesmo que os agrupamentos de banco de dados e de instância sejam diferentes:  
  
```sql  
CREATE TABLE T1 (T1_txt nvarchar(max)) ;  
GO  
CREATE TABLE #T2 (T2_txt nvarchar(max));  
GO  
SELECT T1_txt, T2_txt  
FROM T1   
JOIN #T2   
    ON T1.T1_txt = #T2.T2_txt ;  
```  
  
 Isso funciona porque `T1_txt` e `T2_txt` são coletados no agrupamento de banco de dados contido.  
  
## <a name="crossing-between-contained-and-uncontained-contexts"></a>Cruzando entre contextos contidos e não contidos  
 Desde que uma sessão em um banco de dados contido permaneça contida, ela deve permanecer no banco de dados ao qual está conectada. Nesse caso, o comportamento é muito simples. Mas se uma sessão cruzar entre contextos contidos e não contidos, o comportamento se tornará mais complexo, pois os dois conjuntos de regras deverão ser ligados. Isso pode ocorrer em um banco de dados parcialmente contido, pois um usuário pode utilizar **USE** para outro banco de dados. Nesse caso, a diferença nas regras de agrupamento é tratada pelo princípio a seguir.  
  
-   O comportamento de agrupamento para um lote é determinado pelo banco de dados no qual o lote começa.  
  
 Observe que essa decisão é tomada antes da emissão de qualquer comando, inclusive um **USE**inicial. Ou seja, se um lote começar em um banco de dados independente, mas se o primeiro comando for um **USE** para um banco de dados dependente, o comportamento do agrupamento independente ainda será usado para o lote. Dito isto, uma referência para uma variável, por exemplo, pode ter vários possíveis resultados:  
  
-   A referência pode localizar uma correspondência exatamente. Nesse caso, a referência funcionará sem erro.  
  
-   A referência pode não localizar uma correspondência no agrupamento atual onde antes havia uma. Isso gerará um erro que indica que a variável não existe, embora ela tenha sido criada aparentemente.  
  
-   A referência pode localizar várias correspondências que originalmente eram distintas. Isso também gerará um erro.  
  
 Isso será mostrado com alguns exemplos. Para eles, pressupomos que haja um banco de dados parcialmente independente denominado `MyCDB` com seu agrupamento de banco de dados definido como agrupamento padrão **Latin1_General_100_CI_AS_WS_KS_SC**. Pressupomos que o agrupamento de instância seja **Latin1_General_100_CS_AS_WS_KS_SC**. Os dois agrupamentos são distintos apenas na diferenciação de maiúsculas e minúsculas.  
  
### <a name="example-1"></a>Exemplo 1  
 O exemplo a seguir mostra o caso onde a referência localiza uma correspondência exata.  
  
```  
USE MyCDB;  
GO  
  
CREATE TABLE #a(x int);  
INSERT INTO #a VALUES(1);  
GO  
  
USE master;  
GO  
  
SELECT * FROM #a;  
GO  
  
Results:  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
x  
-----------  
1  
```  
  
 Nesse caso, o símbolo #a identificado é associado ao agrupamento de catálogo sem diferenciação de maiúsculas/minúsculas e o agrupamento de instância com diferenciação de maiúsculas/minúsculas, e o código funciona.  
  
### <a name="example-2"></a>Exemplo 2  
 O exemplo a seguir mostra o caso em que a referência não encontra uma correspondência no agrupamento atual, na qual havia uma antes.  
  
```  
USE MyCDB;  
GO  
  
CREATE TABLE #a(x int);  
INSERT INTO #A VALUES(1);  
GO  
```  
  
 Aqui, o #A é associado a #a no agrupamento padrão sem diferenciação de maiúsculas e minúsculas e a inserção funciona,  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
(1 row(s) affected)  
```  
  
 Mas se continuarmos o script...  
  
```  
USE master;  
GO  
  
SELECT * FROM #A;  
GO  
```  
  
 Receberemos um erro ao tentar associar ao #A no agrupamento de instância com diferenciação de maiúsculas e minúsculas;  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 Msg 208, Nível 16, Estado 0, Linha 2  
  
 Nome do objeto inválido '#A'.  
  
### <a name="example-3"></a>Exemplo 3  
 O exemplo a seguir demonstra o caso em que a referência localiza várias correspondências que eram originalmente distintas. Primeiro, começamos pelo **tempdb** (que tem o mesmo agrupamento com diferenciação de maiúsculas e minúsculas da nossa instância) e executamos as instruções a seguir.  
  
```  
USE tempdb;  
GO  
  
CREATE TABLE #a(x int);  
GO  
CREATE TABLE #A(x int);  
GO  
INSERT INTO #a VALUES(1);  
GO  
INSERT INTO #A VALUES(2);  
GO  
```  
  
 Essa operação é bem-sucedida, pois as tabelas são distintas neste agrupamento:  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
(1 row(s) affected)  
(1 row(s) affected)  
```  
  
 Se entrarmos em nosso banco de dados contido, no entanto, descobriremos que não podemos mais associar a essas tabelas.  
  
```  
USE MyCDB;  
GO  
SELECT * FROM #a;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 Msg 12800, Nível 16, Estado 1, Linha 2  
  
 A referência ao nome da tabela temp '#a' é ambígua e não pode ser resolvida. Possíveis candidatos são '#a' e '#A'.  
  
## <a name="conclusion"></a>Conclusão  
 O comportamento de agrupamento de bancos de dados contidos é sutilmente diferente daquele em bancos de dados não contidos. Esse comportamento é geralmente benéfico, fornecendo independência de instância e simplicidade. Alguns usuários podem ter problemas, particularmente quando uma sessão acessa bancos de dados contidos e não contidos.  
  
## <a name="see-also"></a>Consulte Também  
 [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)  
  
  
