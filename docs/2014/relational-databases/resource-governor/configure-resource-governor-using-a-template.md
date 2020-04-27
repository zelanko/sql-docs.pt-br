---
title: Configurar o Resource Governor usando um modelo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, templates
ms.assetid: f342dec2-d1d6-483e-b44e-98eb7d168b5e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3da27154a824433d214dc495bf7f236ff104274f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68198931"
---
# <a name="configure-resource-governor-using-a-template"></a>Configurar o administrador de recursos usando um modelo
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
 [Administrador de Recursos](resource-governor.md)   
 [Habilitar Administrador de Recursos](enable-resource-governor.md)   
 [Pool de recursos do Administrador de Recursos](resource-governor-resource-pool.md)   
 [Grupos de carga de trabalho do Administrador de Recursos](resource-governor-workload-group.md)   
 [Função de classificação do Administrador de Recursos](resource-governor-classifier-function.md)   
 [Exibir Propriedades do Administrador de Recursos](view-resource-governor-properties.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-workload-group-transact-sql)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
