---
title: Configurar o SSIS no Linux com o ssis-conf | Microsoft Docs
description: Este artigo descreve como configurar o SQL Server Integration Services (SSIS) no Linux com o utilitário de ssis-conf.
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 67144e934914549fbb2605b660407c826c409880
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38020633"
---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>Configurar o SQL Server Integration Services no Linux com o ssis-conf

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Executar o `ssis-conf` script de configuração quando você instala o SQL Server Integration Services (SSIS) para o Red Hat Enterprise Linux e Ubuntu. Para obter mais informações sobre como instalar o SSIS, consulte [instalar o SQL Server SSIS (Integration Services) no Linux](sql-server-linux-setup-ssis.md).

Você também pode usar o `ssis-conf` utilitário para configurar as propriedades a seguir:

| Comando | Description |
|-------------|---------------------------------------------------------------------|
| edição de conjunto | Defina a edição do SQL Server                                       |
| Telemetria   | Habilitar ou desabilitar o serviço de telemetria do SQL Server Integration Services |
| instalação       | Inicializar e configurar o Microsoft SQL Server Integration Services      |
|||

## <a name="run-ssis-conf"></a>Executar o ssis-conf

Os exemplos neste artigo executados `ssis-conf` , especificando o caminho completo: `/opt/ssis/bin/ssis-conf`. Se você navegar para esse local antes de executar `ssis-conf`, você pode executar o utilitário no contexto do diretório atual: `./ssis-conf`.

Certifique-se de executar os comandos descritos neste artigo com privilégios de raiz. Por exemplo, execute `sudo /opt/ssis/bin/ssis-conf setup` e não `/opt/ssis/bin/ssis-conf setup`.

Para executar esses comandos com prompts no idioma que você preferir, você pode especificar uma localidade. Por exemplo, para receber solicitações em chinês, execute o seguinte comando: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>Use set-edition para definir a edição do SQL Server Integration Services

A edição do SSIS é alinhada com a edição do SQL Server.

Digite o seguinte comando: `$ sudo /opt/ssis/bin/ssis-conf set-edition`.

Depois de inserir o comando, você receberá a seguinte solicitação:

```
Choose an edition of SQL Server:

1) Evaluation (free, no production use rights, 180-day limit)

2) Developer (free, no production use rights)

3) Express (free)

4) Web (PAID)

5) Standard (PAID)

6) Enterprise (PAID)

7) Enterprise Core (PAID)

8) I bought a license through a retail sales channel and have a product key to enter.

Details about editions can be found at https://go.microsoft.com/fwlink/?LinkId=852748&clcid=0x409.

Use of PAID editions of this software requires separate licensing through a Microsoft Volume Licensing program.

By choosing a PAID edition, you are verifying that you have the appropriate number of licenses in place to install and run this software.

Enter your edition (1-8):
```

Se você inserir um valor de 1 a 7, o sistema configura uma edição gratuita ou paga. Se você inserir 8, o utilitário solicita que você insira a chave de produto que você comprou:

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>Usar a telemetria para configurar os comentários dos clientes

O `telemetry` comando determina se o SSIS envia comentários à Microsoft.

Para as edições gratuitas (ou seja, as edições Evaluation, Developer e Express), o serviço de telemetria está sempre habilitado. Se você tiver uma edição gratuita, você não pode usar o `telemetry` comando para desabilitar a telemetria.

Digite o seguinte comando: `$ sudo /opt/ssis/bin/ssis-conf telemetry`.

Para edições pagas, depois de inserir o comando, você receberá a seguinte solicitação:

```
Send feature usage data to Microsoft. Feature usage data includes information about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

Se você selecionar **Sim**, o serviço de telemetria está habilitado e começa a ser executado. O serviço é iniciado automaticamente após cada inicialização. Se você selecionar **não**, o serviço de telemetria para e está desabilitada.

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>Use a instalação para inicializar e configurar o Microsoft SQL Server Integration Services

Use o `setup` comando sempre que você instale o SSIS.

Digite o seguinte comando: `sudo /opt/ssis/bin/ssis-conf setup`.

O utilitário solicita que você confirmar ou fornecer valores para os seguintes itens:
-   Licença do produto
-   Termos de licença
-   Serviço de telemetria
-   O idioma usado pelo Integration Services

Para executar o `setup` comando prompts no idioma que você preferir, você pode especificar uma localidade. Por exemplo, para receber solicitações em chinês, execute o seguinte comando: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="ssisconf-format"></a>formato de SSIS.conf

O seguinte `/var/opt/ssis/ssis.conf` arquivo fornece um exemplo para cada configuração.

Para o SQL Server, você pode alterar as configurações do sistema, alterando os valores no `mssql.conf` arquivo. Para o SSIS, você *não é possível* alterar configurações do sistema, alterando os valores no `ssis.conf` arquivo. O `ssis.conf` arquivo mostra apenas os resultados da instalação. Se você quiser alterar as configurações para o SSIS, você pode excluir o `ssis.conf` do arquivo e execute o `setup` comando novamente.

Aqui está um exemplo `ssis.conf` arquivo. Cada campo corresponde ao resultado de uma etapa de instalação.

```
[LICENSE]
                       
registered = Y        
                       
pid = enterprisecore  
                       
[EULA]
                       
accepteula = Y        
                       
[TELEMETRY]
                       
enabled = Y           
                       
[language]
                       
lcid = 2052
```

## <a name="related-content-about-ssis-on-linux"></a>Conteúdo relacionado sobre SSIS no Linux
-   [Extrair, transformar e carregar dados em Linux com o SSIS](sql-server-linux-migrate-ssis.md)
-   [Instalar o SQL Server Integration Services (SSIS) no Linux](sql-server-linux-setup-ssis.md)
-   [Limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md)
-   [SQL Server Integration Services de agenda a execução no Linux com cron do pacote](sql-server-linux-schedule-ssis-packages.md)
