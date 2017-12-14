---
title: "Configuração de protocolo de rede padrão do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 07/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- protocols [SQL Server], default settings
- default protocols, after install
ms.assetid: 635ea361-a797-4971-bd05-e3415862bc5c
caps.latest.revision: "4"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d56a9141ce472f9419eca3504dae859dab886689
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="default-sql-server-network-protocol-configuration"></a>Configuração de protocolo de rede padrão do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Para melhorar a segurança, o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] desabilita a conectividade de rede para algumas instalações novas. A conectividade de rede usando TCP/IP não será desabilitada se você estiver usando a edição Enterprise, Standard, Evaluation ou Workgroup ou se houver uma instalação prévia do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Em todas as instalações, o protocolo de memória compartilhada é habilitado para permitir conexões locais com o servidor. O serviço Navegador do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] pode ser parado, dependendo de condições e opções da instalação.

Use o nó Configuração de Rede do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Configuration Manager para configurar os protocolos de rede após a instalação. Use o nó Serviços do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Configuration Manager para configurar o serviço [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Browser para ser iniciado automaticamente. Para obter mais informações, consulte [Habilitar ou desabilitar um protocolo de rede de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).


## <a name="default-configuration"></a>Configuração padrão

A tabela a seguir descreve a configuração após a instalação.

Edição | Nova instalação versus instalação anterior está presente | Memória compartilhada | TCP/IP    | Pipes nomeados
| -------- | -- | -- | -- | --  |  
Enterprise  | Nova instalação  | Ativado   | Ativado   | Desabilitado para conexões de rede.
Standard    | Nova instalação  | Ativado   | Ativado   | Desabilitado para conexões de rede.
Web | Nova instalação  | Ativado   | Ativado   | Desabilitado para conexões de rede.
Desenvolvedor   | Nova instalação  | Ativado   | Desabilitado  | Desabilitado para conexões de rede.
Evaluation  | Nova instalação  | Ativado   | Ativado   | Desabilitado para conexões de rede.
SQL Server Express  | Nova instalação  | Ativado   | Desabilitado  | Desabilitado para conexões de rede.
Todas as edições    | A instalação anterior está presente, mas não está sendo atualizada.   | Igual à nova instalação  | Igual à nova instalação  | Igual à nova instalação
Todas as edições    | Atualizar   | Ativado   | As configurações da instalação anterior são preservadas.    | As configurações da instalação anterior são preservadas.


>[!NOTE]
> Se a instância estiver sendo executada em um cluster de failover do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], ela escutará nas portas de cada endereço IP selecionado para o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] durante a instalação do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
 
>[!NOTE]
> Ao instalar o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] com argumentos de prompt de comando, é possível especificar os protocolos que devem ser habilitados usando os parâmetros `TCPENABLED` e `NPENABLED` . Para obter mais informações, consulte [Instalar o SQL Server por meio do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).

## <a name="creating-a-connection-string"></a>Criando uma cadeia de conexão

Consulte os seguintes tópicos para obter amostras de cadeias de conexão:
* [Criando uma cadeia de conexão válida usando o protocolo de memória compartilhada](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)
* [Criando uma cadeia de conexão válida usando TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)



## <a name="includessnoversionmdincludesssnoversion-mdmd-browser-settings"></a>[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Configurações do navegador

O serviço Navegador do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] pode ser configurado para ser iniciado automaticamente durante a instalação. O padrão é para iniciar automaticamente nas seguintes condições:

* Quando uma instalação é atualizada.
* Durante a instalação lado a lado com outra instância do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
* Quando um cluster é instalado.
* Ao instalar uma instância nomeada do Mecanismo de Banco de Dados, incluindo todas as instâncias do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Express.
* Ao instalar uma instância nomeada do Analysis Services.

## <a name="see-also"></a>Consulte também

[Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)

[Configuração da Área de Superfície](../../relational-databases/security/surface-area-configuration.md)  



