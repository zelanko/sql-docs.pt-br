---
title: Agrupamentos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COLLATE
- COLLATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], COLLATE clause
- COLLATE clause
ms.assetid: 76763ac8-3e0d-4bbb-aa53-f5e7da021daa
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5c9763da1ea1f9bb3e1e0d92ff02fbfa48a22c46
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33071623"
---
# <a name="collations"></a>Agrupamentos
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  É uma cláusula que pode ser aplicada a uma definição de banco de dados ou de coluna para definir o agrupamento ou a uma expressão de cadeia de caracteres ao aplicar uma conversão de agrupamento.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
COLLATE { <collation_name> | database_default }  
<collation_name> :: =   
     { Windows_collation_name } | { SQL_collation_name }  
```  
  
## <a name="arguments"></a>Argumentos  
 *collation_name*  
 É o nome do agrupamento a ser aplicado à expressão, definição de coluna ou de banco de dados. *collation_name* pode ser apenas um *Windows_collation_name* ou um *SQL_collation_name* especificado. *collation_name* deve ser um valor literal. *collation_name* não pode ser representado por uma variável ou expressão.  
  
 *Windows_collation_name* é o nome de agrupamento de um [Nome de Agrupamento do Windows](../../t-sql/statements/windows-collation-name-transact-sql.md).  
  
 *SQL_collation_name* é o nome de agrupamento de um [Nome de Agrupamento do SQL Server](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 Ao aplicar um agrupamento no nível de definição do banco de dados, não é possível usar agrupamentos do Windows somente Unicode com a cláusula COLLATE.  
  
 **database_default**  
 Faz com que a cláusula COLLATE herde o agrupamento do banco de dados atual.  
  
## <a name="remarks"></a>Remarks  
 A cláusula COLLATE pode ser especificada em vários níveis. Entre elas estão as seguintes:  
  
1.  Criando ou alterando um banco de dados.  
  
     É possível usar a cláusula COLLATE da instrução CREATE DATABASE ou ALTER DATABASE para especificar o agrupamento padrão do banco de dados. Também é possível especificar um agrupamento ao criar um banco de dados usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Se um agrupamento não for especificado, o banco de dados será atribuído ao agrupamento padrão da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    > [!NOTE]  
    >  Agrupamentos do Windows somente Unicode podem ser usados com a cláusula COLLATE somente para aplicar agrupamentos aos tipos de dados **nchar**, **nvarchar** e **ntext** em dados nos níveis de coluna e de expressão; não é possível usá-los com a cláusula COLLATE para alterar o agrupamento de uma instância de banco de dados ou de servidor.  
  
2.  Criando ou alterando uma coluna de tabela.  
  
     Você pode especificar agrupamentos para cada coluna de cadeia de caracteres usando a cláusula COLLATE da instrução CREATE TABLE ou ALTER TABLE. Também é possível especificar um agrupamento ao criar uma tabela usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Se um agrupamento não for especificado, a coluna será atribuída ao agrupamento padrão do banco de dados.  
  
     Também é possível usar a opção `database_default` na cláusula COLLATE para especificar que uma coluna de uma tabela temporária usa o padrão de agrupamento do banco de dados de usuário atual para a conexão em vez de **tempdb**.  
  
3.  Convertendo o agrupamento de uma expressão.  
  
     Você pode usar a cláusula COLLATE para aplicar uma expressão de caractere a um determinado agrupamento. Literais de caracteres e variáveis são atribuídos ao agrupamento padrão do banco de dados atual. Referências de coluna são atribuídas ao agrupamento de definição da coluna.  
  
 O agrupamento de um identificador depende do nível em que está definido. Os identificadores de objetos no nível de instância, como logons e nomes de banco de dados, são atribuídos ao agrupamento padrão da instância. Os identificadores de objetos em um banco de dados, como tabelas, exibições e nomes de coluna, são atribuídos ao agrupamento padrão do banco de dados. Por exemplo, duas tabelas com nomes que diferem apenas em maiúsculas e minúsculas podem ser criadas em um banco de dados que possui agrupamento que diferencia maiúsculas e minúsculas, mas não podem ser criadas em um banco de dados com um agrupamento que não faz essa diferenciação. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
 Variáveis, rótulos GOTO, procedimentos armazenados temporários e tabelas temporárias podem ser criados quando o contexto de conexão é associado a um banco de dados e, em seguida, referenciado quando o contexto é alternado para outro banco de dados. Os identificadores para variáveis, os rótulos GOTO, os procedimentos armazenados temporários e as tabelas temporárias estão no agrupamento padrão da instância de servidor.  
  
 A cláusula COLLATE pode ser aplicada apenas aos tipos de dados **char**, **varchar**, **text**, **nchar**, **nvarchar** e **ntext**.  
  
 COLLATE usa *collate_name* para referenciar o nome do agrupamento do SQL Server ou do Windows a ser aplicado à expressão, definição de coluna ou definição de banco de dados. *collation_name* pode ser somente um *Windows_collation_name* ou *SQL_collation_name* especificado e o parâmetro deve conter um valor literal. *collation_name* não pode ser representado por uma variável ou expressão.  
  
 Geralmente, os agrupamentos são identificados por um nome de agrupamento, exceto na Instalação. Na Instalação, especifique o designador de agrupamento raiz (a localidade do agrupamento) para agrupamentos do Windows e, em seguida, especifique opções de classificação que diferenciam ou não maiúsculas e minúsculas ou caracteres com ou sem acentos.  
  
 Execute a função do sistema [fn_helpcollations](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) para recuperar uma lista de todos os nomes de agrupamentos válidos para agrupamentos do Windows e SQL Server:  
  
```sql  
SELECT name, description  
FROM fn_helpcollations();  
```  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] só pode aceitar páginas de código que tenham suporte no sistema operacional subjacente. Quando você executa uma ação que depende de agrupamentos, o agrupamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado pelo objeto referenciado deve usar uma página de código com suporte no sistema operacional executado no computador. Essas ações podem incluir o seguinte:  
  
-   Especificando um agrupamento padrão para um banco de dados ao criar ou alterar o banco de dados.  
  
-   Especificando um agrupamento para uma coluna ao criar ou alterar uma tabela.  
  
-   Ao restaurar ou anexar um banco de dados, o agrupamento padrão do banco de dados e o agrupamento de qualquer coluna ou parâmetro **char**, **varchar** e **text** no banco de dados devem ser compatíveis com o sistema operacional.  
  
> [!NOTE]
> O agrupamento de servidor da Instância Gerenciada do Banco de Dados SQL do Azure é **SQL_Latin1_General_CP1_CI_AS** e não pode ser alterado.

> [!NOTE]
> Há suporte para conversões de página de código em tipos de dados **char** e **varchar**, mas não no tipo de dados **text**. A perda de dados durante traduções de página de código não é informada.  
  
> [!NOTE]
> Se o agrupamento especificado ou o agrupamento usado pelo objeto referenciado usar uma página de código não compatível com o Windows, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibirá um erro.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-specifying-collation-during-a-select"></a>A. Especificando o agrupamento durante uma seleção  
 O exemplo a seguir cria uma tabela simples e insere 4 linhas. Depois, o exemplo aplica dois agrupamentos ao selecionar dados da tabela, demonstrando como `Chiapas` é classificado de forma diferente.  
  
```sql  
CREATE TABLE Locations  
(Place varchar(15) NOT NULL);  
GO  
INSERT Locations(Place) VALUES ('Chiapas'),('Colima')  
                             , ('Cinco Rios'), ('California');  
GO  
--Apply an typical collation  
SELECT Place FROM Locations  
ORDER BY Place  
COLLATE Latin1_General_CS_AS_KS_WS ASC;  
GO  
-- Apply a Spanish collation  
SELECT Place FROM Locations  
ORDER BY Place  
COLLATE Traditional_Spanish_ci_ai ASC;  
GO  
```  

Estes são os resultados da primeira consulta.  
  
```
Place 
------------- 
California 
Chiapas 
Cinco Rios 
Colima
```  
  
Estes são os resultados da segunda consulta.  
 
```
Place 
------------- 
California 
Cinco Rios 
Colima 
Chiapas
```  
  
### <a name="b-additional-examples"></a>B. Exemplos adicionais  
 Para obter mais exemplos que usam **COLLATE**, consulte [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md#examples), exemplo **G. Criando um banco de dados e especificando um nome de agrupamento e opções** e [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md#alter_column), exemplo **V. Alterando um agrupamento de coluna**.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)    
 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)    
 [Precedência de agrupamento &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)     
 [Constants &#40;Transact-SQL&#41;](../../t-sql/data-types/constants-transact-sql.md)     
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)     
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)     
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)     
 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)     
  
  
