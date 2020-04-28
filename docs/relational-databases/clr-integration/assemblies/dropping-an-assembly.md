---
title: Descartando um assembly | Microsoft Docs
description: Você pode excluir ou remover um assembly em SQL Server quando ele não for mais necessário. Use DROP ASSEMBLY para remover um assembly e seus arquivos associados.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- removing assemblies
- DROP ASSEMBLY statement
- assemblies [CLR integration], removing
- dropping assemblies
ms.assetid: 03481034-dc91-4488-ab24-ba44243e2690
author: rothja
ms.author: jroth
ms.openlocfilehash: 48fca2d5a255193800fed39e9869e1be231229a9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81485521"
---
# <a name="dropping-an-assembly"></a>Descartando um assembly
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os assemblies registrados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a instrução CREATE ASSEMBLY podem ser excluídos ou descartados quando a funcionalidade que fornecem deixa de ser necessária. O descarte de um assembly remove o mesmo e todos os seus arquivos associados como, por exemplo, arquivos de depuração, do banco de dados. Para descartar um assembly, use a instrução DROP ASSEMBLY com a seguinte sintaxe:  
  
```  
DROP ASSEMBLY MyDotNETAssembly  
```  
  
 DROP ASSEMBLY não interfere em nenhum código que referencia o assembly atualmente em execução, mas após a execução de DROP ASSEMBLY, qualquer tentativa de invocar o código do assembly falha.  
  
 DROP ASSEMBLY retornará um erro se o assembly for referenciado por outro assembly que exista no banco de dados ou se for usado por funções CLR (Common Language Runtime), procedimentos armazenados, gatilhos, UDTs (tipos definidos pelo usuário) ou UDAs (agregações definidas pelo usuário) no banco de dados atual. Primeiro use as instruções DROP AGGREGATE, DROP FUNCTION, DROP PROCEDURE, DROP TRIGGER e DROP TYPE para excluir todos os objetos de banco de dados gerenciados contidos no assembly.  
  
## <a name="removing-a-udt-from-the-database"></a>Removendo uma UDT do banco de dados  
 A instrução de DROP TYPE remove uma UDT do banco de dados atual. Quando uma UDT é descartada, você pode usar a instrução de DROP ASSEMBLY para descartar o assembly do banco de dados.  
  
 A instrução DROP TYPE falha caso objetos dependam da UDT, como nas seguintes situações:  
  
-   Tabelas no banco de dados que contêm colunas definidas usando a UDT.  
  
-   Funções, procedimentos armazenados ou gatilhos que usam variáveis ou parâmetros da UDT, criadas no banco de dados com a cláusula WITH SCHEMABINDING.  
  
### <a name="finding-udt-dependencies"></a>Localizando dependências do UDT  
 Você deve descartar todos os objetos dependentes primeiro e, em seguida, executar a instrução DROP TYPE. A consulta [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir localiza todas as colunas e parâmetros que usam um UDT no banco de dados **AdventureWorks** .  
  
```  
USE Adventureworks;  
SELECT o.name AS major_name, o.type_desc AS major_type_desc  
     , c.name AS minor_name, c.type_desc AS minor_type_desc  
     , at.assembly_class  
  FROM (  
        SELECT object_id, name, user_type_id, 'SQL_COLUMN' AS type_desc  
          FROM sys.columns  
     UNION ALL  
        SELECT object_id, name, user_type_id, 'SQL_PROCEDURE_PARAMETER'  
          FROM sys.parameters  
     ) AS c  
  JOIN sys.objects AS o  
    ON o.object_id = c.object_id  
  JOIN sys.assembly_types AS at  
    ON at.user_type_id = c.user_type_id;   
```  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciando assemblies de integração CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [Alterando um assembly](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)   
 [Criando um assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [Descartar AGREGAção &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-aggregate-transact-sql.md)   
 [FUNÇÃO DROP &#40;&#41;Transact-SQL](../../../t-sql/statements/drop-function-transact-sql.md)   
 [Descartar procedimento &#40;&#41;Transact-SQL](../../../t-sql/statements/drop-procedure-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-trigger-transact-sql.md)   
 [DROP TYPE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-type-transact-sql.md)  
  
  
