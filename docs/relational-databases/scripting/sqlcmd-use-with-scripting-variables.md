---
title: Usar sqlcmd com variáveis de script | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- scripts [SQL Server], sqlcmd utility
- variables [SQL Server], scripts
- scripting variables [SQL Server]
- sqlcmd utility, scripts
- setvar command
ms.assetid: 793495ca-cfc9-498d-8276-c44a5d09a92c
caps.latest.revision: 47
author: mightypen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 50548a9c34ff3c55c22e5492b807e338bcd4ccc2
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/10/2018
---
# <a name="sqlcmd---use-with-scripting-variables"></a>sqlcmd – Usar com variáveis de script
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  As variáveis usadas em scripts normalmente são chamadas de variáveis de script. As variáveis de script habilitam um script ser usado em vários cenários. Por exemplo, se você desejar executar um script em vários servidores, em vez de modificar o script para cada servidor, pode usar uma variável de script para o nome do servidor. Alterando o nome do servidor fornecido para a variável de script, o mesmo script pode ser executado em diferentes servidores.  
  
 As variáveis de script podem ser definidas explicitamente usando o comando **setvar** , ou implicitamente, usando a opção **sqlcmd-v** .  
  
 Este tópico também inclui exemplos que definem variáveis ambientais no prompt de comando Cmd.exe usando **SET**.  
  
## <a name="setting-scripting-variables-by-using-the-setvar-command"></a>Definindo variáveis de script usando o comando setvar  
 O comando **setvar** é usado para definir variáveis de script. Variáveis definidas usando o comando **setvar** são armazenadas internamente. Variáveis de script não devem ser confundidas com variáveis de ambiente, que são definidas no prompt de comando usando **SET**. Se um script fizer referência a uma variável que não é uma variável de ambiente ou não foi definida usando **setvar**, uma mensagem de erro será retornada e a execução do script será interrompida. Para obter mais informações, veja a opção **-b** em [Utilitário sqlcmd](../../tools/sqlcmd-utility.md).  
  
## <a name="variable-precedence-low-to-high"></a>Precedência de variável (baixa para alta)  
 Se mais de um tipo de variável tiver o mesmo nome, a variável com precedência mais alta será usada.  
  
1.  Variáveis ambientais do nível de sistema  
  
2.  Variáveis ambientais do nível de usuário  
  
3.  Shell de comando (**SET X=Y**) definido no prompt de comando antes de iniciar o **sqlcmd**  
  
4.  **sqlcmd-v** X=Y  
  
5.  **:Setvar** X Y  
  
> [!NOTE]  
>  Para exibir as variáveis ambientais, no **Painel de Controle**, abra **Sistema**e clique na guia **Avançado** .  
  
## <a name="implicitly-setting-scripting-variables"></a>Definindo implicitamente variáveis de script  
 Ao iniciar o **sqlcmd** com uma opção que contém uma variável **sqlcmd** relacionada, a variável **sqlcmd** será implicitamente definida com o valor especificado com a opção. No exemplo a seguir, o `sqlcmd` é iniciado com a opção `-l` . Isto define implicitamente a variável SQLLOGINTIMEOUT.  
  
```
c:\> sqlcmd -l 60
```
 
Também é possível usar a opção **-v** para definir uma variável de script existente em um script. O script a seguir (o nome de arquivo é `testscript.sql`), `ColumnName` é uma variável de script.  
 
```
USE AdventureWorks2012;

SELECT x.$(ColumnName)
FROM Person.Person x
WHERE x.BusinessEntityID < 5;
```

Assim você pode especificar o nome da coluna que deseja que retorne usando a opção `-v` :  
 
```
sqlcmd -v ColumnName ="FirstName" -i c:\testscript.sql
```

Para retornar uma coluna diferente usando o mesmo script, altere o valor da variável de script `ColumnName` .  
  
```
sqlcmd -v ColumnName ="LastName" -i c:\testscript.sql
```

## <a name="guidelines-for-scripting-variable-names-and-values"></a>Diretrizes para nomes e valores de variáveis de script  
 Considere as seguintes diretrizes ao nomear variáveis de script:  
  
-   Os nomes das variáveis não devem conter caracteres de espaços em brancos ou aspas.  
  
-   Os nomes das variáveis não devem ter a mesma forma que uma expressão variável, como *$(var)*.  
  
-   Variáveis de script não diferenciam maiúsculas de minúsculas.  
  
    > [!NOTE]  
    >  Se nenhum valor for atribuído a uma variável de ambiente **sqlcmd** , a variável será removida. Usar **:setvar VarName** sem um valor limpa a variável.  
  
 Considere as seguintes diretrizes ao especificar valores para variáveis de script:  
  
-   Valores de variáveis definidos usando **setvar** ou a opção **-v** deverão ser mantidos entre aspas se o valor da cadeia contiver espaços.  
  
-   Se houver aspas no valor da variável, elas devem ser substituídas. Por exemplo:`setvar MyVar "spac""e"`.  
  
## <a name="guidelines-for-cmdexe-set-variable-values-and-names"></a>Diretrizes para nomes e valores da variável SET de Cmd.exe  
 Variáveis definidas usando SET fazem parte do ambiente de Cmd.exe e podem ser referenciadas por **sqlcmd**. Considere as seguintes diretrizes:  
  
-   Os nomes das variáveis não devem conter caracteres de espaços em brancos ou aspas.  
  
-   Valores de variáveis podem conter espaços ou aspas.  
  
## <a name="sqlcmd-scripting-variables"></a>Variáveis de script do sqlcmd  
 Variáveis definidas por **sqlcmd** são conhecidas como variáveis de script. A tabela a seguir lista variáveis de script do **sqlcmd** .  
  
|        Variável         | Opção relacionada | R/W |         Default         |
| ----------------------- | -------------- | --- | ----------------------- |
| SQLCMDUSER*             | -U             | R   | ""                      |
| SQLCMDPASSWORD*         | -P             | --  | ""                      |
| SQLCMDSERVER*           | -S             | R   | "DefaultLocalInstance"  |
| SQLCMDWORKSTATION       | -H             | R   | "ComputerName"          |
| SQLCMDDBNAME            | -d             | R   | ""                      |
| SQLCMDLOGINTIMEOUT      | -l             | R/W | "8" (segundos)           |
| SQLCMDSTATTIMEOUT       | -t             | R/W | "0" = espere indefinidamente |
| SQLCMDHEADERS           | -H             | R/W | "0"                     |
| SQLCMDCOLSEP            | -S             | R/W | " ."                     |
| SQLCMDCOLWIDTH          | -w             | R/W | "0"                     |
| SQLCMDPACKETSIZE        | -A             | R   | "4096"                  |
| SQLCMDERRORLEVEL        | -M             | R/W | "0"                     |
| SQLCMDMAXVARTYPEWIDTH   | -y             | R/W | "256"                   |
| SQLCMDMAXFIXEDTYPEWIDTH | -y             | R/W | "0" = ilimitado         |
| SQLCMDEDITOR            |                | R/W | "edit.com"              |
| SQLCMDINI               |                | R   | ""                      |

SQLCMDUSER, SQLCMDPASSWORD e SQLCMDSERVER são definidos ao usar **:Connect** .  

R indica que o valor pode ser definido apenas uma vez durante a inicialização do programa.  
  
R/W indica que o valor pode ser redefinido usando o comando **setvar** e que comandos subsequentes usarão o novo valor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-the-setvar-command-in-a-script"></a>A. Usando o comando setvar em um script  
 Muitas opções do **sqlcmd** podem ser controladas em um script usando o comando **setvar** . No exemplo a seguir, o script `test.sql` é criado e nele a variável `SQLCMDLOGINTIMEOUT` é definida como `60` segundos e outra variável de script, `server`, é definida como `testserver`. O código a seguir está em `test.sql`.  

```
:setvar SQLCMDLOGINTIMEOUT 60
:setvar server "testserver"
:connect $(server) -l $(SQLCMDLOGINTIMEOUT)

USE AdventureWorks2012;

SELECT FirstName, LastName
FROM Person.Person;
```

O script é então chamado usando o sqlcmd:

```
sqlcmd -i c:\test.sql
```
  
### <a name="b-using-the-setvar-command-interactively"></a>B. Usando interativamente o comando setvar  
 O exemplo a seguir mostra como definir interativamente uma variável de script usando o comando `setvar` .  

```
sqlcmd
:setvar  MYDATABASE AdventureWorks2012
USE $(MYDATABASE);
GO
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Changed database context to 'AdventureWorks2012'
1>
```
  
### <a name="c-using-command-prompt-environment-variables-within-sqlcmd"></a>C. Usando variáveis de ambiente de prompt de comando no sqlcmd  
 No exemplo a seguir, quatro variáveis de ambiente `are` são definidas e depois chamadas a partir do `sqlcmd`.  

```
C:\>SET tablename=Person.Person
C:\>SET col1=FirstName
C:\>SET col2=LastName
C:\>SET title=Ms.
C:\>sqlcmd -d AdventureWorks2012
1> SELECT TOP 5 $(col1) + ' ' + $(col2) AS Name
2> FROM $(tablename)
3> WHERE Title ='$(title)'
4> GO
```
  
### <a name="d-using-user-level-environment-variables-within-sqlcmd"></a>D. Usando variáveis de ambiente em nível de usuário no sqlcmd  
 No exemplo a seguir, a variável de ambiente de nível de usuário `%Temp%` está definida no prompt de comando e foi passada para o arquivo de entrada do `sqlcmd` . Para obter a variável de ambiente de nível de usuário: em **Painel de Controle**, clique duas vezes em **Sistema**. Clique na guia **Avançado** e em **Variáveis de Ambiente**.  
  
 O código a seguir está no arquivo de entrada `c:\testscript.txt`:

```
:OUT $(MyTempDirectory)
USE AdventureWorks2012;

SELECT FirstName
FROM AdventureWorks2012.Person.Person
WHERE BusinessEntityID` `< 5;
```

O código a seguir é inserido no prompt de comando:

```
C:\ >SET MyTempDirectory=%Temp%\output.txt
C:\ >sqlcmd -i C:\testscript.txt
```

 O resultado a seguir é enviado ao arquivo de saída C:\Documents and Settings\\<user\>\Local Settings\Temp\output.txt.  

```
Changed database context to 'AdventureWorks2012'.
FirstName
--------------------------------------------------
Gustavo
Catherine
Kim
Humberto

(4 rows affected)
```

### <a name="e-using-a-startup-script"></a>E. Usando um script de inicialização  
 Um script de inicialização **sqlcmd** é executado quando **sqlcmd** é iniciado. O exemplo a seguir define a variável de ambiente de `SQLCMDINI`. Este é o conteúdo de `init.sql.`  

```
SET NOCOUNT ON
GO

DECLARE @nt_username nvarchar(128)
SET @nt_username = (SELECT rtrim(convert(nvarchar(128), nt_username))
FROM sys.dm_exec_sessions WHERE spid = @@SPID)
SELECT  @nt_username + ' is connected to ' +
rtrim(CONVERT(nvarchar(20), SERVERPROPERTY('servername'))) +
' (' +`  
rtrim(CONVERT(nvarchar(20), SERVERPROPERTY('productversion'))) +
')'
:setvar SQLCMDMAXFIXEDTYPEWIDTH 100
SET NOCOUNT OFF
GO

:setvar SQLCMDMAXFIXEDTYPEWIDTH
```

 Isto chama o arquivo `init.sql` quando o `sqlcmd` é iniciado.  
  
```
c:\> SET sqlcmdini=c:\init.sql
>1 Sqlcmd
```

 Esta é a saída.  

```
>1 < user > is connected to < server > (9.00.2047.00)
```

  
> [!NOTE]  
>  A opção **-X** desabilita o recurso de script de inicialização.  
  
### <a name="f-variable-expansion"></a>F. Expansão de variável  
 O exemplo a seguir mostra o trabalho com dados no formato de uma variável **sqlcmd** .  

```
USE AdventureWorks2012;
CREATE TABLE AdventureWorks2012.dbo.VariableTest
(
Col1 nvarchar(50)
);
GO
```

 Insira uma linha em `Col1` de `dbo.VariableTest` que contém o valor `$(tablename)`.  

```
INSERT INTO AdventureWorks2012.dbo.VariableTest(Col1)
VALUES('$(tablename)');
GO
```
  
 No prompt do `sqlcmd` , quando nenhuma variável for definida igual a `$(tablename)`, as instruções a seguir retornarão a linha.  
  
```
C:\> sqlcmd
>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = '$(tablename)';
>2 GO
>3 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = N'$(tablename)';
>4 GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```
>1 Col1
>2 ------------------
>3 $(tablename)
>4
>5 (1 rows affected)
```

 Dado que a variável `MyVar` foi definida como `$(tablename)`.  

```
>6 :setvar MyVar $(tablename)
```

 Estas instruções retornam a linha e também a mensagem "variável de script 'tablename' não definida".  

```
>6 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = '$(tablename)';
>7 GO

>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = N'$(tablename)';
>2 GO
```

 Estas instruções retornam a linha.  

```
>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = '$(MyVar)';
>2 GO
```

```
>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = N'$(MyVar)';
>2 GO
```
  
## <a name="see-also"></a>Consulte também  
 [Usar o utilitário sqlcmd](../../relational-databases/scripting/sqlcmd-use-the-utility.md)   
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)   
 [Referência de utilitários de prompt de comando &#40;Mecanismo de Banco de Dados&#41;](../../tools/command-prompt-utility-reference-database-engine.md)  
  
  
