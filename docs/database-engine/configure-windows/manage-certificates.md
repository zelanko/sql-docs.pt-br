---
title: Gerenciamento de certificado (SQL Server Configuration Manager) | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: f767dba6c45c3bdc0d91b29ab561cb5f5de74844
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66785159"
---
# <a name="certificate-management-sql-server-configuration-manager"></a>Gerenciamento de certificado (SQL Server Configuration Manager)

Este tópico descreve como implantar e gerenciar certificados em sua topologia de Grupos de Disponibilidade ou Cluster de Failover do SQL Server Always On.

Certificados SSL/TLS são amplamente usados para proteger o acesso ao SQL Server. Com versões anteriores do SQL Server, as organizações com grandes instalações do SQL Server precisavam realizar esforço considerável para manter sua infraestrutura de certificado do SQL Server, geralmente desenvolvendo scripts e executando comandos manuais. Com o SQL Server 2019, o gerenciamento de certificados está integrado ao SQL Server Configuration Manager, simplificando tarefas comuns como: 

* Exibir e validar certificados instalados em uma instância do SQL Server. 
* Identificar quais certificados podem estar perto de expirar. 
* Implantar certificados em computadores do Grupo de Disponibilidade do nó que contém a réplica primária. 
* Implantar certificados entre computadores que participam de uma instância de Cluster de Failover do nó ativo.

> [!NOTE]
> Você pode usar gerenciamento de certificados no SQL Server Configuration Manager com versões anteriores do SQL Server, começando com o SQL Server 2008.

##  <a name="provision-single-server-cert"></a> Para instalar um certificado para uma única instância do SQL Server  
  
1. No SQL Server Configuration Manager, no painel de console, expanda **Configuração de Rede do SQL Server**.  
  
2. Clique com o botão direito do mouse em **Protocolos para** *&lt;nome da Instância&gt;* e selecione **Propriedades**.  
  
3. Escolha a guia **Certificado** e, em seguida, selecione **Importar**.  
  
4. Selecione **Procurar** e, em seguida, selecione o arquivo de certificado.  
  
5. Selecione **Avançar** para validar o certificado. Se não houver erros, selecione **Avançar** para importar o certificado para a instância local.  
  
 
##  <a name="provision-failover-cluster-cert"></a> Para instalar um certificado em uma configuração do Cluster de Failover  
  
1. No SQL Server Configuration Manager, no painel de console, expanda **Configuração de Rede do SQL Server**.
  
2. Clique com o botão direito do mouse em **Protocolos para** *&lt;nome da Instância&gt;* e escolha **Propriedades**. 

3. Escolha a guia **Certificado** e, em seguida, selecione **Importar**.

4. Selecione o tipo de certificado e se deseja importar para o nó atual ou para cada nó de cluster individual.

5. Se for instalar para um único nó, escolha **Procurar** e selecione o arquivo de certificado. Em seguida, vá para a etapa 8.

6. Se for instalar um certificado para cada nó, selecione **Avançar** para listar os possíveis nós do proprietário. Possíveis proprietários para o SQL Server FCI atual estão pré-selecionados.

7. Escolha **Avançar** para selecionar o certificado a ser importado.

8. Insira a senha quando solicitado. Procure quaisquer avisos ou erros após a validação.

9. Selecione **Avançar** para importar os certificados selecionados.

> [!NOTE]
> Conclua estas etapas no nó ativo da instância do Cluster de Failover do SQL Server. O usuário precisa ter permissões de administrador em todos os nós de cluster.

##  <a name="provision-availability-group-cert"></a>Para instalar um certificado em uma configuração de Grupo de Disponibilidade  
  
1. No SQL Server Configuration Manager, no painel de console, expanda **Configuração de Rede do SQL Server**.
  
2. Clique com o botão direito do mouse em **Protocolos para** *&lt;nome da Instância&gt;* e selecione **Propriedades**.  
  
3. Escolha a guia **Certificado** e, em seguida, selecione **Importar**.  
  
4. Escolha o tipo de certificado e selecione **Avançar** para selecionar na lista de Grupos de Disponibilidade conhecidos.  

5. Selecione **Avançar** para escolher certificados para cada nó de réplica. Os certificados devem ter um nome de arquivo que corresponda ao nome netbios dos nós.

6. Selecione **Avançar** para importar o certificado em cada nó.


> [!NOTE]
> Conclua estas etapas do nó que contém a réplica primária do Grupo de Disponibilidade. O usuário precisa ter permissões de administrador em todos os nós de cluster.

