---
title: "Recursos desativados por padr&#227;o (Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a9529edf-337e-4fdd-9a13-99cfe96b4fa1
caps.latest.revision: 5
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 5
---
# Recursos desativados por padr&#227;o (Analysis Services)
  Uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é considerada segura por padrão. Assim, os recursos que podem comprometer a segurança são desabilitados por padrão. Os recursos a seguir são instalados em um estado desabilitado e deverão ser habilitados especificamente se você quiser usá-los.  
  
## Lista de recursos  
 Para habilitar os recursos a seguir, conecte-se ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Clique com o botão direito do mouse no nome da instância e selecione **Facetas**. Como alternativa, você pode habilitar esses recursos por meio das propriedades do servidor, conforme descrito na próxima seção.  
  
-   Consultas de mineração de dados ad hoc (OpenRowset)  
  
-   Objetos vinculados (para)  
  
-   Objetos vinculados (de)  
  
-   Escutar apenas em conexões locais  
  
-   Funções definidas pelo usuário  
  
## Propriedades do servidor  
 Recursos adicionais que são desativados por padrão podem ser habilitados por meio das propriedades do servidor. Conectar-se a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Clique com o botão direito do mouse no nome da instância e selecione **Propriedades**. Clique em **Geral**e, em seguida, clique em **Mostrar avançado** para exibir uma lista de propriedades maior.  
  
-   Consultas de mineração de dados ad hoc (OpenRowset)  
  
-   Permitir modelos de mineração de sessão (Mineração de dados)  
  
-   Objetos vinculados (para)  
  
-   Objetos vinculados (de)  
  
-   Funções COM definidas pelo usuário  
  
-   Definição de Rastreamento do Registrador de Voo (modelos).  
  
-   Gravação de log de consulta  
  
-   Escutar apenas em conexões locais  
  
-   XML binário  
  
-   Compactação  
  
-   Afinidade do grupo. Para obter detalhes, consulte [Thread Pool Properties](../../analysis-services/server-properties/thread-pool-properties.md) .  
  
  