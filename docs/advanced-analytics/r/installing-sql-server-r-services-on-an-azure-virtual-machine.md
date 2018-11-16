---
title: Instalar serviços do SQL Server Machine Learning com R e Python em uma máquina virtual do Azure | Microsoft Docs
description: Executar soluções em uma máquina de virtual do SQL Server na nuvem do Azure de aprendizado de máquina e de ciência de dados R e Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e416b99c3d4597cb2fe9346819184be43cd98402
ms.sourcegitcommit: ef6e3ec273b0521e7c79d5c2a4cb4dcba1744e67
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2018
ms.locfileid: "51512691"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-on-an-azure-virtual-machine"></a>Instalar serviços do SQL Server Machine Learning com R e Python em uma máquina virtual do Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Você pode instalar a integração de R e Python com os serviços de aprendizado de máquina em uma máquina de virtual do SQL Server no Azure, eliminando as tarefas de instalação e configuração. Depois que a máquina virtual é implantada, os recursos estão prontos para uso.
 
Para obter instruções passo a passo, consulte [como provisionar uma máquina de virtual do Windows SQL Server no portal do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision).

O [configurações de configurar o SQL server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#4-configure-sql-server-settings) etapa é onde adicionar o aprendizado de máquina para sua instância.

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>Desbloquear o firewall

Por padrão, o firewall na máquina virtual do Azure inclui uma regra que bloqueia o acesso para contas de usuário local de rede.

Você deve desabilitar essa regra para garantir que você pode acessar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância de um cliente de ciência de dados remoto.  Caso contrário, o código de aprendizado de máquina não é possível executar em contextos de computação que usam o espaço de trabalho da máquina virtual.

Para habilitar o acesso de clientes de ciência de dados remotos:

1. Na máquina virtual, abra o Firewall do Windows com Segurança Avançada.
2. Selecione **Regras de Saída**
3. Desabilite a regra a seguir:
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>Habilitar retornos de chamada ODBC para clientes remotos

Se você espera que os clientes que chamam o servidor precisará emitir consultas ODBC como parte de sua soluções de aprendizado de máquina, você deve garantir que o Launchpad possa fazer chamadas ODBC em nome do cliente remoto. 

Para fazer isso, você deve permitir que as contas de trabalho do SQL que são usadas pelo Launchpad façam logon na instância. Para obter mais informações, consulte [adicionar SQLRUserGroup como um usuário de banco de dados](../security/add-sqlrusergroup-to-database.md).

<a name="network"></a>

## <a name="add-network-protocols"></a>Adicionar protocolos de rede

+ Habilitar pipes nomeados
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa o protocolo de Pipes Nomeados para conexões entre os computadores cliente e servidor, além de algumas conexões internas. Se a opção Pipes Nomeados não estiver habilitada, instale e habilite-a tanto na máquina virtual do Azure quanto quaisquer clientes de ciência de dados que se conectem ao servidor.
  
+ Habilitar TCP/IP

  TCP/IP é necessário para conexões de loopback. Se você receber o erro "DBNETLIB; SQL Server não existe ou acesso negado", habilitar TCP/IP na máquina virtual que oferece suporte a instância.