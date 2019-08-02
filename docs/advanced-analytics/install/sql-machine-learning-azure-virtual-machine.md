---
title: Instalar a linguagem R e os recursos do Python em uma máquina virtual do Azure
description: Execute soluções R e Python data Science e Machine Learning em uma máquina virtual SQL Server na nuvem do Azure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b7aa37c3ec72390d76ecf9e939916f9641187956
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715880"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-on-an-azure-virtual-machine"></a>Instalar SQL Server Serviços de Machine Learning com R e Python em uma máquina virtual do Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Você pode instalar a integração do R e do Python com o Serviços de Machine Learning em uma máquina virtual SQL Server no Azure, eliminando tarefas de instalação e configuração. Depois que a máquina virtual é implantada, os recursos estão prontos para uso.
 
Para obter instruções passo a passo, consulte [como provisionar uma máquina virtual do Windows SQL Server no portal do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision).

A etapa [definir configurações do SQL Server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings) é onde você adiciona o aprendizado de máquina à sua instância.

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>Desbloquear o firewall

Por padrão, o firewall na máquina virtual do Azure inclui uma regra que bloqueia o acesso à rede para contas de usuário local.

Você deve desabilitar essa regra para garantir que você possa acessar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância de um cliente de ciência de dados remoto.  Caso contrário, o código de aprendizado de máquina não poderá ser executado em contextos de computação que usam o espaço de trabalho da máquina virtual.

Para habilitar o acesso de clientes de ciência de dados remotos:

1. Na máquina virtual, abra o Firewall do Windows com Segurança Avançada.
2. Selecione **Regras de Saída**
3. Desabilite a regra a seguir:
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>Habilitar retornos de chamada ODBC para clientes remotos

Se você espera que os clientes que chamam o servidor precisem emitir consultas ODBC como parte de suas soluções de aprendizado de máquina, você deve garantir que o Launchpad possa fazer chamadas ODBC em nome do cliente remoto. 

Para fazer isso, você deve permitir que as contas de trabalho do SQL que são usadas pelo Launchpad façam logon na instância. Para obter mais informações, consulte [Adicionar SQLRUserGroup como um usuário de banco de dados](../security/create-a-login-for-sqlrusergroup.md).

<a name="network"></a>

## <a name="add-network-protocols"></a>Adicionar protocolos de rede

+ Habilitar pipes nomeados
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa o protocolo de Pipes Nomeados para conexões entre os computadores cliente e servidor, além de algumas conexões internas. Se a opção Pipes Nomeados não estiver habilitada, instale e habilite-a tanto na máquina virtual do Azure quanto quaisquer clientes de ciência de dados que se conectem ao servidor.
  
+ Habilitar TCP/IP

  O TCP/IP é necessário para conexões de loopback. Se você receber o erro "DBNETLIB; SQL Server não existe ou acesso negado ", habilite o TCP/IP na máquina virtual que dá suporte à instância.