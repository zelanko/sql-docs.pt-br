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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fdb3a128753ca5e6be23eadf1c0b4fb91e9654c4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85674217"
---
# <a name="catalogstartup"></a>catalog.startup 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
  
  
