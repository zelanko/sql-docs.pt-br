---
title: Funções definidas pelo usuário não são permitidas em system_function_schema | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- system functions [SQL Server]
- user-defined functions [SQL Server], system
ms.assetid: 3cb54053-ef65-4558-ae96-8686b6b22f4f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a91275eadeebd6b996774363ab279eddc76f0f75
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540015"
---
# <a name="user-defined-functions-are-not-allowed-in-systemfunctionschema"></a>Funções definidas pelo usuário não são permitidas no system_function_schema
  O Supervisor de atualização detectou funções definidas pelo usuário que são propriedade do usuário não documentado **system_function_schema**. Você não pode criar uma função de sistema definida pelo usuário especificando esse usuário. O **system_function_schema** nome de usuário não existe e a ID de usuário que está associado com esse nome (UID = 4) é reservada para o **sys** esquema e restrita para uso interno apenas.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 O armazenamento de objeto de sistema mudou da seguinte maneira:  
  
-   Objetos de sistema são armazenados em somente leitura **recurso** de banco de dados e direcionar atualizações de objeto do sistema não são permitidas.  
  
     Objetos do sistema aparecem logicamente na **sys** esquema de cada banco de dados. Isso mantém a habilidade para invocar funções de sistema de qualquer banco de dados especificando um nome de função de uma parte. Por exemplo, a instrução `SELECT * FROM fn_helpcollations()` pode ser executada de qualquer banco de dados.  
  
-   O usuário não documentado **system_function_schema** foi removido.  
  
-   O usuário associado à ID **system_function_schema** (UID = 4) é reservada para o **sys** esquema e restrita para uso interno apenas.  
  
 Essas alterações têm o seguinte efeito em funções de sistema definidas pelo usuário:  
  
-   Instruções do Data Definition Language (DDL) que referenciam **system_function_schema** falhará. Por exemplo, a instrução `CREATE FUNCTION system`_`function` \_ `schema.fn` \_ `MySystemFunction` ... não terá êxito.  
  
-   Depois de atualizar para [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], objetos existentes que são de propriedade **system_function_schema** estão contidas no apenas o **sys** esquema do **mestre** banco de dados. Como objetos do sistema não podem ser modificados, essas funções nunca podem ser alteradas ou descartadas do **mestre** banco de dados. Além disso, essas funções não podem ser invocadas a partir de outros bancos de dados pela especificação apenas de um nome de função de uma parte.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Antes da atualização, faça o seguinte:  
  
1.  Alterar a propriedade das funções existentes definidas pelo usuário para **dbo** usando o **sp_changeobjectowner** procedimento armazenado do sistema.  
  
2.  Considere renomear a função de forma que ela não use o prefixo ‘fn_’. Isso evitará potenciais conflitos de nome com atuais ou futuras funções de sistema.  
  
3.  Adicione uma cópia das funções modificadas a todos os bancos de dados que as usam.  
  
4.  Substitua referências a **system_function_schema** com **dbo** em todos os scripts que contêm instruções DDL de funções definidas pelo usuário.  
  
5.  Modifique os scripts que invocam essas funções para usar ambos o nome de duas partes dbo **. * * * function_name*, ou o nome de três partes *database_name ***.** dbo.* function_name *.  
  
 Para obter mais informações, consulte os seguintes tópicos dos Manuais Online do SQL Server:  
  
-   ‘sp_changeobjectowner’  
  
-   ‘Separação do esquema de usuário’  
  
-   ‘Banco de dados Recurso’  
  
## <a name="see-also"></a>Consulte também  
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)   
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Remover instruções que modificam objetos do sistema](../../../2014/sql-server/install/remove-statements-that-modify-system-objects.md)   
 [Remover instruções que descartam objetos do sistema](../../../2014/sql-server/install/remove-statements-that-drop-system-objects.md)  
  
  
