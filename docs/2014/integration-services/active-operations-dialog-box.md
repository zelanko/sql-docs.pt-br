---
title: Caixa de diálogo operações ativas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isoperations.executions.f1
- sql12.ssis.ssms.isoperations.general.f1
ms.assetid: 5bb0fcd6-0ce9-488a-85b8-25dddaa03cda
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b3c9105d6649443d8ec2d3425f86d609dfe6a2b3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151117"
---
# <a name="active-operations-dialog-box"></a>Caixa de diálogo Operações Ativas
  Use a caixa de diálogo **Operações Ativas** para exibir o status de operações do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em execução no momento no servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , como implantação, validação e execução de pacotes. Esses dados são armazenados no catálogo SSISDB.  
  
 Para obter mais informações sobre modos de exibição do [!INCLUDE[tsql](../includes/tsql-md.md)] relacionados, consulte [catalog.operations &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database), [catalog.validations &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-validations-ssisdb-database), e [catalog.executions &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database)  
  
 **O que você deseja fazer?**  
  
1.  [Abrir a caixa de diálogo operações ativas](#open_dialog)  
  
2.  [Configurar as opções](#options)  
  
##  <a name="open_dialog"></a> Abrir a caixa de diálogo Operações Ativas  
  
1.  Abra [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
2.  Conectar-se ao Mecanismo de Banco de Dados do Microsoft SQL Server  
  
3.  No Pesquisador de Objetos, expanda o nó **Integration Services** , clique com o botão direito do mouse em **SSISDB**e clique em **Operações Ativas**.  
  
##  <a name="options"></a> Configurar as opções  
  
### <a name="options"></a>Opções  
 **Tipo**  
 Especifica o tipo de operação. A seguir estão os valores possíveis para o **tipo** campo e os valores correspondentes na coluna operations_type da Transact-SQL `catalog.operations` modo de exibição.  
  
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
|Configurar catálogo|1.000|  
  
 **Parar**  
 Clique para parar uma operação em execução no momento.  
  
  
