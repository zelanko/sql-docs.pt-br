---
title: Injeção de SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: security, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Injection
ms.assetid: eb507065-ac58-4f18-8601-e5b7f44213ab
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b7ca69386615c8f9af55955f47071c1b93d122e6
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43080739"
---
# <a name="sql-injection"></a>Injeção SQL
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Injeção SQL é um ataque no qual um código mal-intencionado é inserido em cadeias de caracteres que são passadas posteriormente para uma instância do SQL Server para análise e execução. Qualquer procedimento que construa instruções SQL deve ser verificado quanto a vulnerabilidades de injeção porque o SQL Server executará todas as consultas sintaticamente válidas que receber. Mesmo dados com parâmetros podem ser manipulados por um invasor qualificado e determinado.  
  
## <a name="how-sql-injection-works"></a>Como funciona a injeção de SQL  
 A forma principal de injeção SQL consiste em inserção direta de código em variáveis de entrada de usuário, concatenadas com comandos SQL e executadas. Um ataque menos direto injeta código mal-intencionado em cadeias de caracteres destinadas a armazenamento em uma tabela ou como metadados. Quando as cadeias de caracteres armazenadas são concatenadas subsequentemente em um comando SQL dinâmico, o código mal-intencionado é executado.  
  
 O processo de injeção funciona encerrando prematuramente uma cadeia de caracteres de texto e anexando um novo comando. Como o comando inserido pode ter cadeias de caracteres adicionais anexadas a ele antes de ser executado, o malfeitor encerra a cadeia de caracteres injetada com uma marca de comentário "--". O texto subsequente é ignorado no momento da execução.  
  
 O script a seguir mostra uma injeção SQL simples. O script cria uma consulta SQL concatenando cadeias de caracteres codificadas com uma cadeia de caracteres inserida pelo usuário:  
  
```  
var Shipcity;  
ShipCity = Request.form ("ShipCity");  
var sql = "select * from OrdersTable where ShipCity = '" + ShipCity + "'";  
```  
  
 O usuário é solicitado a inserir o nome de uma cidade. Se ele inserir `Redmond`, a consulta criada pelo script terá a seguinte aparência:  
  
```  
SELECT * FROM OrdersTable WHERE ShipCity = 'Redmond'  
```  
  
 No entanto, suponha que o usuário insira o seguinte:  
  
```  
Redmond'; drop table OrdersTable--  
```  
  
 Nesse caso, a seguinte consulta é gerada pelo script:  
  
```  
SELECT * FROM OrdersTable WHERE ShipCity = 'Redmond';drop table OrdersTable--'  
```  
  
 O ponto-e-vírgula (;) denota o término de uma consulta e o início de outra. O hífen duplo (--) indica que o restante da linha atual é um comentário e deve ser ignorado. Se o código modificado estiver sintaticamente correto, será executado pelo servidor. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processar essa instrução, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selecionará primeiro todos os registros em `OrdersTable` onde `ShipCity` é `Redmond`. Em seguida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] descartará `OrdersTable`.  
  
 Contanto que o código SQL injetado esteja sintaticamente correto, a violação não poderá ser detectada programaticamente. Portanto, é necessário validar todas as entradas de usuário e verificar com cuidado o código que executa comandos SQL construídos no servidor que você está usando. Práticas recomendadas de codificação são descritas nas seções seguintes deste tópico.  
  
## <a name="validate-all-input"></a>Valide todas as entradas  
 Sempre valide entrada de usuário testando tipo, comprimento, formato e intervalo. Quando você estiver implementando precauções contra entrada mal-intencionada, considere os cenários de arquitetura e implantação de seu aplicativo. Lembre-se de que programas projetados para executar em um ambiente seguro podem ser copiados para um ambiente não seguro. As sugestões seguintes devem ser consideradas práticas recomendadas:  
  
-   Não faça suposições sobre o tamanho, o tipo ou o conteúdo dos dados recebidos pelo seu aplicativo. Por exemplo, você deve fazer a seguinte avaliação:  
  
    -   Como seu aplicativo se comportará se um usuário errôneo ou mal-intencionado inserir um arquivo MPEG de 10 megabytes onde seu aplicativo espera um código postal?  
  
    -   Como seu aplicativo se comportará se uma instrução `DROP TABLE` for inserida em um campo de texto?  
  
-   Teste o tamanho e tipo de dados de entrada e imponha limites apropriados. Isso pode ajudar a impedir excesso deliberado de buffer.  
  
-   Teste o conteúdo de variáveis de cadeia de caracteres e só aceite valores esperados. Rejeite entradas que contenham dados binários, sequências de escape e caracteres de comentário. Isso pode ajudar a impedir injeção de script e proteger contra explorações de excesso de buffer.  
  
-   Quando você estiver trabalhando com documentos XML, valide todos os dados em seu esquema à medida que são inseridos.  
  
-   Nunca construa instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] diretamente da entrada do usuário.  
  
-   Use procedimentos armazenados para validar entrada de usuário.  
  
-   Em ambientes de várias camadas, todos os dados devem ser validados antes de serem admitidos à zona de confiança. Os dados que não passam pelo processo de validação devem ser rejeitados e um erro deve ser retornado à camada anterior.  
  
-   Implemente várias camadas de validação. Precauções tomadas contra usuários casualmente mal-intencionados podem ser ineficazes contra determinados invasores. Uma prática mais recomendada é validar a entrada na interface do usuário e em todos os pontos subsequentes onde ele cruza um limite confiável.   
    Por exemplo, a validação de dados em um aplicativo cliente pode evitar injeção de script simples. No entanto, se a próxima camada assumir que sua entrada já foi validada, qualquer usuário mal-intencionado que possa contornar um cliente poderá ter acesso irrestrito ao sistema.  
  
-   Nunca concatene entrada de usuário que não seja validada. A concatenação de cadeia de caracteres é o ponto principal de entrada de injeção de script.  
  
-   Não aceite as seguintes cadeias de caracteres em campos dos quais nomes de arquivos podem ser construídos: AUX, CLOCK$, COM1 a COM8, CON, CONFIG$, LPT1 a LPT8, NUL e PRN.  
  
 Sempre que puder, rejeite entrada que contenha os caracteres a seguir.  
  
|Caractere de entrada|Significado em Transact-SQL|  
|---------------------|------------------------------|  
|**;**|Delimitador de consulta.|  
|**'**|Delimitador de cadeia de dados de caractere.|  
|**--**|Delimitador de cadeia de dados de caractere.<br />para obter informações sobre a ferramenta de configuração e recursos adicionais.|  
|**/\*** ... **\*/**|Delimitadores de comentário. Texto entre **/\*** e **\*/** não é avaliado pelo servidor.|  
|**xp_**|Usado no início do nome de procedimentos armazenados estendidos de catálogo, como `xp_cmdshell`.|  
  
### <a name="use-type-safe-sql-parameters"></a>Use parâmetros SQL de tipo seguro  
 A coleção **Parameters** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece verificação de tipo e validação de tamanho. Se você usar a coleção **Parameters** , a entrada será tratada como um valor literal e não como código executável. Um benefício adicional de usar a coleção **Parameters** é que você pode impor verificações de tipo e tamanho. Valores fora do intervalo irão disparar uma exceção. O seguinte fragmento de código mostra o uso da coleção **Parameters** :  
  
```  
SqlDataAdapter myCommand = new SqlDataAdapter("AuthorLogin", conn);  
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure;  
SqlParameter parm = myCommand.SelectCommand.Parameters.Add("@au_id",  
     SqlDbType.VarChar, 11);  
parm.Value = Login.Text;  
```  
  
 Nesse exemplo, o parâmetro `@au_id` é tratado como um valor literal e não como código executável. Esse valor é verificado quanto ao tipo e comprimento. Se o valor `@au_id` não estiver de acordo com o tipo especificado e as restrições de comprimento, uma exceção será gerada.  
  
### <a name="use-parameterized-input-with-stored-procedures"></a>Use entrada com parâmetros com procedimentos armazenados  
 Os procedimentos armazenados poderão ser suscetíveis a injeção SQL se usarem entrada não filtrada. Por exemplo, o código seguinte é vulnerável:  
  
```  
SqlDataAdapter myCommand =   
new SqlDataAdapter("LoginStoredProcedure '" +   
                               Login.Text + "'", conn);  
```  
  
 Se você usar procedimentos armazenados, deverá usar parâmetros como entrada.  
  
### <a name="use-the-parameters-collection-with-dynamic-sql"></a>Use coleção de parâmetros com SQL dinâmico  
 Se você não puder usar procedimentos armazenados, ainda poderá usar parâmetros, como mostrado no exemplo de código a seguir.  
  
```  
SqlDataAdapter myCommand = new SqlDataAdapter(  
"SELECT au_lname, au_fname FROM Authors WHERE au_id = @au_id", conn);  
SQLParameter parm = myCommand.SelectCommand.Parameters.Add("@au_id",   
                        SqlDbType.VarChar, 11);  
Parm.Value = Login.Text;  
```  
  
### <a name="filtering-input"></a>Filtrando a entrada  
 A filtragem de entrada também pode ser útil para proteger contra injeção de SQL, removendo caracteres de escape. Porém, por causa do número grande de caracteres que podem causar problemas, essa não é uma defesa confiável. O exemplo a seguir procura o delimitador de cadeia de caracteres.  
  
```  
private string SafeSqlLiteral(string inputSQL)  
{  
  return inputSQL.Replace("'", "''");  
}  
```  
  
### <a name="like-clauses"></a>Cláusulas LIKE  
 Observe que se você estiver usando uma cláusula `LIKE` , os caracteres curinga ainda deverão ter escape:  
  
```  
s = s.Replace("[", "[[]");  
s = s.Replace("%", "[%]");  
s = s.Replace("_", "[_]");  
```  
  
## <a name="reviewing-code-for-sql-injection"></a>Revisando código para injeção SQL  
 É necessário examinar todo o código que chama `EXECUTE`, `EXEC`ou `sp_executesql`. Você pode usar consultas semelhantes à que segue para ajudá-lo a identificar procedimentos que contenham essas instruções. Essa consulta verifica se existem 1, 2, 3 ou 4 espaços após as palavras `EXECUTE` ou `EXEC`.  
  
```  
SELECT object_Name(id) FROM syscomments  
WHERE UPPER(text) LIKE '%EXECUTE (%'  
OR UPPER(text) LIKE '%EXECUTE  (%'  
OR UPPER(text) LIKE '%EXECUTE   (%'  
OR UPPER(text) LIKE '%EXECUTE    (%'  
OR UPPER(text) LIKE '%EXEC (%'  
OR UPPER(text) LIKE '%EXEC  (%'  
OR UPPER(text) LIKE '%EXEC   (%'  
OR UPPER(text) LIKE '%EXEC    (%'  
OR UPPER(text) LIKE '%SP_EXECUTESQL%';  
```  
  
### <a name="wrapping-parameters-with-quotename-and-replace"></a>Envolvendo parâmetros com QUOTENAME () e REPLACE()  
 Em cada procedimento armazenado selecionado, verifique se todas as variáveis usadas no Transact-SQ dinâmico estão sendo tratadas corretamente. Dados oriundos de parâmetros de entrada de procedimento armazenado ou que são lidos de uma tabela devem ser envolvidos em QUOTENAME() ou REPLACE(). Lembre-se de que o valor de @variable que é passado para QUOTENAME() pertence a sysname e tem um comprimento máximo de 128 caracteres.  
  
|@variable|Invólucro recomendado|  
|---------------|-------------------------|  
|Nome de um protegível|`QUOTENAME(@variable)`|  
|Cadeia de caracteres de ≤ 128 caracteres|`QUOTENAME(@variable, '''')`|  
|Cadeia de caracteres de > 128 caracteres|`REPLACE(@variable,'''', '''''')`|  
  
 Quando você usa essa técnica, uma instrução SET pode ser examinada como segue:  
  
```  
--Before:  
SET @temp = N'SELECT * FROM authors WHERE au_lname ='''   
 + @au_lname + N'''';  
  
--After:  
SET @temp = N'SELECT * FROM authors WHERE au_lname = '''   
 + REPLACE(@au_lname,'''','''''') + N'''';  
```  
  
### <a name="injection-enabled-by-data-truncation"></a>Injeção habilitada por truncamento de dados  
 Qualquer [!INCLUDE[tsql](../../includes/tsql-md.md)] dinâmico atribuído a uma variável será truncado se for maior do que o buffer alocado para aquela variável. Um invasor que é capaz de impor truncamento de instrução ao passar cadeias de caracteres longas inesperadamente para um procedimento armazenado pode manipular o resultado. Por exemplo, o procedimento armazenado criado pelo script a seguir é vulnerável a injeção habilitada por truncamento.  
  
```  
CREATE PROCEDURE sp_MySetPassword  
@loginname sysname,  
@old sysname,  
@new sysname  
AS  
-- Declare variable.  
-- Note that the buffer here is only 200 characters long.   
DECLARE @command varchar(200)  
-- Construct the dynamic Transact-SQL.  
-- In the following statement, we need a total of 154 characters   
-- to set the password of 'sa'.   
-- 26 for UPDATE statement, 16 for WHERE clause, 4 for 'sa', and 2 for  
-- quotation marks surrounded by QUOTENAME(@loginname):  
-- 200 – 26 – 16 – 4 – 2 = 154.  
-- But because @new is declared as a sysname, this variable can only hold  
-- 128 characters.   
-- We can overcome this by passing some single quotation marks in @new.  
SET @command= 'update Users set password='   
    + QUOTENAME(@new, '''') + ' where username='   
    + QUOTENAME(@loginname, '''') + ' AND password = '   
    + QUOTENAME(@old, '''')  
  
-- Execute the command.  
EXEC (@command)  
GO  
```  
  
 Ao passar 154 caracteres para um buffer de 128 caracteres, um invasor pode definir uma nova senha para sa sem conhecer a senha antiga.  
  
```  
EXEC sp_MySetPassword 'sa', 'dummy',   
'123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012'''''''''''''''''''''''''''''''''''''''''''''''''''   
```  
  
 Por esse motivo, é necessário usar um buffer grande para uma variável de comando ou executar diretamente o [!INCLUDE[tsql](../../includes/tsql-md.md)] dinâmico na instrução `EXECUTE` .  
  
### <a name="truncation-when-quotenamevariable--and-replace-are-used"></a>Truncamento quando QUOTENAME(@variable, '''') e REPLACE() são usados  
 Cadeias de caracteres retornadas por QUOTENAME() e REPLACE() serão silenciosamente truncadas se ultrapassarem o espaço alocado. O procedimento armazenado criado nos exemplos a seguir mostram o que pode acontecer.  
  
```  
CREATE PROCEDURE sp_MySetPassword  
    @loginname sysname,  
    @old sysname,  
    @new sysname  
AS  
  
-- Declare variables.  
    DECLARE @login sysname  
    DECLARE @newpassword sysname  
    DECLARE @oldpassword sysname  
    DECLARE @command varchar(2000)  
  
-- In the following statements, the data stored in temp variables  
-- will be truncated because the buffer size of @login, @oldpassword,  
-- and @newpassword is only 128 characters, but QUOTENAME() can return  
-- up to 258 characters.  
    SET @login = QUOTENAME(@loginname, '''')  
    SET @oldpassword = QUOTENAME(@old, '''')  
    SET @newpassword = QUOTENAME(@new, '''')  
  
-- Construct the dynamic Transact-SQL.  
-- If @new contains 128 characters, then @newpassword will be '123... n  
-- where n is the 127th character.   
-- Because the string returned by QUOTENAME() will be truncated,   
-- it can be made to look like the following statement:  
-- UPDATE Users SET password ='1234. . .[127] WHERE username=' -- other stuff here  
    SET @command = 'UPDATE Users set password = ' + @newpassword   
     + ' where username =' + @login + ' AND password = ' + @oldpassword;  
  
-- Execute the command.  
EXEC (@command);  
GO  
```  
  
 Portanto, a instrução a seguir definirá as senhas de todos os usuários como o valor passado no código anterior  
  
```  
EXEC sp_MyProc '--', 'dummy', '12345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678'  
```  
  
 Você pode impor truncamento de cadeia de caracteres excedendo o espaço do buffer alocado ao usar REPLACE(). O procedimento armazenado criado nos exemplos a seguir mostram o que pode acontecer.  
  
```  
CREATE PROCEDURE sp_MySetPassword  
    @loginname sysname,  
    @old sysname,  
    @new sysname  
AS  
  
-- Declare variables.  
    DECLARE @login sysname  
    DECLARE @newpassword sysname  
    DECLARE @oldpassword sysname  
    DECLARE @command varchar(2000)  
  
-- In the following statements, data will be truncated because   
-- the buffers allocated for @login, @oldpassword and @newpassword   
-- can hold only 128 characters, but QUOTENAME() can return   
-- up to 258 characters.   
    SET @login = REPLACE(@loginname, '''', '''''')  
    SET @oldpassword = REPLACE(@old, '''', '''''')  
    SET @newpassword = REPLACE(@new, '''', '''''')  
  
-- Construct the dynamic Transact-SQL.  
-- If @new contains 128 characters, @newpassword will be '123...n   
-- where n is the 127th character.   
-- Because the string returned by QUOTENAME() will be truncated, it  
-- can be made to look like the following statement:  
-- UPDATE Users SET password='1234…[127] WHERE username=' -- other stuff here   
    SET @command= 'update Users set password = ''' + @newpassword + ''' where username='''   
     + @login + ''' AND password = ''' + @oldpassword + '''';  
  
-- Execute the command.  
EXEC (@command);  
GO  
```  
  
 Assim como acontece com QUOTENAME(), o truncamento da cadeia de caracteres por REPLACE() pode ser evitado declarando variáveis temporárias suficientemente grandes para todos os casos. Quando possível, você deve chamar QUOTENAME () ou REPLACE() diretamente dentro do [!INCLUDE[tsql](../../includes/tsql-md.md)]dinâmico. Caso contrário, você pode calcular o tamanho do buffer exigido como segue. Para `@outbuffer = QUOTENAME(@input)`, o tamanho de `@outbuffer` deve ser `2*(len(@input)+1)`. Quando você usa `REPLACE()` e aspas duplas, como no exemplo anterior, um buffer de `2*len(@input)` é suficiente.  
  
 O cálculo seguinte cobre todos os casos:  
  
```  
WHILE LEN(@find_string) > 0, required buffer size =  
ROUND(LEN(@input)/LEN(@find_string),0) * LEN(@new_string)   
 + (LEN(@input) % LEN(@find_string))  
```  
  
### <a name="truncation-when-quotenamevariable--is-used"></a>Truncamento quando QUOTENAME(@variable, ']') é usado  
 Pode ocorrer truncamento quando o nome de um protegível do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é passado a instruções que usam a forma `QUOTENAME(@variable, ']')`. O exemplo a seguir mostra a isso.  
  
```  
CREATE PROCEDURE sp_MyProc  
    @schemaname sysname,  
    @tablename sysname,  
AS  
  
-- Declare a variable as sysname. The variable will be 128 characters.  
-- But @objectname actually must allow for 2*258+1 characters.   
DECLARE @objectname sysname  
SET @objectname = QUOTENAME(@schemaname)+'.'+ QUOTENAME(@tablename)   
-- Do some operations.  
GO  
```  
  
 Quando você está concatenando valores do tipo sysname, deve usar variáveis temporárias suficientemente grandes para manter no máximo 128 caracteres por valor. Se possível, chame `QUOTENAME()` diretamente no [!INCLUDE[tsql](../../includes/tsql-md.md)]dinâmico. Caso contrário, você pode calcular o tamanho do buffer exigido como explicado na seção anterior.  
  
## <a name="see-also"></a>Consulte Também  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)   
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)   
 [sp_executesql &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md)   
 [Protegendo o SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
  
