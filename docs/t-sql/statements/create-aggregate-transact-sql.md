---
title: "Criar agregação (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ad5cf36e97bf3903cc9d42ec5179de6375624f95
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-aggregate-transact-sql"></a>CREATE AGGREGATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma função de agregação definida pelo usuário, cuja implementação está definida em uma classe de um assembly no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Para que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] associe a função de agregação à sua implementação, o assembly do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que contém a implementação deverá primeiramente ser carregado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o uso de uma instrução CREATE ASSEMBLY.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
 **@***param_name*  
 Um ou mais parâmetros na agregação definida pelo usuário. O valor de um parâmetro deve ser fornecido pelo usuário quando a função de agregação é executada. Especifique um nome de parâmetro usando um sinal de "arroba" (**@**) como o primeiro caractere. O nome do parâmetro deve estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md). Os parâmetros são locais à função.  
  
 *system_scalar_type*  
 É qualquer um dos tipos de dados escalares de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conter o valor do parâmetro de entrada ou o valor de retorno. Todos os tipos de dados escalares podem ser usados como um parâmetro para uma agregação definida pelo usuário, exceto **texto**, **ntext**, e **imagem**. Tipos não escalares, como **cursor** e **tabela**, não pode ser especificado.  
  
 *udt_schema_name*  
 É o nome do esquema ao qual pertence o tipo de dado CLR definido pelo usuário. Se não for especificado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] referências *udt_type_name* na seguinte ordem:  
  
-   O namespace do tipo SQL nativo.  
  
-   O esquema padrão do usuário atual no banco de dados atual.  
  
-   O esquema **dbo** no banco de dados atual.  
  
 *udt_type_name*  
 É o nome de um tipo de dado CLR definido pelo usuário já criado no banco de dados atual. Se *udt_schema_name* não for especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supõe que o tipo pertence ao esquema do usuário atual.  
  
 *nome_do_assembly* [ **.** *class_name* ]  
 Especifica o assembly a ser associado à função de agregação definida pelo usuário e, opcionalmente, o nome do esquema ao qual pertence o assembly e o nome da classe no assembly que implementa a agregação definida pelo usuário. O assembly já deve ter sido criado no banco de dados usando uma instrução CREATE ASSEMBLY. *class_name* deve ser um válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador e corresponder ao nome de uma classe que existe no assembly. *class_name* pode ser um nome qualificado de namespace se a linguagem de programação usada para gravar a classe usar namespaces, tal como c#. Se *class_name* não for especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assume que é o mesmo que *aggregate_name*.  
  
## <a name="remarks"></a>Comentários  
 Por padrão, a capacidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em executar código CLR está desligada. Você pode criar, modificar e descartar objetos de banco de dados que referenciam módulos de código gerenciado, mas o código nesses módulos não será executado em uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a menos que o [opção clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) é habilitada usando [SP _ configurar](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 A classe do assembly referenciado no *nome_do_assembly* e seus métodos devem satisfazer todos os requisitos para implementar uma função de agregação definida pelo usuário em uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [agregações CLR definidas pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md).  
  
## <a name="permissions"></a>Permissões  
 Requer permissão CREATE AGGREGATE e também permissão REFERENCES no assembly que é especificado na cláusula EXTERNAL NAME.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir supõe que um aplicativo de exemplo StringUtilities.csproj é compilado. Para obter mais informações, consulte [exemplo de funções de utilitário de cadeia de caracteres](http://msdn.microsoft.com/library/9623013f-15f1-4614-8dac-1155e57c880c).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Remover agregação &#40; Transact-SQL &#41;](../../t-sql/statements/drop-aggregate-transact-sql.md)  
  
  

