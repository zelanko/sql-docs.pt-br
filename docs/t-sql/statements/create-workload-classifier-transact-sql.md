---
title: Classificador CREATE WORKLOAD (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD CLASSIFIER
- WORKLOAD_CLASSIFIER_TSQL
- CREATE WORKLOAD CLASSIFIER
- CREATE_WORKLOAD_CLASSIFIER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD CLASSIFIER statement
ms.assetid: ''
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: b5566230f1739fd1d19d7ffa9dd34ce07caf1fa4
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71951657"
---
# <a name="create-workload-classifier-transact-sql"></a>CREATE WORKLOAD CLASSIFIER (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Cria um classificador de gerenciamento de carga de trabalho.  O classificador alinha solicitações de entrada a um grupo de carga de trabalho e atribui a importância com base nos parâmetros especificados na definição de instrução do classificador.  Os classificadores são avaliados com o envio de cada solicitação.  Se uma solicitação não corresponde a um classificador, ela é atribuída ao grupo de carga de trabalho padrão.  O grupo de carga de trabalho padrão é a classe de recurso smallrc.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe

```
CREATE WORKLOAD CLASSIFIER classifier_name  
WITH  
    ( WORKLOAD_GROUP = 'name'  
     ,MEMBERNAME = 'security_account'
 [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL (default) | ABOVE_NORMAL | HIGH }])
[;]
```

## <a name="arguments"></a>Argumentos

 *classifier_name*  
 Especifique o nome pelo qual o classificador de carga de trabalho é identificado.  classifier_name é um sysname.  Ele pode ter até 128 caracteres e deve ser exclusivo dentro da instância.

WORKLOAD_GROUP = *'name'* Quando as condições são atendidas pelas regras de classificador, o nome mapeia a solicitação para um grupo de carga de trabalho.  o nome é um sysname.  Ele pode ter até 128 caracteres e deve ser um nome de grupo de carga de trabalho válido no momento da criação do classificador.

WORKLOAD_GROUP deve mapear para uma classe de recurso existente:

|Classes de recurso estáticas|Classes de recurso dinâmicas|
|------------------------|-----------------------|
|staticrc10|smallrc|
|staticrc20|mediumrc|
|staticrc30|largerc|
|staticrc40|xlargerc|
|staticrc50||
|staticrc60||
|staticrc70||
|staticrc80||

MEMBERNAME = *'security_account'* Essa é a conta de segurança que está sendo adicionada à função.  Security_account é um sysname, sem padrão. Security_account pode ser um usuário de banco de dados, uma função de banco de dados, um logon do Azure Active Directory ou um grupo do Azure Active Directory.

IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH } Especifica a importância relativa de uma solicitação.  A importância é uma das seguintes:

- LOW
- BELOW_NORMAL
- NORMAL (padrão)
- ABOVE_NORMAL
- HIGH  

A importância influencia a ordem na qual as solicitações são agendadas, oferecendo primeiro acesso a recursos e bloqueios.

Se um usuário for um membro de várias funções com classes de recursos diferentes atribuídos ou correspondentes em vários classificadores, o usuário receberá a atribuição de classe de recurso mais alta. Para obter mais informações, confira [classificação da carga de trabalho](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification#classification-precedence)

## <a name="permissions"></a>Permissões

 Requer a permissão CONTROL DATABASE.  
  
## <a name="examples"></a>Exemplos

 O exemplo seguinte mostra como criar um classificador de carga de trabalho denominado `wgcELTRole`. Ele usa o grupo de carga de trabalho staticrc20, o usuário `ELTRole` e define a importância como `above_normal`.

```sql
CREATE WORKLOAD CLASSIFIER wgcELTRole
  WITH (WORKLOAD_GROUP = 'staticrc20'
       ,MEMBERNAME = 'ELTRole'
      ,IMPORTANCE = above_normal);
```

## <a name="see-also"></a>Consulte Também

[Classificação do SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)</br>
[DROP WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-classifier-transact-sql.md)</br>
[sys.workload_management_workload_classifiers](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifiers-transact-sql.md)</br>
[sys.workload_management_workload_classifier_details](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifier-details-transact-sql.md)

