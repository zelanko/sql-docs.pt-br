---
title: Realizar o balanceamento de carga de pacotes em servidores remotos usando o SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- load-balancing [Integration Services]
- parent packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 9281c5f8-8da3-4ae8-8142-53c5919a4cfe
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d2e52b17b84f2032aec6e142dc2b845ff1ae0bd8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235216"
---
# <a name="load-balancing-packages-on-remote-servers-by-using-sql-server-agent"></a>Pacotes de balanceamento de carga em servidores remotos usando o SQL Server Agent
  Quando for necessário executar muitos pacotes, será conveniente usar outros servidores que estejam disponíveis. Este método de usar outros servidores para executar pacotes quando os pacotes estão sob o controle de um pacote pai é chamado balanceamento de carga. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], o balanceamento de carga é um procedimento manual que deve ser projetado pelos proprietários dos pacotes. Balanceamento de carga não é executado automaticamente pelos servidores. Além disso, os pacotes que estão em execução nos servidores remotos devem ser pacotes completos, não tarefas individuais em outros pacotes.  
  
 Balanceamento de carga é útil nos seguintes cenários:  
  
-   Pacotes podem executar ao mesmo tempo.  
  
-   Pacotes são grandes e, se executados em sequência, podem executar por mais tempo que o permitido para o processamento.  
  
 Administradores e arquitetos podem determinar se usar servidores adicionais para o processamento beneficiaria os processos.  
  
## <a name="illustration-of-load-balancing"></a>Ilustração do balanceamento de carga  
 O diagrama a seguir mostra um pacote pai em um servidor. O pacote pai contém várias tarefas Executar Trabalho do SQL Agent. Cada tarefa no pacote pai chama um SQL Server Agent em um servidor remoto. Esses servidores remotos contêm trabalhos do SQL Server Agent que incluem uma etapa que chama um pacote naquele servidor.  
  
 ![Visão geral da arquitetura de balanceamento de carga do SSIS](../media/loadbalancingoverview.gif "Visão geral da arquitetura de balanceamento de carga do SSIS")  
  
 As etapas exigidas para balanceamento de carga nesta arquitetura não são conceitos novos. Em vez disso, o balanceamento de carga é alcançado usando conceitos existentes e objetos SSIS comuns em uma nova maneira.  
  
## <a name="execution-of-packages-on-a-remote-instance-by-using-sql-server-agent"></a>Execução de pacotes em uma instância remota por meio do SQL Server Agent  
 Na arquitetura básica para execução de pacote remoto, um pacote central está localizado na instância do SQL Server que controla os pacotes remotos. O diagrama mostra esse pacote central, nomeado o Pai do SSIS. A instância onde esse pacote pai reside controla a execução dos trabalhos do SQL Server Agent que executam os pacotes filhos. Os pacotes filhos não executam conforme uma agenda fixa controlada pelo SQL Server Agent no servidor remoto. Em vez disso, os pacotes filhos são iniciados pelo SQL Server Agent, quando chamados pelo pacote pai, e são executados na mesma instância do SQL Server em que o SQL Server Agent reside.  
  
 Antes que possa executar um pacote remoto usando um SQL Server Agent, é preciso configurar os pacotes pai e filho e os trabalhos do SQL Server Agent que controlam os pacotes filhos. As seções a seguir fornecem mais informações sobre como criar, configurar, executar e manter pacotes que executam em servidores remotos. Há várias etapas para esse processo:  
  
-   Criando e instalando o pacote filho em servidores remotos.  
  
-   Criando os trabalhos SQL Server Agent nas instâncias remotas que executarão os pacotes.  
  
-   Criando um pacote pai.  
  
-   Determine o cenário de log para os pacotes filhos.  
  
 A tabela a seguir fornece links a tópicos que o guiam pelo processo.  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Implementação de pacotes filho](../implementation-of-child-packages.md)|Descreve a instalação de pacotes e a criação de trabalhos do SQL Server Agent para execução dos pacotes.|  
|[Implementação do pacote pai](../implementation-of-the-parent-package.md)|Descreve a criação do pacote pai que contém muitas tarefas de Executar Trabalho do SQL Server Agent. Cada tarefa executa um dos pacotes filhos.|  
|[Log para carga de pacotes balanceados em servidores remotos](../logging-for-load-balanced-packages-on-remote-servers.md)|Descreve o cenário de log para os pacotes remotos.|  
  
## <a name="related-tasks"></a>Related Tasks  
 [Agendar um pacote usando o SQL Server Agent](../schedule-a-package-by-using-sql-server-agent.md)  
  
  
