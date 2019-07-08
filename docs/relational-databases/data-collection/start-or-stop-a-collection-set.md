---
title: Iniciar ou interromper um conjunto de coleta | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- collection sets [SQL Server], stopping
- collection sets [SQL Server], starting
ms.assetid: 48a7b2fe-6bc3-4278-a7ec-1babc1290345
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 12e425f889826a5fc9464ee8c85c88ab05043f4b
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67580288"
---
# <a name="start-or-stop-a-collection-set"></a>Iniciar ou interromper um conjunto de coleta
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como iniciar ou interromper um conjunto de coleta no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para iniciar ou interromper um conjunto de coleta usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Os procedimentos armazenados e as exibições do catálogo do coletor de dados são armazenados no banco de dados **msdb** .  
  
-   Diferentemente de procedimentos armazenados comuns, os procedimentos armazenados do coletor de dados usam estritamente parâmetros digitados e não oferecem suporte à conversão automática de tipo de dados. Se esses parâmetros não forem chamados pelos tipos de dados com parâmetros de entrada corretos, como especificado na descrição do argumento, o procedimento armazenado retornará um erro.  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   O SQL Server Agent deve ser iniciado.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Para obter informações sobre conjuntos de coleta, consulte a exibição de catálogo [syscollector_collection_sets](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md) .  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a associação na função de banco de dados fixa **dc_operator** . Se o conjunto de coleta não tiver uma conta proxy, a associação da função de servidor fixa **sysadmin** será necessária. Exemplos  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-start-a-collection-set"></a>Para iniciar um conjunto de coleta  
  
1.  No Pesquisador de Objetos, expanda o nó **Gerenciamento** , expanda **Coleta de Dados**e, em seguida, **Conjuntos de Coleta de Dados do Sistema**.  
  
2.  Clique com o botão direito do mouse no conjunto de coleta que deseja iniciar e clique em **Iniciar Conjunto de Coleta de Dados**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     A message box displays the results of this action, and a green arrow on the icon for the collection set indicates that the collection set has started.  
  
#### <a name="to-stop-a-collection-set"></a>Para parar um conjunto de coleta  
  
1.  No Pesquisador de Objetos, expanda o nó **Gerenciamento** , expanda **Coleta de Dados**e, em seguida, **Conjuntos de Coleta de Dados do Sistema**.  
  
2.  Clique com o botão direito do mouse no conjunto de coleta a ser interrompido e clique em **Parar Conjunto de Coleta de Dados**.  
  
     Uma caixa de mensagem exibe os resultados dessa ação e um círculo vermelho no ícone do conjunto de coleta indica que o conjunto de coleta foi interrompido.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-start-a-collection-set"></a>Para iniciar um conjunto de coleta  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo usa [sp_syscollector_start_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql.md) para iniciar o conjunto de coleta que tem a ID `1`.  
  
```sql  
USE msdb;  
GO  
EXEC sp_syscollector_start_collection_set @collection_set_id = 1;  
```  
  
#### <a name="to-stop-a-collection-set"></a>Para parar um conjunto de coleta  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo usa [sp_syscollector_stop_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md) para interromper o conjunto de coleta que tem a ID `1`.  
  
```sql  
USE msdb;  
GO  
EXEC sp_syscollector_stop_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do Coletor de Dados &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
