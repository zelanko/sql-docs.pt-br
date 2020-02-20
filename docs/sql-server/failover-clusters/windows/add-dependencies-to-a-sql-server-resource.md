---
title: Adicionar dependências a um recurso FCI do SQL Server
descriptoin: Describes how to add dependencies to an Always On failover cluster instance (FCI) resource using the Failover Cluster Manager.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- resource dependencies [SQL Server]
- failover clustering [SQL Server], dependencies
- clusters [SQL Server], dependencies
- dependencies [SQL Server], clustering
ms.assetid: 25dbb751-139b-4c8e-ac62-3ec23110611f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e78380d509d2b291c0794cb408909a10622c3f53
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74822067"
---
# <a name="add-dependencies-to-a-sql-server-resource"></a>Adicionar dependências a um recurso do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como adicionar dependências a um recurso de FCI (instância de cluster de failover) Always On usando o snap-in Gerenciador de Cluster de Failover. O snap-in Gerenciador de Cluster de Failover é o aplicativo de gerenciamento de cluster do serviço WSFC (Windows Server Failover Clustering).  
  
-   **Antes de começar:**  [Limitações e restrições](#Restrictions), [Pré-requisitos](#Prerequisites)  
  
-   **Para adicionar uma dependência a um recurso do SQL Server, usando:** [Gerenciador de Cluster de Failover do Windows](#WinClusManager)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 É importante observar que se você adicionar qualquer outro recurso ao grupo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , esses recursos deverão sempre ter seus próprios recursos de nomes de rede do SQL exclusivos e seus próprios recursos de endereço IP do SQL.  
  
 Use os recursos de nome de rede do SQL existentes e os recursos de endereço IP do SQL somente para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se os recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] forem compartilhados com outros recursos, os seguintes problemas poderão ocorrer:  
  
-   Poderão ocorrer falhas inesperadas.  
  
-   As instalações do service pack poderão não ter êxito.  
  
-   O programa de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] poderá não ser bem-sucedido. Se esse problema ocorrer, você não poderá instalar mais instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nem executar manutenção rotineira.  
  
 Considere esses outros problemas:  
  
-   FTP com replicação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: para as instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que usam o FTP com replicação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], seu serviço de FTP deverá usar um dos mesmos discos físicos que a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] configurada para usar o serviço FTP.  
  
-   Dependências de recursos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: se você adicionar um recurso a um grupo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e tiver uma dependência no recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para verificar se o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está disponível, o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomendará que você adicione uma dependência no recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent. Não adicione uma dependência no recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para garantir que o computador que está executando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permanece altamente disponível, configure o recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent para que ele não afete o grupo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] caso o recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent falhe.  
  
-   Compartilhamentos de arquivos e recursos da impressora: quando você instala os recursos do Compartilhamento de Arquivo ou os recursos de cluster da Impressora, eles não devem ser colocados nos mesmos recursos de disco físico que o computador que está executando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se você for colocado nos mesmos recursos de disco físico, poderá vivenciar degradação de desempenho e perda de serviço para o computador que está executando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Considerações sobre o MS DTC: Depois de instalar o sistema operacional e configurar sua FCI, você deverá configurar o MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../../includes/msconame-md.md)]) para funcionar em um cluster usando o snap-in Gerenciador de Cluster de Failover. A falha ao agrupar o MS DTC não bloqueará a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , mas a funcionalidade do aplicativo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] poderá ser afetada se o MS DTC não for configurado corretamente.  
  
     Se você instalar o MS DTC em seu grupo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e tiver outros recursos que sejam dependentes do MS DTC, o MS DTC não estará disponível se esse grupo estiver offline ou durante um failover. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomendará que você coloque o MS DTC em seu próprio grupo com seu próprio recurso de disco físico, se for possível.  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Se você instalar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em um grupo de recursos do WSFC com várias unidades de disco em uma das unidades, o recurso [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será definido para ser dependente somente daquela unidade. Para colocar dados ou logs em outro disco, primeiro você deverá adicionar uma dependência ao recurso [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o disco adicional.  
  
##  <a name="WinClusManager"></a> Usando o snap-in Gerenciador de Cluster de Failover  
 **Para adicionar uma dependência a um recurso do SQL Server**  
  
-   Abra o snap-in Gerenciador de Cluster de Failover.  
  
-   Localize o grupo que contém o recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aplicável que você gostaria de tornar dependente.  
  
-   Se o recurso para o disco já estiver nesse grupo, vá para etapa 4. Caso contrário, localize o grupo que contém o disco. Se esse grupo e o grupo que contém o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não pertencerem ao mesmo nó, mova o grupo que contém o recurso para o disco para o nó que possui o grupo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Selecione o recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , abra a caixa de diálogo **Propriedades** e use a guia **Dependências** para adicionar o disco ao conjunto de dependências do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
  
