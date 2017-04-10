---
title: "Op&#231;&#227;o de Configura&#231;&#227;o de Servidor external scripts enabled | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "language-reference"
f1_keywords: 
  - "external scripts enabled"
  - "external_scripts_enabled_TSQL"
helpviewer_keywords: 
  - "opção external scripts enabled"
ms.assetid: 9d0ce165-8719-4007-9ae8-00f85cab3a0d
caps.latest.revision: 9
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 8
---
# Op&#231;&#227;o de Configura&#231;&#227;o de Servidor external scripts enabled
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Use a opção **external scripts enabled** para habilitar a execução de scripts com certas extensões de linguagens remotas. Essa propriedade será OFF por padrão. Opcionalmente, a instalação poderá definir essa propriedade como true se os **Serviços de Análise Avançada** estiverem instalados.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658).|  
  
 É necessário habilitar a opção external script enabled para poder executar um script externo usando o procedimento **sp_execute_external_script**. Use **sp_execute_external_script** para executar scripts escritos em uma linguagem com suporte, como R. No [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] é composto por um componente de servidor instalado com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e um conjunto de ferramentas de estação de trabalho e bibliotecas de conectividade que conectam o cientista de dados ao ambiente de alto desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Instale o recurso **Extensões de Análise Avançada** durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar a execução de scripts escritos em R. Para saber mais, confira [Installing Previous Versions of SQL Server R Services](../Topic/Installing%20Previous%20Versions%20of%20SQL%20Server%20R%20Services.md).  
  
 Execute o script a seguir para habilitar scripts externos.  
  
```  
sp_configure 'external scripts enabled', 1;  
RECONFIGURE;  
```  
  
 Você deve reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para efetivar a alteração.  
  
## Consulte também  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  