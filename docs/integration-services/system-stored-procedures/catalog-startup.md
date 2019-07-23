---
title: catalog.startup | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 271fd405-246a-4852-bfbe-f557241ce6ea
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4d3087f5816b32ffa83876a32a07ccca521c9394
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038637"
---
# <a name="catalogstartup"></a>catalog.startup 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
 None  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY na instância de execução, permissões READ e EXECUTE no projeto, e se aplicável, permissões READ no ambiente referenciado  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
  
