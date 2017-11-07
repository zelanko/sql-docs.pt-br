---
title: "(Analysis Services) de configuração de pós-instalação | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
- setup-install
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 7f4417b2-0efb-4361-a79e-fa56e43ee054
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8e172989400466a7ab78e3a2ff24022651524bd0
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="post-install-configuration-analysis-services"></a>Configuração de pós-instalação (Analysis Services)
  Após a instalação do Analysis Services, será necessário definir uma configuração adicional para tornar o servidor totalmente operacional e disponível para uso geral. Esta seção apresenta as tarefas adicionais que concluem a instalação. Dependendo dos requisitos de conexão, talvez você também precise configurar a autenticação (consulte [Conectar-se ao Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)).  
  
 Posteriormente, será necessário realizar outras tarefas quando houver bancos de dados prontos para serem implantados. Basicamente, você precisará configurar as associações de função no banco de dados para conceder ao usuário acesso aos dados, criar uma estratégia de backup e recuperação de banco de dados, e determinar se você precisa de uma carga de trabalho de processamento agendado para atualizar dados em intervalos regulares. Mais informações sobre a administração e a implantação de bancos de dados podem ser encontradas nestes links: [Bancos de dados de modelo multidimensional &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md) e [Bancos de dados de modelo de tabela &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md).  
  
## <a name="instance-configuration"></a>Configuração da instância  
 O Analysis Services é um serviço replicável, o que significa que você pode instalar várias instâncias do serviço em um único servidor. Cada instância adicional é instalada separadamente como uma instância nomeada, usando a Instalação do SQL Server, e é configurada de forma independente para oferecer suporte conforme pretendido. Por exemplo, um servidor de desenvolvimento poderá executar o Flight Recorder ou usar valores padrão para armazenamento de dados que você poderia alterar em servidores que oferecem suporte a cargas de trabalho de produção. Outro exemplo que requer o ajuste da configuração do sistema é a instalação da instância do Analysis Services no hardware compartilhado por outros serviços. Ao hospedar vários aplicativos com uso intensivo de dados no mesmo hardware, talvez você queira configurar propriedades de servidor que reduzam os limites de memória para otimizar recursos disponíveis em todos os aplicativos.  
  
## <a name="post-installation-tasks"></a>Tarefas pós-instalação  
  
|Link|Descrição da tarefa|  
|----------|----------------------|  
|[Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Crie uma regra de entrada no Firewall do Windows de modo que as solicitações possam ser roteadas através da porta TCP usada pela instância do Analysis Services. Esta tarefa é necessária. Ninguém pode acessar o Analysis Services em um computador remoto até que uma regra de entrada de firewall seja definida.|  
|[Conceder direitos de administração de servidor a uma instância do Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)|Durante a instalação, você precisava adicionar pelo menos uma conta de usuário à função Administrador da instância do Analysis Services. As permissões administrativas são necessárias a várias operações rotineiras do servidor, como processar dados de bancos de dados relacionais externos. Use as informações deste tópico para adicionar ou modificar a associação da função Administrador.|
|[Configurar software antivírus em computadores que executam o SQL Server](https://support.microsoft.com/kb/309422) |Talvez você precise configurar softwares de verificação, como aplicativos antivírus e antispyware, para excluir pastas e tipos de arquivos do SQL Server. Se o software de verificação bloquear um programa ou arquivo de dados quando o Analysis Services precisar usá-lo, poderá ocorrer interrupção do serviço ou dados corrompidos. |
|[Configurar contas de serviço &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)|Durante a instalação, a conta de serviço do Analysis Services foi fornecida, com permissões apropriadas para permitir o acesso controlado a programas executáveis e a arquivos de banco de dados. Como uma tarefa pós-instalação, agora você deve considerar se deve permitir o uso da conta de serviço ao executar tarefas adicionais. As cargas de trabalho de processamento e de consulta podem ser executadas na conta de serviço. Essas operações terão êxito somente quando a conta de serviço tiver as permissões apropriadas.|  
|[Registrar uma instância do Analysis Services em um grupo de servidores](../../analysis-services/instances/register-an-analysis-services-instance-in-a-server-group.md)|O SQL Server Management Studio (SSMS) permite criar grupos de servidores para organizar as instâncias do SQL Server. As implantações escalonáveis compostas de várias instâncias de servidor são mais fáceis de gerenciar em grupos de servidores. Use as informações deste tópico para organizar as instâncias do Analysis Services em grupos no SSMS.|  
|[Determina o Modo de Servidor de uma instância do Analysis Services.](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)|Durante a instalação, você escolhe um modo de servidor que determine o tipo de modelo (multidimensional ou de tabela) executado no servidor. Se você não tiver certeza do modo de servidor, use as informações deste tópico para determinar qual modo foi instalado.|  
|[Renomear uma instância do Analysis Services](../../analysis-services/instances/rename-an-analysis-services-instance.md)|Um nome descritivo pode ajudá-lo a fazer a distinção entre as várias instâncias que têm diferentes modos de servidor, ou entre as instâncias usadas principalmente por departamentos ou equipes da organização. Se você quiser alterar o nome da instância para uma que o ajude a gerenciar melhor as instalações, use as informações deste tópico para saber como fazer.|  
  
## <a name="next-steps"></a>Próximas etapas  
 Saiba como conectar-se ao Analysis Services em aplicativos Microsoft ou em aplicativos personalizados usando as bibliotecas de clientes. Dependendo dos requisitos da solução, talvez você também precise configurar o serviço para autenticação Kerberos. As conexões que devem ultrapassar os limites de domínio precisarão de acesso HTTP. Consulte [Connect to Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md) para obter instruções sobre as próximas etapas.  
  
## <a name="see-also"></a>Consulte também  
 [Instalação do SQL Server 2016](../../database-engine/install-windows/installation-for-sql-server-2016.md)   
 [Instalar o Analysis Services em modo multidimensional e de mineração de dados](http://msdn.microsoft.com/library/8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60)   
 [Instalar o Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md)   
 [Instale o Analysis Services no modo do Power Pivot.](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
  

