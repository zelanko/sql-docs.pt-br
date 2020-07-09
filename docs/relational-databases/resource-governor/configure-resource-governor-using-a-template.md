---
title: Configurar o Resource Governor usando um modelo | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, templates
ms.assetid: f342dec2-d1d6-483e-b44e-98eb7d168b5e
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: bb17a0d2b42528d886430e92b82908a3e08b5694
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720528"
---
# <a name="configure-resource-governor-using-a-template"></a>Configurar o administrador de recursos usando um modelo
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Você pode configurar o Administrador de recursos usando um modelo que é fornecido em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   **Antes de começar:**  [Permissões](#Permissions)  
  
-   **Para criar um grupo de carga de trabalho usando:** [um modelo](#ConfRGTemplate)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
 Use as etapas a seguir para abrir e modificar um modelo que cria um pool de recursos e um grupo de cargas de trabalho para o pool. Além disso, esse modelo permite que você crie uma função de classificador definida pelo usuário que roteia novas conexões para o grupo padrão ou o grupo de cargas de trabalho que você criar.  
  
###  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 As instruções do [!INCLUDE[tsql](../../includes/tsql-md.md)] do administrador de recursos no modelo exigem a permissão CONTROL SERVER.  
  
##  <a name="configure-resource-governor-using-a-template"></a><a name="ConfRGTemplate"></a> Configurar o administrador de recursos usando um modelo  
 **Para configurar o Administrador de Recursos usando um modelo no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no menu **Exibir** , clique em **Gerenciador de Modelos**.  
  
2.  Em **Explorador de Modelos**, expanda **Administrador de Recursos**e clique duas vezes em **Configurar Administrador de Recursos**.  
  
3.  Em **Conectar ao Database Engine**, digite as informações exigidas e então clique em **OK**. O modelo Configurar administrador de recursos.sql é fornecido no Editor de consultas. Use este modelo para criar e configurar um pool de recursos, um grupo de carga de trabalho e uma função de classificador.  
  
4.  Para alterar os valores no modelo, pressione CTRL+SHIFT+M. Na janela **Especificar Valores para Parâmetros de Modelos** , digite os valores que deseja usar.  
  
5.  Para salvar as alterações que fizer no modelo, clique em **OK**.  
  
6.  Para executar a consulta, clique em **Executar**.  

## <a name="see-also"></a>Consulte Também  
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Habilitar Administrador de Recursos](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Pool de recursos do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Grupos de carga de trabalho do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Função de classificação do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [Exibir Propriedades do Administrador de Recursos](../../relational-databases/resource-governor/view-resource-governor-properties.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
