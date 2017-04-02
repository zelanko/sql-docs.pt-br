---
title: "Script de implanta&#231;&#227;o de inst&#226;ncia CDC | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8fa82822-ac99-48ef-a18d-f4f3a77105b4
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Script de implanta&#231;&#227;o de inst&#226;ncia CDC
  A caixa de diálogo CDC Instance Deployment Script que exibe o script de implantação de instância CDC. Este script pode ser usado para recriar o banco de dados CDC com todos os seus artefatos em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferente.  
  
 Depois de concluído o script de implantação, você deve ter certeza do seguinte:  
  
-   O script de implantação presume que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino estivesse preparada para o Oracle CDC, usando o Console de Configuração do Serviço Oracle CDC ou usando **prepare script** que o programa cria.  
  
-   A parte do script que é usada para habilitar o banco de dados para CDC precisa ser executada por um `sysadmin`.  
  
-   O script não preserva a senha da mineração de logs do Oracle. Isto precisa ser definido manualmente depois que o script é executado e o Serviço Oracle CDC é iniciado.  
  
 Selecione as seguintes opções na caixa de diálogo **CDC Instance Deployment Script** .  
  
 **Salvar como**  
 Salva o script em um arquivo de texto que você pode salvar em qualquer local desejado. Você pode copiar o arquivo com o script para qualquer outro servidor executá-lo lá.  
  
 **Copiar**  
 Copiar o script para a área de transferência. Você pode em seguida colar o script no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou em qualquer editor de texto para executar os scripts posteriormente.  
  
## Consulte também  
 [Preparar SQL Server para CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)  
  
  