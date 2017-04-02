---
title: "Caixa de di&#225;logo Opera&#231;&#245;es Ativas | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.ssms.isoperations.executions.f1"
  - "sql13.ssis.ssms.isoperations.general.f1"
ms.assetid: 5bb0fcd6-0ce9-488a-85b8-25dddaa03cda
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Caixa de di&#225;logo Opera&#231;&#245;es Ativas
  Use a caixa de diálogo **Operações Ativas** para exibir o status de operações do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em execução no momento no servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , como implantação, validação e execução de pacotes. Esses dados são armazenados no catálogo SSISDB.  
  
 Para obter mais informações sobre modos de exibição do [!INCLUDE[tsql](../../includes/tsql-md.md)] relacionados, consulte [catalog.operations &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md), [catalog.validations &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md), e [catalog.executions &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
  
 **O que você deseja fazer?**  
  
-   [Abrir a caixa de diálogo Operações Ativas](../../integration-services/performance/active-operations-dialog-box.md#open_dialog)  
  
-   [Opções](#options)  
  
##  <a name="open_dialog"></a> Abrir a caixa de diálogo Operações Ativas  
  
1.  Abra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Conectar-se ao Mecanismo de Banco de Dados do Microsoft SQL Server  
  
3.  No Pesquisador de Objetos, expanda o nó **Integration Services**, clique com o botão direito do mouse em **SSISDB** e clique em **Operações Ativas**.  
  
## Configurar as opções  
  
###  <a name="options"></a> Opções  
 **Tipo**  
 Especifica o tipo de operação. Os seguintes são os valores possíveis para o campo **Tipo** e os valores correspondentes na coluna operations_type da exibição **catalog.operations** do Transact-SQL.  
  
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
  
  