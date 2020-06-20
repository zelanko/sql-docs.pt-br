---
title: Funções definidas pelo usuário não são permitidas em system_function_schema | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- system functions [SQL Server]
- user-defined functions [SQL Server], system
ms.assetid: 3cb54053-ef65-4558-ae96-8686b6b22f4f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 7242f9fda74288a2b7354ac0550ff4966e05c555
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058776"
---
# <a name="user-defined-functions-are-not-allowed-in-system_function_schema"></a>Funções definidas pelo usuário não são permitidas no system_function_schema
  O supervisor de atualização detectou funções definidas pelo usuário que são de Propriedade do usuário não documentado **system_function_schema**. Você não pode criar uma função de sistema definida pelo usuário especificando esse usuário. O nome de usuário **system_function_schema** não existe e a ID de usuário que está associada a esse nome (UID = 4) é reservada para o esquema **Sys** e é restrita somente ao uso interno.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 O armazenamento de objeto de sistema mudou da seguinte maneira:  
  
-   Os objetos do sistema são armazenados no banco de dados de **recursos** somente leitura e as atualizações diretas do objeto do sistema não são permitidas.  
  
     Os objetos do sistema aparecem logicamente no esquema **Sys** de cada banco de dados. Isso mantém a habilidade para invocar funções de sistema de qualquer banco de dados especificando um nome de função de uma parte. Por exemplo, a instrução `SELECT * FROM fn_helpcollations()` pode ser executada de qualquer banco de dados.  
  
-   A **system_function_schema** de usuário não documentada foi removida.  
  
-   A ID de usuário associada a **system_function_schema** (UID = 4) é reservada para o esquema **Sys** e é restrita somente ao uso interno.  
  
 Essas alterações têm o seguinte efeito em funções de sistema definidas pelo usuário:  
  
-   Instruções DDL (linguagem de definição de dados) que fazem referência a **system_function_schema** falharão. Por exemplo, a instrução `CREATE FUNCTION system` _ `function` \_ `schema.fn` \_ `MySystemFunction` ... Não terá sucesso.  
  
-   Depois de atualizar para o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] , os objetos existentes que pertencem a **system_function_schema** estão contidos apenas no esquema **Sys** do banco de dados **mestre** . Como os objetos do sistema não podem ser modificados, essas funções nunca podem ser alteradas ou removidas do banco de dados **mestre** . Além disso, essas funções não podem ser invocadas a partir de outros bancos de dados pela especificação apenas de um nome de função de uma parte.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Antes da atualização, faça o seguinte:  
  
1.  Altere a propriedade das funções definidas pelo usuário existentes para **dbo** usando o procedimento armazenado do sistema **sp_changeobjectowner** .  
  
2.  Considere renomear a função de forma que ela não use o prefixo ‘fn_’. Isso evitará potenciais conflitos de nome com atuais ou futuras funções de sistema.  
  
3.  Adicione uma cópia das funções modificadas a todos os bancos de dados que as usam.  
  
4.  Substitua referências a **system_function_schema** com **dbo** em todos os scripts que contêm instruções DDL da função definida pelo usuário.  
  
5.  Modifique os scripts que chamam essas funções para usar o nome dbo de duas partes **.** _function_name_ou o nome de três partes _database_name_**.** dbo. *function_name*.  
  
 Para obter mais informações, consulte os seguintes tópicos dos Manuais Online do SQL Server:  
  
-   ‘sp_changeobjectowner’  
  
-   ‘Separação do esquema de usuário’  
  
-   ‘Banco de dados Recurso’  
  
## <a name="see-also"></a>Consulte Também  
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)   
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Remover instruções que modificam objetos do sistema](../../../2014/sql-server/install/remove-statements-that-modify-system-objects.md)   
 [Remover instruções que descartam objetos do sistema](../../../2014/sql-server/install/remove-statements-that-drop-system-objects.md)  
  
  
