---
title: Adicionar dependências a um recurso do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 2a29577d6027c43fd35a8b27db8b402123c89a4b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63035630"
---
# <a name="add-dependencies-to-a-sql-server-resource"></a>Adicionar dependências a um recurso do SQL Server
  Este tópico descreve como adicionar dependências a um recurso de FCI (instância de cluster de failover) AlwaysOn usando o snap-in Gerenciador de Cluster de Failover. O snap-in Gerenciador de Cluster de Failover é o aplicativo de gerenciamento de cluster do serviço WSFC (Windows Server Failover Clustering).  
  
-   **Antes de começar:**  [Limitações e restrições](#Restrictions), [pré-requisitos](#Prerequisites)  
  
-   **Para adicionar uma dependência a um recurso do SQL Server, usando:** [Gerenciador de Cluster de Failover do Windows](#WinClusManager)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e Restrições  
 É importante observar que se você adicionar qualquer outro recurso ao grupo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , esses recursos deverão sempre ter seus próprios recursos de nomes de rede do SQL exclusivos e seus próprios recursos de endereço IP do SQL.  
  
 Use os recursos de nome de rede do SQL existentes e os recursos de endereço IP do SQL somente para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se os recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] forem compartilhados com outros recursos, os seguintes problemas poderão ocorrer:  
  
-   Poderão ocorrer falhas inesperadas.  
  
-   As instalações do service pack poderão não ter êxito.  
  
-   O programa de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] poderá não ser bem-sucedido. Se esse problema ocorrer, você não poderá instalar mais instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nem executar manutenção rotineira.  
  
 Considere esses outros problemas:  
  
-   FTP com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] replicação: Para instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que usam o FTP com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] replicação, o serviço FTP deve usar um dos mesmos discos físicos que a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que está configurado para usar o serviço FTP.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dependências de recursos: Se você adicionar um recurso a um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] grupo e tiver uma dependência na [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] recursos para certificar-se de que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estiver disponível, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomenda que você adicione uma dependência no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] recurso de agente. Não adicione uma dependência no recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para garantir que o computador que está executando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permanece altamente disponível, configure o recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent para que ele não afete o grupo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] caso o recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent falhe.  
  
-   Compartilhamentos de arquivos e recursos da impressora: Quando você instala os recursos de compartilhamento de arquivos ou recursos de cluster de impressora, eles não devem ser colocados nos mesmos recursos de disco físico do computador que está executando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se você for colocado nos mesmos recursos de disco físico, poderá vivenciar degradação de desempenho e perda de serviço para o computador que está executando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Considerações sobre o MS DTC: Depois de instalar o sistema operacional e configurar sua FCI, você deve configurar [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) para funcionar em um cluster usando o snap-in Gerenciador de Cluster de Failover. A falha ao agrupar o MS DTC não bloqueará a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , mas a funcionalidade do aplicativo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] poderá ser afetada se o MS DTC não for configurado corretamente.  
  
     Se você instalar o MS DTC em seu grupo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e tiver outros recursos que sejam dependentes do MS DTC, o MS DTC não estará disponível se esse grupo estiver offline ou durante um failover. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomendará que você coloque o MS DTC em seu próprio grupo com seu próprio recurso de disco físico, se for possível.  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Se você instalar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em um grupo de recursos do WSFC com várias unidades de disco em uma das unidades, o recurso [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será definido para ser dependente somente daquela unidade. Para colocar dados ou logs em outro disco, primeiro você deverá adicionar uma dependência ao recurso [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o disco adicional.  
  
##  <a name="WinClusManager"></a> Usando o snap-in Gerenciador de Cluster de Failover  
 **Para adicionar uma dependência a um recurso do SQL Server**  
  
-   Abra o snap-in Gerenciador de Cluster de Failover.  
  
-   Localize o grupo que contém o recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aplicável que você gostaria de tornar dependente.  
  
-   Se o recurso para o disco já estiver nesse grupo, vá para etapa 4. Caso contrário, localize o grupo que contém o disco. Se esse grupo e o grupo que contém o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não pertencerem ao mesmo nó, mova o grupo que contém o recurso para o disco para o nó que possui o grupo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Selecione o recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , abra a caixa de diálogo **Propriedades** e use a guia **Dependências** para adicionar o disco ao conjunto de dependências do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
  
