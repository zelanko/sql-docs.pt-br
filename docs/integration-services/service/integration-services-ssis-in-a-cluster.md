---
title: "SSIS (Integration Services) em um cluster | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0216266d-d866-4ea2-bbeb-955965f4d7c2
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# SSIS (Integration Services) em um cluster
  Clusterizar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não é recomendável, porque o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não é um serviço clusterizado ou que reconheça clusters e não dá suporte ao failover de um nó de cluster para outro. Portanto, em um ambiente clusterizado, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] deve ser instalado e iniciado como um serviço autônomo em cada nó do cluster.  
  
 Embora o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não seja um serviço clusterizado, você pode configurá-lo manualmente para operar como um recurso de cluster após instalar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] separadamente em cada nó do cluster.  
  
 No entanto, se seu objetivo for a alta disponibilidade ao estabelecer um ambiente de hardware clusterizado, você poderá atingi-lo sem configurar o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como um recurso de cluster.  Para gerenciar seus pacotes em qualquer nó do cluster por meio de qualquer outro nó do cluster, modifique o arquivo de configuração do serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em cada nó do cluster. Modifique cada um dos arquivos de configuração para que eles apontem a todas as instâncias disponíveis do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nas quais os pacotes estão armazenados. Esta solução oferece a alta disponibilidade necessária para a maioria dos clientes, sem os possíveis problemas encontrados quando o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é configurado como um recurso de cluster. Para obter mais informações sobre como modificar esse arquivo de configuração, veja [Configurando o Serviço Integration Services &#40;Serviço SSIS&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)  
  
 Compreender a função do serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é fundamental para tomar uma decisão sobre como configurar o serviço em um ambiente clusterizado. Para obter mais informações, veja [Serviço Integration Services &#40;Serviço SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
## <a name="understanding-the-disadvantages-of-configuring-integration-services-as-a-cluster-resource"></a>Compreendendo as desvantagens de configurar o Integration Services como um recurso de cluster  
 Algumas das possíveis desvantagens de configurar o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como um recurso de cluster são:  
  
-   **Quando um failover ocorre, os pacotes que estão sendo executados não reiniciam.**
    
    As falhas do pacote podem ser recuperadas reiniciando o pacote a partir dos pontos de verificação. A reinicialização a partir dos pontos de verificação pode ser realizada sem configurar o serviço como um recurso de cluster. Para saber mais, confira [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
-   Ao configurar o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em outro grupo de recursos por meio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], não é possível usar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] em computadores cliente para gerenciar os pacotes armazenados no banco de dados msdb. O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não pode delegar as credenciais neste cenário de salto duplo.  
  
-   Quando há vários grupos de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que incluem o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um cluster, um failover poderá causar resultados inesperados. Considere o cenário a seguir. O Grupo 1, que inclui o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , está em execução no Nó A. O Grupo 2, que também inclui o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , está em execução no Nó B. Ocorre um failover no Grupo 2 para o Nó A. A tentativa de iniciar outra instância do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no Nó A falha porque o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é um serviço de instância única. Saber se o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está tentando realizar failover para o Nó A também falhará depende da configuração do serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no Grupo 2. Se o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] foi configurado para afetar outros serviços no grupo de recursos, o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estiver em failover falhará devido a uma falha no serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Se o serviço foi configurado para não afetar outros serviços no grupo de recursos, o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá realizar failover para o Nó A. A menos que o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no Grupo 2 tenha sido configurado para não afetar outros serviços no grupo de recursos, a falha do serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que estiver em failover poderá fazer com que o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estiver realizando failover também falhe.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 Para obter instruções passo a passo sobre como configurar o serviço Integration Services em um cluster, consulte [Configurar o serviço Integration Services como um recurso de cluster](../../integration-services/service/configure-the-integration-services-service-as-a-cluster-resource.md).  
  
  