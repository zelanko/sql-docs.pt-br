---
title: "Configurar FILESTREAM em um cluster de failover | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-blob"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FILESTREAM [SQL Server], configurando em um cluster de failover"
ms.assetid: 6721f780-20b7-4109-8ddb-ac327310699e
caps.latest.revision: 20
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 20
---
# Configurar FILESTREAM em um cluster de failover
  Este tópico descreve como habilitar FILESTREAM em um cluster de failover. Antes de tentar este procedimento, você deve entender [clustering de failover](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md) e ter o FILESTREAM habilitado. Para obter informações sobre como habilitar o FILESTREAM, veja [Habilitar e configurar o FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md).  
  
### Para configurar FILESTREAM em um cluster de failover  
  
1.  Configure o nó primário para o cluster de failover.  
  
     Depois de concluir a configuração, habilite o FILESTREAM no nó primário usando o **SQL Server Configuration Manager**. Isto habilita as configurações que requerem privilégios Admin do Windows. Se acesso remoto for necessário, selecione **Permitir que clientes remotos tenham acesso contínuo aos dados FILESTREAM**. Isso criará um recurso de cluster de compartilhamento de arquivo.  
  
2.  Configure um nó passivo.  
  
     Depois de concluir a configuração, habilite o FILESTREAM no nó passivo usando o **SQL Server Configuration Manager**. O nome especificado para **Nome de Compartilhamento do Windows** deve ser o mesmo em todos os nós no cluster.  
  
3.  Para adicionar mais nós passivos, repita a etapa 2.  
  
4.  Depois que todos os nós forem adicionados, conclua o processo executando o procedimento armazenado sp_configure em cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  Para adicionar e habilitar nós adicionais ao cluster, em qualquer momento, repita as etapas 2, 3 e 4.  
  
## Consulte também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Criar um novo cluster de failover do SQL Server &#40;Instalação&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)   
 [Remover uma Instância de Cluster de Failover do SQL Server &#40;Instalação&#41;](../../sql-server/failover-clusters/install/remove-a-sql-server-failover-cluster-instance-setup.md)   
 [Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
  