---
title: Configurar SSIS em Linux com o ssis conf | Microsoft Docs
description: "Este artigo mostra como configurar o SQL Server Integration Services em Linux com o utilitário de conferência do ssis."
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.date: 09/26/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 46327772e8c22f76770bc51f72817ceedffae469
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>Configurar o SQL Server Integration Services no Linux com conf ssis

`ssis-conf`é um script de configuração que é quando você instala o SQL Server Integration Services (SSIS) para Red Hat Enterprise Linux e Ubuntu. Você pode usar esse utilitário para configurar as seguintes propriedades:

| Comando | Description |
|-------------|---------------------------------------------------------------------|
| edição de conjunto | Definir a edição do SQL Server                                       |
| Telemetria   | Habilitar ou desabilitar o serviço de telemetria do SQL Server Integration Services |
| instalação       | Inicializar e configurar o Microsoft SQL Server Integration Services      |
|||

## <a name="how-to-run-ssis-conf"></a>A execução de ssis conf

Os exemplos neste artigo executar `ssis-conf` ao especificar o caminho completo: `/opt/ssis/bin/ssis-conf`. Se você navegar para o caminho antes de executar `ssis-conf`, você pode executá-lo no contexto do diretório atual: `./ssis-conf`.

Certifique-se de que você execute os comandos descritos neste artigo com privilégios de raiz. Por exemplo, execute `sudo /opt/ssis/bin/ssis-conf setup` e não `/opt/ssis/bin/ssis-conf setup`.

Para executar esses comandos com avisos no idioma que você preferir, você pode especificar uma localidade. Por exemplo, para ver avisos em chinês, execute o seguinte comando:

`sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>Usar a edição de conjunto para definir a edição do SQL Server Integration Services

A edição do SSIS é alinhada com a edição do SQL Server.

Insira o seguinte comando:

`$ sudo /opt/ssis/bin/ssis-conf set-edition`

Depois de inserir o comando, você verá o seguinte prompt:

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

Details about editions can be found at

https://go.microsoft.com/fwlink/?LinkId=852748&clcid=0x409

Use of PAID editions of this software requires separate licensing through a

Microsoft Volume Licensing program.

By choosing a PAID edition, you are verifying that you have the appropriate

number of licenses in place to install and run this software.

Enter your edition(1-8):
```

Se digitar um valor entre 1 e 7, o sistema configura uma edição gratuita ou paga. Se você inserir 8, o utilitário solicita que você insira a chave do produto que você comprou:

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>Usar a telemetria para configurar comentários do cliente

O `telemetry` comando determina se o SSIS envia comentários à Microsoft.

Para as edições gratuitas (ou seja, as edições Express, Developer e Evaluation), o serviço de telemetria está sempre habilitado. Se você tiver uma edição gratuita, você não pode usar o `telemetry` comando para desabilitar a telemetria.

Insira o seguinte comando:

`$ sudo /opt/ssis/bin/ssis-conf telemetry`

Para edições pagas, depois de inserir o comando, você verá o seguinte prompt:

```
Send feature usage data to Microsoft. Feature usage data includes information
about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

Se escolher **Sim**, o serviço de telemetria está habilitado e começa a ser executado. O serviço de autoinicia após cada inicialização. Se escolher **não**, o serviço de telemetria para e está desabilitado.

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>Use a instalação para inicializar e configurar o Microsoft SQL Server Integration Services

Use o `setup` comando toda vez que você instalar o SSIS.

Insira o seguinte comando:

`sudo /opt/ssis/bin/ssis-conf setup`

O utilitário solicita que você confirme ou para fornecer valores para os seguintes itens:
-   Licença do produto
-   Termos de licença
-   Serviço de telemetria
-   O idioma usado pelo Integration Services

Para executar o `setup` comando solicitações no idioma que você preferir, você pode especificar uma localidade. Por exemplo, para ver avisos em chinês, execute o seguinte comando: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="ssisconf-format"></a>formato de SSIS.conf

O seguinte `/var/opt/ssis/ssis.conf` arquivo fornece um exemplo para cada configuração.

Para o SQL Server, você pode alterar as configurações do sistema alterando os valores de `mssql.conf` arquivo. Para SSIS, você **não é possível** alterar configurações do sistema, alterando os valores no `ssis.conf` arquivo. O `ssis.conf` arquivo só mostra os resultados da instalação. Se você quiser alterar as configurações do SSIS, você pode excluir o `ssis.conf` de arquivo e execute o `setup` comando novamente.

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
