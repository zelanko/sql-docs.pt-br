---
title: Baixar o SQL Server Management Studio (SSMS) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
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
ms.custom: ''
ms.date: 06/12/2019
ms.openlocfilehash: 0841379b0b64ebe81e4a23f76b21f6cf6abe0ec3
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265156"
---
# <a name="download-sql-server-management-studio-ssms"></a>Baixar o SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

O SSMS (SQL Server Management Studio) é um ambiente integrado para gerenciar qualquer infraestrutura de SQL, do SQL Server para o Banco de Dados SQL do Azure. O SSMS fornece ferramentas para configurar, monitorar e administrar instâncias do SQL Server e bancos de dados. Use o SSMS para implantar, monitorar e atualizar os componentes da camada de dados usados pelos seus aplicativos, além de construir consultas e scripts.

Use o SSMS para consultar, criar e gerenciar seus bancos de dados e data warehouses, independentemente de onde estiverem – no computador local ou na nuvem.

O SSMS é gratuito!

## <a name="download-ssms-181"></a>Baixar o SSMS 18.1

**O SSMS 18.1 já está disponível e é a última versão de GA (disponibilidade geral) do *SQL Server Management Studio* compatível com o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]!**

**[![download](../ssdt/media/download.png) Baixar o SQL Server Management Studio 18.1](https://go.microsoft.com/fwlink/?linkid=2094583)**

O SSMS 18.1 é a versão mais recente de GA do SSMS. Se você tiver o SSMS 18.0 (GA) instalado, a instalação do SSMS 18.1 causará a atualização do produto. Se você tiver *versões prévias* anteriores do SSMS 18.0 instaladas, desinstale-as antes de instalar o SSMS 18.1.

**Informações da versão**

- Número da versão: 18.1<br>
- Número de build: 15.0.18131.0<br>
- Data de lançamento: 11 de junho de 2019

Se você tem sugestões ou comentários ou deseja relatar problemas, a melhor maneira de entrar em contato com a equipe do SSMS é usando o [UserVoice](https://aka.ms/sqlfeedback).

A instalação do SSMS 18.x não atualiza nem substitui versões do SSMS 17.x ou anteriores. O SSMS 18.x é instalado lado a lado com versões anteriores para que ambas versões estejam disponíveis para uso.

Se um computador contiver instalações lado a lado do SSMS, verifique se você iniciou a versão correta para suas necessidades específicas. A versão mais recente é rotulada **Microsoft SQL Server Management Studio 18**

## <a name="available-languages-ssms-181"></a>Idiomas disponíveis (SSMS 18.1)

Esta versão do SSMS pode ser instalada nos seguintes idiomas:

SQL Server Management Studio 18.1:<br>
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40a)

> [!NOTE]
> O módulo do SQL Server PowerShell é uma instalação separada por meio da Galeria do PowerShell. Para obter mais informações, consulte [Baixar o Módulo SQL Server PowerShell](download-sql-server-ps-module.md).

## <a name="new-in-this-release-ssms-181"></a>Novidades desta versão (SSMS 18.1)

- **Diagramas de banco de dados** – foram adicionados novamente ao SSMS. Para saber detalhes, confira [Diagramas de banco de dados](https://feedback.azure.com/forums/908035/suggestions/37507828).
- **SSBDIAGNOSE.EXE** – a ferramenta de linha de comando Diagnosticar do SQL Server foi adicionada novamente ao pacote do SSMS.
- **SSIS (Integration Services)** – compatibilidade com o agendamento do pacote do SSIS, localizado no Catálogo do SSIS no Azure ou no Sistema de Arquivos no Azure. Há três entradas para iniciar a caixa de diálogo Novo agendamento, o item de menu *Novo agendamento…* mostrado ao clicar com o botão direito do mouse no pacote do Catálogo do SSIS no Azure; o item de menu *Agendar Pacote do SSIS no Azure* em *Migrar para o Azure* no item de menu *Ferramentas*; e "Agendar o SSIS no Azure", mostrado ao clicar com o botão direito do mouse na pasta Trabalhos no agente do SQL Server da Instância Gerenciada do Banco de Dados SQL do Azure.

Para obter detalhes sobre as novidades desta versão, confira [notas sobre a versão do SSMS](release-notes-ssms.md).

## <a name="supported-sql-offerings-ssms-181"></a>Ofertas de SQL compatíveis (SSMS 18.1)

* Esta versão do SSMS funciona com todas as [versões com suporte do SQL Server 2008 – [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) e fornece o maior nível de suporte para trabalhar com os recursos de nuvem mais recentes no Banco de Dados SQL do Azure e SQL Data Warehouse do Azure.
* Além disso, o SSMS 18.x pode ser instalado lado a lado com o SSMS 17.x, o SSMS 16.x ou o SSMS do SQL Server 2014 e anteriores.
* SSIS (SQL Server Integration Services) – a versão SSMS 17.x ou posterior não permite a conexão com o serviço herdado do SQL Server Integration Services. Para conectar-se a uma versão anterior do Integration Services herdado, use a versão do SSMS alinhada com a versão do SQL Server. Por exemplo, use o SSMS 16.x para conectar ao serviço herdado do SQL Server Integration Services 2016. O SSMS 17.x e o SSMS 16.x podem ser instalados lado a lado no mesmo computador. Desde o lançamento do SQL Server 2012, o banco de dados de catálogo do SSIS, o SSISDB, é a maneira recomendada para armazenar, gerenciar, executar e monitorar os pacotes do Integration Services. Para obter detalhes, veja o [Catálogo do SSIS](../integration-services/catalog/ssis-catalog.md).

## <a name="supported-operating-systems-ssms-181"></a>Sistemas operacionais compatíveis (SSMS 18.1)

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
> O SSMS é executado somente no Windows. Se você precisar de uma ferramenta que seja executada em plataformas diferentes do Windows, confira o Azure Data Studio. O Azure Data Studio é uma nova ferramenta multiplataforma executada no macOS, no Linux e no Windows. Para obter detalhes, veja [Azure Data Studio](../azure-data-studio/what-is.md).

## <a name="release-notes-ssms-181"></a>Notas sobre a versão (SSMS 18.1)

Há alguns [problemas conhecidos](release-notes-ssms.md#known-issues-181) nesta versão.

Para saber detalhes sobre esta versão, confira [as notas sobre a versão do SSMS](release-notes-ssms.md).

## <a name="previous-ssms-releases"></a>Versões anteriores do SSMS

[Versões anteriores do SQL Server Management Studio](../ssms/release-notes-ssms.md#previous-ssms-releases)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

## <a name="see-also"></a>Consulte Também

- [Tutorial: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Documentação do SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Pacotes de serviço e atualizações adicionais](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [Baixar o SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
