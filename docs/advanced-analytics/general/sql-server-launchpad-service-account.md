---
title: Configuração de conta de serviço do Launchpad do SQL Server | Microsoft Docs
description: Como modificar a conta de serviço do Launchpad do SQL Server usada para a execução do script externo no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0afdb02c578de92bc91c5f47e973148136ebd919
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43892845"
---
# <a name="sql-server-launchpad-service-configuration"></a>Configuração do serviço Launchpad do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Um separado [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] serviço é criado para a instância do mecanismo de banco de dados ao qual você adicionou a integração (R ou Python) de aprendizado de máquina do SQL Server.

## <a name="service-account-configuration"></a>Configuração da conta de serviço

Por padrão, o Launchpad do SQL Server está configurado para ser executado sob **NT Service\MSSQLLaunchpad**, que é provisionado com todas as permissões necessárias para executar scripts externos. Removendo permissões desta conta pode resultar em Launchpad Falha ao iniciar ou acessar a instância do SQL Server em que os scripts externos devem ser executados.

Permissão necessária para esta conta estão listados abaixo. Se você modificar a conta de serviço, certifique-se de usar o **política de segurança Local** aplicativo para incluir estas permissões:

+ Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)
+ Ignorar verificação completa (SeChangeNotifyPrivilege)
+ Fazer logon como um serviço (SeServiceLogonRight)
+ Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)

Para obter mais informações sobre as permissões necessárias para executar serviços SQL Server, consulte [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>Propriedades de configuração

1. Abra [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md). 

2. Launchpad do SQL Server com o botão direito e selecione **propriedades**.

    + Para alterar a conta de serviço, clique o **fazer logon** guia.

    + Para aumentar o número de usuários, clique o **avançado** guia.

> [!Note]
> Em versões anteriores do SQL Server 2016 R Services, você pode alterar algumas propriedades do serviço, editando o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] arquivo de configuração. Esse arquivo não é usado para alterar as configurações. SQL Server Configuration Manager é a abordagem correta para que as alterações de configuração de serviço, como a conta de serviço e o número de usuários.

#### <a name="debug-settings"></a>Configurações de depuração

Algumas propriedades só podem ser alteradas usando o arquivo de configuração da barra inicial, que pode ser útil em casos limitados, como a depuração. O arquivo de configuração é criado durante a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instalação e por padrão é salvo como um arquivo de texto sem formatação no seguinte local: `<instance path>\binn\rlauncher.config`

Você deve ser um administrador no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer alterações nesse arquivo. Se você editar o arquivo, é recomendável que você faça uma cópia de backup antes de salvar as alterações.

A tabela a seguir lista as configurações avançadas para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], com os valores permitidos. 

|**Nome da configuração**|**Tipo**|**Descrição**|
|----|----|----|
|TRABALHO\_LIMPEZA\_ON\_SAIR|Integer |Isso é uma configuração interna apenas, não altere esse valor. </br></br>Especifica se a pasta de trabalho temporária criada para cada sessão de tempo de execução externos deve ser limpos após o término da sessão. Essa configuração é útil para depuração. </br></br>Valores com suporte são **0** (desativado) ou **1** (habilitado). </br></br>O padrão é 1, arquivos de log do significado são removidos ao sair.|
|RASTREAMENTO\_NÍVEL|Integer |Configura o nível de detalhamento do rastreamento de MSSQLLAUNCHPAD para fins de depuração. Isso afeta os arquivos de rastreamento no caminho especificado pela configuração LOG_DIRECTORY. </br></br>Valores com suporte são: **1** (erro), **2** (desempenho), **3** (aviso) **4** (informações). </br></br>O padrão é 1, que significa que somente os avisos de saída.|

Todas as configurações assumem a forma de um par chave-valor, com cada configuração em uma linha separada. Por exemplo, para alterar o nível de rastreamento, você adicionaria a linha `Default: TRACE_LEVEL=4`.

## <a name="see-also"></a>Confira também

[Estrutura de extensibilidade](../concepts/extensibility-framework.md)
