---
title: Baixar o SQL Server Management Studio (SSMS)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
keywords:
- instalar ssms, baixar ssms, ssms mais recentes
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- instalação do SQL management studio
- baixar o sql management studio
- ms sql management studio
- instalar o sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
author: dnethi
ms.author: dinethi
ms.reviewer: sstein, maghan
ms.custom: seo-lt-2019
ms.date: 02/18/2020
ms.openlocfilehash: 8045c054d05a1e92eaf18f9aba852d9301f7ef60
ms.sourcegitcommit: 64e96ad1ce6c88c814e3789f0fa6e60185ec479c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2020
ms.locfileid: "77652925"
---
# <a name="download-sql-server-management-studio-ssms"></a>Baixar o SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

O SSMS (SQL Server Management Studio) é um ambiente integrado para gerenciar qualquer infraestrutura de SQL, do SQL Server para o Banco de Dados SQL do Azure. O SSMS fornece ferramentas para configurar, monitorar e administrar instâncias do SQL Server e bancos de dados. Use o SSMS para implantar, monitorar e atualizar os componentes da camada de dados usados pelos seus aplicativos, além de criar consultas e scripts.

Use o SSMS para consultar, criar e gerenciar seus bancos de dados e data warehouses, independentemente de onde estiverem – no computador local ou na nuvem.

O SSMS é gratuito!

## <a name="download-ssms"></a>Baixar o SSMS

**[![download](media/download-icon.png) Baixar o SSMS (SQL Server Management Studio)](https://aka.ms/ssmsfullsetup)**

O SSMS 18.4 é a versão mais recente de GA (disponibilidade geral) do SSMS. Se você tiver uma versão de GA anterior do SSMS 18 instalada, a instalação do SSMS 18.4 atualizará o produto para a versão 18.4.

### <a name="version-information"></a>Informações da versão

- Número da versão: 18.4  
- Número de build: 15.0.18206.0  
- Data de lançamento: 04 de novembro de 2019  

Se você tem sugestões ou comentários ou deseja relatar problemas, a melhor maneira de entrar em contato com a equipe do SSMS é usando o [UserVoice](https://aka.ms/sqlfeedback).

A instalação do SSMS 18.x não atualiza nem substitui versões do SSMS 17.x ou anteriores. O SSMS 18.x é instalado lado a lado com versões anteriores para que as duas versões estejam disponíveis para uso. No entanto, se você tiver uma ***versão prévia*** do SSMS 18.x instalada, será necessário **desinstalar** essa versão antes de instalar o SSMS 18.4. É possível conferir se você tem a *Versão Prévia* acessando a janela Ajuda > Sobre.

Se um computador contiver instalações lado a lado do SSMS, verifique se você iniciou a versão correta para suas necessidades específicas. A versão mais recente é rotulada **Microsoft SQL Server Management Studio 18**

> [!Note]
> Se você estiver acessando esta página em uma versão de idioma diferente do inglês e desejar ver o conteúdo mais atualizado, acesse a [versão do site em inglês dos EUA](https://aka.ms/downloadssmsusenglish). Você pode baixar idiomas diferentes do site da versão em inglês dos EUA selecionando [idiomas disponíveis](#available-languages).

## <a name="available-languages"></a>Idiomas disponíveis

Esta versão do SSMS pode ser instalada nos seguintes idiomas:

SQL Server Management Studio 18.4:  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x40a)

> [!NOTE]
> O módulo do SQL Server PowerShell é uma instalação separada por meio da Galeria do PowerShell. Para obter mais informações, consulte [Baixar o Módulo SQL Server PowerShell](download-sql-server-ps-module.md).

## <a name="whats-new"></a>Novidades

Para obter detalhes e mais informações sobre as novidades desta versão, confira as [Notas sobre a versão do SSMS](release-notes-ssms.md).

Há alguns [problemas conhecidos](release-notes-ssms.md#known-issues-184) nesta versão.

## <a name="previous-versions"></a>Versões anteriores

Este artigo destina-se somente à versão mais recente do SSMS. Para baixar as versões anteriores do SSMS, acesse [Versões anteriores do SSMS](../ssms/release-notes-ssms.md#previous-ssms-releases).

## <a name="unattended-install"></a>Instalação autônoma

Você também pode instalar o SSMS usando um script de prompt de comando.

Se quiser instalar o SSMS em segundo plano sem prompts de GUI, siga as etapas abaixo.

1. Inicialize o prompt de comando com permissões elevadas.

2. Digite o comando abaixo no prompt de comando.

    ```console
    start "" <path where SSMS-ENU.exe file is located> /Quiet SSMSInstallRoot=<path where you want to install SSMS>
    ```

    Exemplo:

    ```console
    start "" %systemdrive%\SSMSfrom\SSMS-Setup-ENU.exe /Quiet SSMSInstallRoot=%systemdrive%\SSMSto
    ```

    Você também pode passar */Passive* em vez de */Quiet* para ver a interface do usuário da configuração.

3. Se tudo correr bem, será possível ver o SSMS instalado em %systemdrive%\SSMSto\Common7\IDE\Ssms.exe” com base no exemplo. Se algo der errado, você poderá inspecionar o código de erro retornado e dar uma olhada em %TEMP%\SSMSSetup para o arquivo de log.

## <a name="supported-sql-offerings-ssms-184"></a>Ofertas de SQL compatíveis (SSMS 18.4)

- Esta versão do SSMS funciona com todas as [versões com suporte do SQL Server 2008 – [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) e fornece o maior nível de suporte para trabalhar com os recursos de nuvem mais recentes no Banco de Dados SQL do Azure e SQL Data Warehouse do Azure.
- Além disso, o SSMS 18.x pode ser instalado lado a lado com o SSMS 17.x, o SSMS 16.x ou o SSMS do SQL Server 2014 e anteriores.
- SSIS (SQL Server Integration Services) – a versão SSMS 17.x ou posterior não dá suporte à conexão com o serviço herdado do SQL Server Integration Services. Para conectar-se a uma versão anterior do Integration Services herdado, use a versão do SSMS alinhada com a versão do SQL Server. Por exemplo, use o SSMS 16.x para conectar ao serviço herdado do SQL Server Integration Services 2016. O SSMS 17.x e o 16.x podem ser instalados lado a lado no mesmo computador. Desde o lançamento do SQL Server 2012, o banco de dados de catálogo do SSIS, o SSISDB, é a maneira recomendada para armazenar, gerenciar, executar e monitorar os pacotes do Integration Services. Para obter detalhes, veja o [Catálogo do SSIS](../integration-services/catalog/ssis-catalog.md).

## <a name="supported-operating-systems-ssms-184"></a>Sistemas operacionais compatíveis (SSMS 18.4)

Esta versão do SSMS é compatível com as seguintes plataformas de 64 bits quando usada com o service pack mais recente disponível:

- Windows 10 (64-bit) <sup>*</sup>
- Windows 8.1 (64 bits)
- Windows Server 2019 (64 bits)
- Windows Server 2016 (64 bits) <sup>*</sup>
- Windows Server 2012 R2 (64 bits)
- Windows Server 2012 (64 bits)
- Windows Server 2008 R2 (64 bits)

<sup>*</sup> Exige a versão 1607 (10.0.14393) ou posterior

> [!NOTE]
> O SSMS é executado somente no Windows (AMD ou Intel). Se você precisar de uma ferramenta que seja executada em plataformas diferentes do Windows, confira o Azure Data Studio. O Azure Data Studio é uma nova ferramenta multiplataforma executada no macOS, no Linux e no Windows. Para obter detalhes, veja [Azure Data Studio](../azure-data-studio/what-is.md).

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

## <a name="see-also"></a>Confira também

- [Tutorial: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Documentação do SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Atualizações mais recentes](../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)
- [Azure Data Studio](../azure-data-studio/what-is.md)
- [Baixar o SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- [Guia de Arquitetura de Dados do Azure](https://docs.microsoft.com/azure/architecture/data-guide/)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]