---
title: Configuração de rede do servidor | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Named Pipes [SQL Server], configuring
- connections [SQL Server], server network configuration
- Database Engine [SQL Server], network configurations
- server network configuration [SQL Server]
- protocols [SQL Server], choosing
- ports [SQL Server], changing
- server configuration [SQL Server]
ms.assetid: 890c09a1-6dad-4931-aceb-901c02ae34c5
caps.latest.revision: 50
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 43467af34ad8e6fde2fc8874ace1e6f7f2fa17e5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32870101"
---
# <a name="server-network-configuration"></a>Configuração de rede do servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Tarefas de configuração de rede do servidor incluem habilitação de protocolos, modificação de porta ou pipe usado por um protocolo, criptografia de configuração, configuração do serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , exposição ou ocultação do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] na rede e registro do Nome do Principal do Servidor. Na maioria das vezes, não é necessário alterar a configuração de rede do servidor. Só reconfigure os protocolos de rede do servidor se houver requisitos de rede especiais.  
  
 A configuração da rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é realizada usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o Utilitário de Rede do Servidor fornecido com esses produtos.  
  
## <a name="protocols"></a>Protocolos  
 Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para habilitar ou desabilitar os protocolos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e configurar as opções disponíveis para os protocolos. É possível habilitar mais de um protocolo. É necessário habilitar todos os protocolos que você deseja que os clientes usem. Todos os protocolos têm acesso idêntico ao servidor. Para obter informações sobre quais protocolos devem ser usados, consulte [Habilitar ou desabilitar um protocolo de rede de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md) e [Configuração de protocolo de rede padrão do SQL Server](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md).  
  
### <a name="changing-a-port"></a>Alterando uma porta  
 É possível configurar o protocolo TCP/IP e VIA para escutar em uma porta designada. Por padrão, a instância padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)] escuta na porta TCP 1433. As instâncias nomeadas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e do [!INCLUDE[ssEW](../../includes/ssew-md.md)] são configuradas para portas dinâmicas. Isso significa que elas selecionam uma porta disponível quando o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado. O serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajuda os clientes a identificar a porta no momento da conexão.  
  
 Quando configurado para portas dinâmicas, a porta usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá ser alterada sempre que o programa for iniciado. Ao conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por um firewall, é necessário abrir a porta usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Configure o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usar uma porta específica, assim você pode configurar o firewall para permitir a comunicação com o servidor. Para obter mais informações, veja [Configurar um servidor para escuta em uma porta TCP específica &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
### <a name="changing-a-named-pipe"></a>Alterando um pipe nomeado  
 É possível configurar o protocolo de pipe nomeado para escutar em um pipe nomeado designado. Por padrão, a instância padrão do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] escuta no pipe \\\\.\pipe\sql\query da instância padrão e \\\\.\pipe\MSSQL$*\<instancename>* \sql\query de uma instância nomeada. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] pode escutar somente em um pipe nomeado, mas, se desejar, é possível alterar o pipe para outro nome. O serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajuda os clientes a identificar o pipe no momento da conexão. Para obter mais informações, veja [Como configurar um servidor para escuta em um pipe alternativo &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-an-alternate-pipe.md).  
  
## <a name="force-encryption"></a>Forçar criptografia  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] pode ser configurado para exigir criptografia ao comunicar-se com aplicativos cliente. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
## <a name="extended-protection-for-authentication"></a>Proteção Estendida para Autenticação  
 O suporte à Proteção Estendida para Autenticação usando associação de canal e associação de serviço está disponível para sistemas operacionais que dão suporte à Proteção Estendida. Para obter mais informações, veja [Conectar-se ao mecanismo de banco de dados usando proteção estendida](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md).  
  
## <a name="authenticating-by-using-kerberos"></a>Autenticando usando o Kerberos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à autenticação Kerberos. Para obter mais informações, veja [Registrar um nome da entidade de serviço para conexões de Kerberos](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md) e [Microsoft Kerberos Configuration Manager para SQL Server](http://www.microsoft.com/download/details.aspx?id=39046).  
  
### <a name="registering-a-server-principal-name-spn"></a>Registrando um SPN (Nome da Entidade de Serviço)  
 O serviço de autenticação Kerberos usa um SPN para autenticar um serviço. Para obter mais informações, veja [Registrar um nome de entidade de serviço para conexões de Kerberos](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).  
  
 Também podem ser usados SPNs para fazer autenticação de cliente mais segura ao conectar-se com NTLM. Para obter mais informações, veja [Conectar-se ao mecanismo de banco de dados usando proteção estendida](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md).  
  
## <a name="sql-server-browser-service"></a>SQL Server Browser Service  
 O serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado no servidor e ajuda computadores cliente a encontrar instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não é necessário configurar o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas é necessário estar em execução em alguns cenários de conexão. Para obter mais informações sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser, veja [Serviço SQL Server Browser &#40;Mecanismo de Banco de Dados e SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)  
  
## <a name="hiding-sql-server"></a>Ocultando o SQL Server  
 Em execução, o Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] responde a consultas, com nome, versão e informações de conexão para cada instância instalada. Para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o sinalizador do **HideInstance** indica que o Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não deve responder com informações sobre essa instância do servidor. Aplicativos cliente ainda podem conectar, mas devem saber as informações de conexão exigidas. Para obter mais informações, veja [Ocultar uma instância do Mecanismo de Banco de Dados do SQL Server](../../database-engine/configure-windows/hide-an-instance-of-sql-server-database-engine.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Configuração de rede de cliente](../../database-engine/configure-windows/client-network-configuration.md)  
  
 [Gerenciar os serviços do Mecanismo de Banco de Dados](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  
