---
title: Cluster DTC para grupos de disponibilidade do SQL Server 2016 | Microsoft Docs
ms.custom: 
ms.date: 08/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a47c5005-20e3-4880-945c-9f78d311af7a
caps.latest.revision: 3
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dd12e9e9a611a850b739522be29e79ff850ce3a2
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="cluster-dtc-for-sql-server-2016-availability-groups"></a>Cluster DTC para Grupos de Disponibilidade do SQL Server 2016
Este tópico descreve os requisitos e as etapas para agrupar em cluster o serviço DTC (Coordenador de Transações Distribuídas) da Microsoft do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para obter mais informações sobre transações distribuídas e o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [Transações entre bancos de dados e transações distribuídas para Grupos de Disponibilidade AlwaysOn e Espelhamento de Banco de Dados (SQL Server)](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).

 ## <a name="checklist-preliminary-requirements"></a>Lista de verificação: Requisitos preliminares
||Tarefa|Referência|  
|------|-----------------|----------|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Verifique se todos os nós, os serviços e o Grupo de Disponibilidade foram configurados corretamente.|[Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)|
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Verifique se os requisitos do DTC do Grupo de Disponibilidade foram atendidos.|[Transações entre bancos de dados e transações distribuídas para Grupos de Disponibilidade AlwaysOn e o Espelhamento de Banco de Dados (SQL Server)](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)

## <a name="checklist-clustered-dtc-resource-dependencies"></a>Lista de verificação: Dependências de recurso DTC clusterizado
||Tarefa|Referência|  
|------|-----------------|----------|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Uma unidade de armazenamento compartilhado.|[Configurando a unidade de armazenamento compartilhado](https://msdn.microsoft.com/library/cc982358(v=bts.10).aspx). Considere o uso da letra da unidade **M**.|
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Um recurso exclusivo do Nome de Rede do DTC.  O nome será registrado como um objeto de computador de cluster no Active Directory.<br /><br />Garanta que uma das seguintes opções é verdadeira:<br /><br />• O usuário que cria o recurso de nome de rede do DTC tem a permissão de objetos Create Computer para a UO ou o contêiner em que o recurso de nome de rede do DTC residirá.<br /><br />• Se o usuário não tiver a permissão de objetos Create Computer, peça ao administrador do domínio para pré-preparar um objeto de computador de cluster para o recurso de Nome de Rede do DTC.|[Pré-configurar objetos de computador de cluster no Active Directory Domain Services](https://technet.microsoft.com/library/dn466519(v=ws.11).aspx)|
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Um endereço IP estático disponível válido e a máscara de sub-rede apropriada para esse endereço IP.||

## <a name="cluster-the-dtc-resource"></a>Agrupar o recurso DTC em cluster
Depois de criar o recurso de grupo de disponibilidade, crie um recurso DTC clusterizado e adicione-o ao grupo de disponibilidade.  Um exemplo de script pode ser visto em [Criar DTC clusterizado para um Grupo de Disponibilidade AlwaysOn](../../../database-engine/availability-groups/windows/create-clustered-dtc-for-an-always-on-availability-group.md).


## <a name="checklist-post-clustered-dtc-resource-configurations"></a>Lista de verificação: Pós-configurações de recurso DTC clusterizados
||Tarefa|Referência|  
|------|-----------------|----------|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Habilite o acesso à rede com segurança para o recurso DTC clusterizado.|[Habilitar o acesso à rede com segurança para o MS DTC](https://technet.microsoft.com/library/cc753620(v=ws.10).aspx)|
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Interrompa e desabilite o serviço DTC local.|[Configurar como um serviço é iniciado](https://technet.microsoft.com/library/cc755249(v=ws.11).aspx)|
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Realize um ciclo do serviço SQL Server de cada instância no Grupo de Disponibilidade.  Execute failover do Grupo de Disponibilidade, conforme necessário.|[Executar um failover manual planejado de um grupo de disponibilidade (SQL Server)](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)<br /><br />[Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)|

- Se o servidor for Windows Server 2012 R2, o sistema operacional deve ter [KB 3030373](http://support.microsoft.com/kb/3090973) aplicado.

- Preparar os servidores para Grupos de Disponibilidade de acordo com as listas de verificação em [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).

- Configurar instâncias de servidor para [**Grupos de Disponibilidade AlwaysOn**](../../../database-engine/availability-groups/windows/configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md).

### <a name="resources"></a>RESOURCES


[Mais informações sobre como testar o DTC em grupos de disponibilidade:](https://blogs.technet.microsoft.com/dataplatform/2016/01/25/sql-server-2016-dtc-support-in-availability-groups/)

[Monitorando exibições do sistema de grupos de disponibilidade AlwaysOn](https://msdn.microsoft.com/library/ff878305.aspx)

[Criar grupo de disponibilidade passo a passo](https://msdn.microsoft.com/library/ff878307.aspx)


[Suporte do DTC no SQL Server 2016 em grupos de disponibilidade](http://blogs.technet.microsoft.com/dataplatform/2016/01/25/sql-server-2016-dtc-support-in-availability-groups/) 

[Link externo: configurar o DTC para uma instância clusterizada do SQL Server com o Windows Server 2008 R2](http://sqlha.com/2013/03/12/how-to-properly-configure-dtc-for-clustered-instances-of-sql-server-with-windows-server-2008-r2/)

