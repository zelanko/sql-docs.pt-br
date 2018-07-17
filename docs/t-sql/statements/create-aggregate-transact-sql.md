---
title: CREATE AGGREGATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_AGGREGATE_TSQL
- CREATE AGGREGATE
- AGGREGATE_TSQL
- AGGREGATE
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE AGGREGATE statement
- aggregate functions [SQL Server], user-defined
- user-defined functions [CLR integration]
ms.assetid: 62eebc19-9f15-4245-94fa-b3fcd64a9d42
caps.latest.revision: 50
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 248fe1397de470076aa0060019d156ec0718ab2a
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37786957"
---
# <a name="create-aggregate-transact-sql"></a>CREATE AGGREGATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma função de agregação definida pelo usuário, cuja implementação está definida em uma classe de um assembly no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Para que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] associe a função de agregação à sua implementação, o assembly do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que contém a implementação deverá primeiramente ser carregado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o uso de uma instrução CREATE ASSEMBLY.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE AGGREGATE [ schema_name . ] aggregate_name  
        (@param_name <input_sqltype>   
        [ ,...n ] )  
RETURNS <return_sqltype>  
EXTERNAL NAME assembly_name [ .class_name ]  
  
<input_sqltype> ::=  
        system_scalar_type | { [ udt_schema_name. ] udt_type_name }  
  
<return_sqltype> ::=  
        system_scalar_type | { [ udt_schema_name. ] udt_type_name }  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 É o nome do esquema ao qual pertence a função de agregação definida pelo usuário.  
  
 *aggregate_name*  
 É o nome da função de agregação que você deseja criar.  
  
 **@** *param_name*  
 Um ou mais parâmetros na agregação definida pelo usuário. O valor de um parâmetro deve ser fornecido pelo usuário quando a função de agregação é executada. Especifique um nome de parâmetro usando um sinal de "arroba" (**@**) como o primeiro caractere. O nome do parâmetro precisa estar em conformidade com as regras para [identificadores](../../relational-databases/databases/database-identifiers.md). Os parâmetros são locais à função.  
  
 *system_scalar_type*  
 É qualquer um dos tipos de dados escalares de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conter o valor do parâmetro de entrada ou o valor de retorno. Todos os tipos de dados escalares podem ser usados como um parâmetro para uma agregação definida pelo usuário, exceto **text**, **ntext** e **image**. Os tipos não escalares, como **cursor** e **tabela**, não podem ser especificado.  
  
 *udt_schema_name*  
 É o nome do esquema ao qual pertence o tipo de dado CLR definido pelo usuário. Se não for especificado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] referenciará *udt_type_name* na seguinte ordem:  
  
-   O namespace do tipo SQL nativo.  
  
-   O esquema padrão do usuário atual no banco de dados atual.  
  
-   O esquema **dbo** no banco de dados atual.  
  
 *udt_type_name*  
 É o nome de um tipo de dado CLR definido pelo usuário já criado no banco de dados atual. Se *udt_schema_name* não for especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considerará que o tipo pertence ao esquema do usuário atual.  
  
 *assembly_name* [ **.***class_name* ]  
 Especifica o assembly a ser associado à função de agregação definida pelo usuário e, opcionalmente, o nome do esquema ao qual pertence o assembly e o nome da classe no assembly que implementa a agregação definida pelo usuário. O assembly já deve ter sido criado no banco de dados usando uma instrução CREATE ASSEMBLY. *class_name* precisa ser um identificador válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e corresponder ao nome de uma classe que exista no assembly. *class_name* poderá ser um nome qualificado de namespace se a linguagem de programação usada para escrever a classe usar namespaces, como C#. Se *class_name* não for especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assumirá que ele é o mesmo que *aggregate_name*.  
  
## <a name="remarks"></a>Remarks  
 Por padrão, a capacidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em executar código CLR está desligada. Você pode criar, modificar e descartar objetos de banco de dados que referenciam módulos de código gerenciado, mas o código nesses módulos não será executado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a menos que a [opção clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) seja habilitada usando [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 A classe do assembly referenciado em *assembly_name* e seus métodos devem atender a todos os requisitos para implementar uma função de agregação definida pelo usuário em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, confira [Agregações do CLR (Common Language Runtime) definidas pelo usuário ](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md).  
  
## <a name="permissions"></a>Permissões  
 Requer permissão CREATE AGGREGATE e também permissão REFERENCES no assembly que é especificado na cláusula EXTERNAL NAME.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir supõe que um aplicativo de exemplo StringUtilities.csproj é compilado. Para obter mais informações, confira [Exemplo de funções de utilitário de cadeia de caracteres](http://msdn.microsoft.com/library/9623013f-15f1-4614-8dac-1155e57c880c).  
  
 O exemplo cria a agregação `Concatenate`. Antes que a agregação seja criada, o assembly `StringUtilities.dll` é registrado no banco de dados local.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @SamplesPath nvarchar(1024)  
-- You may have to modify the value of the this variable if you have  
--installed the sample some location other than the default location.  
  
SELECT @SamplesPath = REPLACE(physical_name, 'Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\master.mdf', 'Microsoft SQL Server\130\Samples\Engine\Programmability\CLR\')   
     FROM master.sys.database_files   
     WHERE name = 'master';  
  
CREATE ASSEMBLY StringUtilities FROM @SamplesPath + 'StringUtilities\CS\StringUtilities\bin\debug\StringUtilities.dll'  
WITH PERMISSION_SET=SAFE;  
GO  
  
CREATE AGGREGATE Concatenate(@input nvarchar(4000))  
RETURNS nvarchar(4000)  
EXTERNAL NAME [StringUtilities].[Microsoft.Samples.SqlServer.Concatenate];  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DROP AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-aggregate-transact-sql.md)  
  
  
