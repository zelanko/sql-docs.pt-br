---
title: Caixa de diálogo operações ativas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isoperations.executions.f1
- sql12.ssis.ssms.isoperations.general.f1
ms.assetid: 5bb0fcd6-0ce9-488a-85b8-25dddaa03cda
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f930a2e6f3ce84c330a4b7292ebaaba3b2ab871e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66062216"
---
# <a name="active-operations-dialog-box"></a>Caixa de diálogo Operações Ativas
  Use a caixa de diálogo **Operações Ativas** para exibir o status de operações do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em execução no momento no servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , como implantação, validação e execução de pacotes. Esses dados são armazenados no catálogo SSISDB.  
  
 Para obter mais informações sobre modos de exibição do [!INCLUDE[tsql](../includes/tsql-md.md)] relacionados, consulte [catalog.operations &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database), [catalog.validations &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-validations-ssisdb-database), e [catalog.executions &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database)  
  
 **O que você deseja fazer?**  
  
1.  [Abrir a caixa de diálogo Operações Ativas](#open_dialog)  
  
2.  [Configurar as opções](#options)  
  
##  <a name="open-the-active-operations-dialog-box"></a><a name="open_dialog"></a>Abrir a caixa de diálogo operações ativas  
  
1.  Abra [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
2.  Conectar-se ao Mecanismo de Banco de Dados do Microsoft SQL Server  
  
3.  No Pesquisador de Objetos, expanda o nó **Integration Services** , clique com o botão direito do mouse em **SSISDB**e clique em **Operações Ativas**.  
  
##  <a name="configure-the-options"></a><a name="options"></a>Configurar as opções  
  
### <a name="options"></a>Opções  
 **Tipo**  
 Especifica o tipo de operação. A seguir estão os valores possíveis para o campo **Type** e os valores correspondentes na coluna operations_type da exibição TRANSACT-SQL `catalog.operations` .  
  
|||  
|-|-|  
|Inicialização do Integration Services|1|  
|Limpeza de operações (trabalho do SQL Agent)|2|  
|Limpeza de versões do projeto (trabalho do SQL Agent)|3|  
|Implantar projeto|101|  
|Restaurar projeto|106|  
|Criar e iniciar execução de pacote|200|  
|Parar operação (parando uma validação ou execução|202|  
|Validar projeto|300|  
|Validar pacote|301|  
|Configurar catálogo|1000|  
  
 **Parar**  
 Clique para parar uma operação em execução no momento.  
  
  
