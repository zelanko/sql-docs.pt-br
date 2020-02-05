---
title: Configurar o SSIS no Linux com ssis-conf
description: Este artigo descreve como agendar pacotes SSIS (SQL Server Integration Services) no Linux com o utilitário ssis-conf.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 51dc2ba27e346dea75f1bd347491d4932695fd43
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68077529"
---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>Configurar o SQL Server Integration Services no Linux com ssis-conf

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Você executa o script de configuração `ssis-conf` ao instalar o SSIS (SQL Server Integration Services) para Red Hat Enterprise Linux e Ubuntu. Para obter mais informações sobre a instalação do SSIS, confira [Instalar o SSIS (SQL Server Integration Services) no Linux](sql-server-linux-setup-ssis.md).

Você também pode usar o utilitário `ssis-conf` para configurar as seguintes propriedades:

| Comando | DESCRIÇÃO |
|-------------|---------------------------------------------------------------------|
| set-edition | Definir a edição do SQL Server                                       |
| telemetria   | Habilitar ou desabilitar o serviço de telemetria do SQL Server Integration Services |
| instalação       | Inicializar e configurar o Microsoft SQL Server Integration Services      |
|||

## <a name="run-ssis-conf"></a>Executar ssis-conf

Os exemplos neste artigo executam `ssis-conf` especificando o caminho completo: `/opt/ssis/bin/ssis-conf`. Se navegar até essa localização antes de executar `ssis-conf`, você poderá executar o utilitário no contexto do diretório atual: `./ssis-conf`.

É preciso que você execute os comandos que são descritos neste artigo com privilégios de raiz. Por exemplo, execute `sudo /opt/ssis/bin/ssis-conf setup` e não `/opt/ssis/bin/ssis-conf setup`.

Para executar esses comandos com prompts no idioma de sua preferência, você pode especificar uma localidade. Por exemplo, para receber prompts em chinês, execute o seguinte comando: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>Use set-edition para definir a edição do SQL Server Integration Services

A edição do SSIS está alinhada com a edição do SQL Server.

Digite o comando a seguir: `$ sudo /opt/ssis/bin/ssis-conf set-edition`.

Depois de inserir o comando, você receberá o seguinte prompt:

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

Se você inserir um valor de 1 a 7, o sistema configurará uma edição gratuita ou paga. Se você inserir 8, o utilitário solicitará que você insira a chave do produto (Product Key) que adquiriu:

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>Usar telemetria para configurar comentários do cliente

O comando `telemetry` determina se o SSIS envia comentários à Microsoft.

Para edições gratuitas (ou seja, edições Express, Developer e Evaluation), o serviço de telemetria está sempre habilitado. Se tiver uma edição gratuita, você não poderá usar o comando `telemetry` para desabilitar a telemetria.

Digite o comando a seguir: `$ sudo /opt/ssis/bin/ssis-conf telemetry`.

Para edições pagas, depois de inserir o comando, você receberá o seguinte prompt:

```
Send feature usage data to Microsoft. Feature usage data includes information about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

Se você selecionar **Sim**, o serviço de telemetria será habilitado e começará a executar. O serviço iniciará automaticamente após cada inicialização. Se você selecionar **Não**, o serviço de telemetria será interrompido e desabilitado.

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>Use a instalação para inicializar e configurar o Microsoft SQL Server Integration Services

Use o comando `setup` toda vez que você instalar o SSIS.

Digite o comando a seguir: `sudo /opt/ssis/bin/ssis-conf setup`.

O utilitário solicita que você reconheça ou forneça valores para os itens a seguir:
-   Licença do produto
-   Contrato EULA
-   Serviço de telemetria
-   A linguagem usada pelo Integration Services

Para executar o comando `setup` com prompts no idioma de sua preferência, você pode especificar uma localidade. Por exemplo, para receber prompts em chinês, execute o seguinte comando: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="ssisconf-format"></a>Formato ssis.conf

O arquivo `/var/opt/ssis/ssis.conf` a seguir fornece um exemplo para cada configuração.

Para o SQL Server, você pode alterar as configurações do sistema alterando os valores no arquivo `mssql.conf`. Para o SSIS, você *não pode* alterar as configurações do sistema alterando os valores no arquivo `ssis.conf`. O arquivo `ssis.conf` mostra somente os resultados da instalação. Se você quiser alterar as configurações do SSIS, poderá excluir o arquivo `ssis.conf` e executar o comando `setup` novamente.

Aqui está um arquivo `ssis.conf` de exemplo. Cada campo corresponde ao resultado de uma etapa da instalação.

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

## <a name="related-content-about-ssis-on-linux"></a>Conteúdo relacionado sobre o SSIS no Linux
-   [Extrair, transformar e carregar dados no Linux com o SSIS](sql-server-linux-migrate-ssis.md)
-   [Instalar o SSIS (SQL Server Integration Services) no Linux](sql-server-linux-setup-ssis.md)
-   [Limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md)
-   [Agendar a execução de pacotes do SQL Server Integration Services no Linux com cron](sql-server-linux-schedule-ssis-packages.md)
