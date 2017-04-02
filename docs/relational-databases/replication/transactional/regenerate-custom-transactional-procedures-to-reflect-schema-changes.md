---
title: "Regenerar os procedimentos transacionais personalizados para refletir altera&#231;&#245;es de esquema | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "procedimentos personalizados [replicação do SQL Server]"
  - "replicação transacional, replicando alterações de esquema"
  - "esquemas [replicação do SQL Server], replicando alterações"
ms.assetid: ccf68a13-e748-4455-8168-90e6d2868098
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Regenerar os procedimentos transacionais personalizados para refletir altera&#231;&#245;es de esquema
  Por padrão, a replicação transacional faz todas as alterações de dados nos Assinantes por meio de um conjunto de procedimentos armazenados gerados por procedimentos internos para cada artigo de tabela na publicação. Os três procedimentos (um de cada para inserir, atualizar e excluir) são copiados para o Assinante e executados quando uma inserção, atualização ou exclusão for replicada para o Assinante. Quando uma alteração de esquema é feita em uma tabela do Publicador [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a replicação regenera esses procedimentos automaticamente, chamando o mesmo conjunto de procedimentos de script interno, de modo que os novos procedimentos correspondam ao novo esquema (a replicação de alterações de esquema não tem suporte para Publicadores Oracle).  
  
 Também é possível especificar procedimentos personalizados para substituir um ou mais procedimentos padrão. Os procedimentos personalizados devem ser alterados se a alteração do esquema afetar o procedimento. Por exemplo, se um procedimento fizer referência a uma coluna descartada em uma alteração de esquema, as referências à coluna deverão ser removidas do procedimento. Há dois modos para que a replicação propague um novo procedimento personalizado aos Assinantes:  
  
-   A primeira opção é usar um procedimento de script personalizado para substituir os padrões usados pela replicação:  
  
    1.  Ao executar [sp_addarticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), certifique-se de **@schema_option** 0x02 bit é **true**.  
  
    2.  Executar [sp_register_custom_scripting & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md) e especifique um valor de 'insert', 'update' ou 'delete' para o parâmetro **@type** e procedimento para o parâmetro de script o nome personalizado **@value**.  
  
     Na próxima alteração de esquema, a replicação chamará esse procedimento armazenado para substituir a definição pelo novo procedimento armazenado personalizado definido pelo usuário e depois propagará o procedimento para cada Assinante.  
  
-   A segunda opção é usar um script que contenha uma nova definição de procedimento personalizada:  
  
    1.  Ao executar [sp_addarticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), defina o **@schema_option** 0x02 bit como **false** para replicação não gere automaticamente procedimentos personalizados no assinante.  
  
    2.  Antes de cada mudança de esquema, crie um novo arquivo de script e registre o script com replicação executando [sp_register_custom_scripting & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md). Especifique um valor de 'custom_script' para o parâmetro **@type** e o caminho para o script no Editor para o parâmetro **@value**.  
  
     Na próxima vez em que for feita uma alteração de esquema relevante, esse script será executado em cada Assinante dentro da mesma transação como o comando DDL. Após concluir a alteração de esquema, o registro do script será removido. Você deve registrar de novo o script para que ele seja executado depois de uma alteração de esquema subsequente.  
  
## Consulte também  
 [Especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)   
 [Fazer alterações de esquema em bancos de dados de publicação](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  