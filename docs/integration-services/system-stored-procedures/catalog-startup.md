---
title: catalog.startup | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 271fd405-246a-4852-bfbe-f557241ce6ea
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0d7e53242f007691f69ea85a31371129cd7c4216
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35331700"
---
# <a name="catalogstartup"></a>catalog.startup
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Executa a manutenção do estado das operações para o catálogo SSISDB.  
  
 O procedimento armazenado corrige o status de todos os pacotes que estavam sendo executados se e quando a instância do servidor [!INCLUDE[ssIS](../../includes/ssis-md.md)] fica inoperante.  
  
 Você tem a opção de permitir a execução automática do procedimento armazenado cada vez que a instância do servidor [!INCLUDE[ssIS](../../includes/ssis-md.md)] é reiniciada selecionando a opção **Habilitar a execução automática do procedimento armazenado do Integration Services na inicialização do SQL Server** na caixa de diálogo **Criar Catálogo**.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.startup  
```  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY na instância de execução, permissões READ e EXECUTE no projeto, e se aplicável, permissões READ no ambiente referenciado  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
  
