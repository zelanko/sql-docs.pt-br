---
title: "Op&#231;&#227;o clr enabled de configura&#231;&#227;o de servidor | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assemblies [integração CLR], verificando a possibilidade de execução"
  - "opção clr enabled"
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
caps.latest.revision: 36
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 36
---
# Op&#231;&#227;o clr enabled de configura&#231;&#227;o de servidor
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Use a opção clr habilitado para especificar se assemblies de usuário podem ser executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A opção clr enabled fornece os seguintes valores: 
  
|Valor|Descrição|  
|-----------|-----------------|  
|0|Execução de assembly não permitida no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|1|Execução de assembly permitida no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
Somente WOW64. Reinicie os servidores WOW64 para fazer com que as alterações de configurações tenham efeito. A reinicialização não é necessária para outros tipos de servidores.  

Ao executar RECONFIGURE e o valor de execução da opção clr enabled é alterado de 1 para 0, todos os domínios de aplicativo que contêm assemblies de usuário são descarregados imediatamente.  
  
>  **A execução de CLR (Common Language Runtime) não tem suporte com agrupamento simples** Desabilite uma das duas opções: "clr enabled" ou "lightweight pooling". Alguns dos recursos que dependem de CLR e não funcionam corretamente no modo fibra incluem o tipo de dados de **hierarquia**, a replicação e Gerenciamento Baseado em Políticas.  
  
## Exemplo  
 O exemplo a seguir primeiro mostra a configuração atual da opção clr enabled e, em seguida, habilita a opção configurando o valor da opção como 1. Para desabilitar a opção, defina o valor para 0.  
  
```tsql  
EXEC sp_configure 'clr enabled';  
EXEC sp_configure 'clr enabled' , '1';  
RECONFIGURE;    
```  
  
## Consulte também  
 [Opção lightweight pooling de configuração de Servidor](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opção lightweight pooling de configuração de Servidor](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
  