---
title: Instalar em uma máquina virtual do Azure
description: Execute soluções de aprendizado de máquina e de ciência de dados do R e do Python em uma máquina virtual do SQL Server na nuvem do Azure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: aeec25b561822e8083b89e03f0f7e74f40660f7b
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727618"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-on-an-azure-virtual-machine"></a>Instalar os Serviços de Machine Learning do SQL Server com R e Python em uma máquina virtual do Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Você pode instalar a integração do R e do Python com os Serviços de Machine Learning em uma máquina virtual do SQL Server no Azure, eliminando as tarefas de instalação e configuração. Depois que a máquina virtual for implantada, os recursos estarão prontos para uso.
 
Para obter instruções passo a passo, confira [Como provisionar uma máquina virtual do SQL Server do Windows no portal do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision).

É na etapa [Definir configurações do SQL Server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings) que você adiciona o aprendizado de máquina à sua instância.

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>Desbloquear o firewall

Por padrão, o firewall na máquina virtual do Azure inclui uma regra que bloqueia o acesso de rede para contas de usuários locais.

Você precisa desabilitar essa regra para assegurar que você possa acessar a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um cliente de ciência de dados remotos.  Caso contrário, o código de aprendizado de máquina não poderá ser executado em contextos de computação que usem o workspace da máquina virtual.

Para habilitar o acesso de clientes de ciência de dados remotos:

1. Na máquina virtual, abra o Firewall do Windows com Segurança Avançada.
2. Selecione **Regras de Saída**
3. Desabilite a regra a seguir:
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>Habilitar retornos de chamada ODBC para clientes remotos

Se você esperar que clientes que chamam o servidor precisem emitir consultas ODBC como parte das respectivas soluções de aprendizado de máquina, você deverá assegurar que o Launchpad possa fazer chamadas ODBC em nome do cliente remoto. 

Para fazer isso, você deve permitir que as contas de trabalho do SQL que são usadas pelo Launchpad façam logon na instância. Para obter mais informações, confira [Adicionar SQLRUserGroup como um usuário de banco de dados](../security/create-a-login-for-sqlrusergroup.md).

<a name="network"></a>

## <a name="add-network-protocols"></a>Adicionar protocolos de rede

+ Habilitar pipes nomeados
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa o protocolo de Pipes Nomeados para conexões entre os computadores cliente e servidor, além de algumas conexões internas. Se a opção Pipes Nomeados não estiver habilitada, instale e habilite-a tanto na máquina virtual do Azure quanto quaisquer clientes de ciência de dados que se conectem ao servidor.
  
+ Habilitar TCP/IP

  O TCP/IP é necessário para conexões de loopback. Se você receber o erro "DBNETLIB; o SQL Server não existe ou acesso negado", habilite TCP/IP na máquina virtual que dá suporte à instância.