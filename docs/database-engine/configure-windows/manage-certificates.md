---
title: Gerenciamento de certificado (SQL Server Configuration Manager) | Microsoft Docs
description: Saiba como instalar certificados em várias configurações do SQL Server. Os exemplos incluem instâncias únicas, clusters de failover e grupos de disponibilidade Always On.
ms.custom: ''
ms.date: 01/16/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 835d0b1da11ba014b14ede9637117357e84dc208
ms.sourcegitcommit: d498110ec0c7c62782fb694d14436f06681f2c30
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/22/2020
ms.locfileid: "85196043"
---
# <a name="certificate-management-sql-server-configuration-manager"></a>Gerenciamento de certificado (SQL Server Configuration Manager)

Este tópico descreve como implantar e gerenciar certificados em sua topologia de Grupos de Disponibilidade ou Cluster de Failover do SQL Server Always On.

Certificados SSL/TLS são amplamente usados para proteger o acesso ao SQL Server. Com versões anteriores do SQL Server, as organizações com grandes instalações do SQL Server precisavam realizar esforço considerável para manter sua infraestrutura de certificado do SQL Server, geralmente desenvolvendo scripts e executando comandos manuais. Com o SQL Server 2019, o gerenciamento de certificados está integrado ao SQL Server Configuration Manager, simplificando tarefas comuns como: 

* Exibir e validar certificados instalados em uma instância do SQL Server. 
* Identificar quais certificados podem estar perto de expirar. 
* Implantar certificados em computadores do Grupo de Disponibilidade Always On com base no nó que contém a réplica primária. 
* Implantar certificados entre computadores que participam de uma instância de cluster de failover sempre ativado com base no nó ativo.

> [!NOTE]
> Você pode usar gerenciamento de certificados no SQL Server Configuration Manager com versões anteriores do SQL Server, começando com o SQL Server 2008.

##  <a name="to-install-a-certificate-for-a-single-sql-server-instance"></a><a name="provision-single-server-cert"></a> Para instalar um certificado para uma única instância do SQL Server  
  
1. No SQL Server Configuration Manager, no painel de console, expanda **Configuração de Rede do SQL Server**.  
  
2. Clique com o botão direito do mouse em **Protocolos de** *&lt;Nome da instância&gt;* e, em seguida, selecione **Propriedades**.  
  
3. Escolha a guia **Certificado** e, em seguida, selecione **Importar**.  
  
4. Selecione **Procurar** e, em seguida, selecione o arquivo de certificado.  
  
5. Selecione **Avançar** para validar o certificado. Se não houver erros, selecione **Avançar** para importar o certificado para a instância local.  
  
 
##  <a name="to-install-a-certificate-in-a-failover-cluster-instance-configuration"></a><a name="provision-failover-cluster-cert"></a> Para instalar um certificado em uma configuração de instância do cluster de failover  
  
1. No SQL Server Configuration Manager, no painel de console, expanda **Configuração de Rede do SQL Server**.
  
2. Clique com o botão direito do mouse em **Protocolos de** *&lt;Nome da Instância&gt;* e, em seguida, escolha **Propriedades**. 

3. Escolha a guia **Certificado** e, em seguida, selecione **Importar**.

4. Selecione o tipo de certificado e se deseja importar para o nó atual ou para cada nó de cluster individual.

5. Se for instalar para um único nó, escolha **Procurar** e selecione o arquivo de certificado. Em seguida, vá para a etapa 8.

6. Se for instalar um certificado para cada nó, selecione **Avançar** para listar os possíveis nós do proprietário. Os possíveis proprietários da instância do cluster de failover atual são previamente selecionados.

7. Escolha **Avançar** para selecionar o certificado a ser importado.

8. Insira a senha quando solicitado. Procure quaisquer avisos ou erros após a validação.

9. Selecione **Avançar** para importar os certificados selecionados.

> [!NOTE]
> Conclua estas etapas no nó ativo da instância do cluster de failover sempre ativado. O usuário precisa ter permissões de administrador em todos os nós de cluster.

##  <a name="to-install-a-certificate-in-an-always-on-availability-group-configuration"></a><a name="provision-availability-group-cert"></a>Para instalar um certificado em uma configuração de Grupo de Disponibilidade Always On  
  
1. No SQL Server Configuration Manager, no painel de console, expanda **Configuração de Rede do SQL Server**.
  
2. Clique com o botão direito do mouse em **Protocolos de** *&lt;Nome da instância&gt;* e, em seguida, selecione **Propriedades**.  
  
3. Escolha a guia **Certificado** e, em seguida, selecione **Importar**.  
  
4. Escolha o tipo de certificado e selecione **Avançar** para selecionar na lista de Grupos de Disponibilidade conhecidos.  

5. Selecione **Avançar** para escolher certificados para cada nó de réplica. Os certificados devem ter um nome de arquivo que corresponda ao nome netbios dos nós.

6. Selecione **Avançar** para importar o certificado em cada nó.


> [!NOTE]
> Conclua estas etapas do nó que contém a réplica primária do Grupo de Disponibilidade. O usuário precisa ter permissões de administrador em todos os nós de cluster.

