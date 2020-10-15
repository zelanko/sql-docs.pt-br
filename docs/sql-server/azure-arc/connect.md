---
title: Conecte-se ao Azure Arc
titleSuffix: ''
description: Conectar uma instância do SQL Server com o Azure Arc
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: d5b66ac431bfadff06c930f76517f35d95dcb12f
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987992"
---
# <a name="connect-your-sql-server-to-azure-arc"></a>Conectar o SQL Server ao Azure Arc

Você pode conectar a instância do SQL Server local com o Azure Arc seguindo estas etapas.

## <a name="prerequisites"></a>Pré-requisitos

* Seu computador precisa ter pelo menos uma instância do SQL Server instalada
* Para computadores Windows, o Azure PowerShell precisa estar instalado. Siga as instruções para [instalar o Azure PowerShell](/powershell/azure/install-az-ps).
* Para computadores Linux, você precisa ter baixado a CLI do Azure e conectado-se usando sua conta do Azure. Siga as instruções para [instalar a CLI do Azure](/cli/azure/install-azure-cli-apt).


## <a name="generate-a-registration-script-for-sql-server"></a>Gerar um script de registro para o SQL Server

Nesta etapa, você gera um script que descobre todas as instâncias do SQL Server instaladas no computador e registra-as como recursos __SQL Server – Azure Arc__. Se o computador físico ou a máquina virtual host não estiver registrada no Azure Arc, o script a registrará automaticamente.

1. Procure o tipo de recurso __SQL Server – Azure Arc__ e adicione outro por meio da folha de criação.

![Iniciar a criação](media/join/start-creation-of-sql-server-azure-arc-resource.png)
    
2. Examine os pré-requisitos e acesse a guia **Detalhes do servidor**.  

3. Selecione a assinatura, o grupo de recursos, a região do Azure e o sistema operacional do host. Se necessário, especifique também o proxy que sua rede usa para conectar-se com a Internet.

> [!IMPORTANT]
> Se o computador que hospeda a instância do SQL Server já estiver [conectado ao Azure Arc](/azure/azure-arc/servers/onboard-portal), selecione o mesmo grupo de recursos que contém o recurso __Computador – Azure Arc__ correspondente.

![Detalhes do servidor](media/join/server-details-sql-server-azure-arc.png)

4. Acesse a guia **Executar script** e baixe o script de registro exibido. O portal gera o script para o sistema operacional do host que você especificou.

![Baixar script](media/join/download-script-sql-server-azure-arc.png)

## <a name="connect-the-installed-sql-server-instances-to-azure-arc"></a>Conectar as instâncias do SQL Server instaladas com o Azure Arc

Nesta etapa, você obterá o script baixado do portal do Azure e o executará no computador físico ou na máquina virtual de destino. Como resultado, cada instância do SQL Server instalada no computador será registrada como um recurso __SQL Server – Azure Arc__. Além disso, se o agente de configuração de convidado não estiver instalado nos computadores em si, ele será instalado automaticamente e registrado como um recurso __Computador – Azure Arc__.

> [!NOTE]
> Execute o script usando uma conta que atenda aos requisitos mínimos de permissão descritos em [Pré-requisitos](overview.md#prerequisites).

### <a name="windows"></a>Windows

1. Inicie uma instância de administrador do __powershell.exe__ e entre no módulo do PowerShell com suas credenciais do Azure. Siga as [instruções de entrada](/powershell/azure/install-az-ps#sign-in).

2. Executar o script baixado

   ```powershell
   & '.\RegisterSqlServerArc.ps1'
   ```

   > [!NOTE]
   > Na primeira vez, poderá haver problemas se você ainda não tiver instalado o módulo AZ para PowerShell. Nesse caso, siga as instruções no script para instalar e conectar sua conta e execute o script novamente.

### <a name="linux"></a>Linux

1. Use a CLI do Azure para entrar com suas credenciais do Azure. Siga as [instruções de entrada](/cli/azure/authenticate-azure-cli)

2. Conceda a permissão de execução para o script baixado e execute-o.

   ```bash
   sudo chmod +x ./RegisterSqlServerArc.sh
   ./RegisterSqlServerArc.sh
   ```

## <a name="register-sql-server-instances-on-multiple-machines"></a>Registrar as instâncias do SQL Server em vários computadores

Você pode conectar várias instâncias do SQL Server instaladas em vários computadores Windows ou Linux ao Azure Arc usando o mesmo script que gerou para um único computador. Siga as instruções de como [conectar as instâncias do SQL Server ao Azure Arc em escala](connect-at-scale.md).

## <a name="validate-the-sql-server---azure-arc-resources"></a>Validar os recursos SQL Server – Azure Arc

Acesse o [portal do Azure](https://ms.portal.azure.com/#home) e abra o recurso __SQL Server – Azure Arc__ recém-registrado a ser validado.

![Validar o SQL Server conectado ](media/join/validate-sql-server-azure-arc.png)

## <a name="un-register-the-sql-server---azure-arc-resources"></a>Cancelar o registro dos recursos SQL Server – Azure Arc

Para remover um recurso __SQL Server – Azure Arc__ existente, acesse o grupo de recursos que o contém e remova-o da lista de recursos no grupo.

![Cancelar o registro do SQL Server](media/join/delete-sql-server-azure-arc.png)

## <a name="next-steps"></a>Próximas etapas

* [Configurar a segurança de dados avançada para a instância do SQL Server](configure-advanced-data-security.md)

* [Configurar a avaliação do SQL sob demanda para a instância do SQL Server](assess.md)