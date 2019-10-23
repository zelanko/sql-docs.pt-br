---
title: Baixar o SQL Server Management Studio (SSMS) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: sstein, maghan
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
ms.date: 10/03/2019
ms.openlocfilehash: a51b0a3da9fda396b23f6ddcf9121fe7a30ec202
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "72542221"
---
# <a name="download-sql-server-management-studio-ssms"></a>Baixar o SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

O SSMS (SQL Server Management Studio) é um ambiente integrado para gerenciar qualquer infraestrutura de SQL, do SQL Server para o Banco de Dados SQL do Azure. O SSMS fornece ferramentas para configurar, monitorar e administrar instâncias do SQL Server e bancos de dados. Use o SSMS para implantar, monitorar e atualizar os componentes da camada de dados usados pelos seus aplicativos, além de criar consultas e scripts.

Use o SSMS para consultar, criar e gerenciar seus bancos de dados e data warehouses, independentemente de onde estiverem – no computador local ou na nuvem.

O SSMS é gratuito!

## <a name="download-ssmshttpsakamsssmsfullsetup"></a>[Baixar o SSMS](https://aka.ms/ssmsfullsetup)

O SSMS 18.3.1 é a versão mais recente de GA (disponibilidade geral) do SSMS. Se você tiver uma versão de GA anterior do SSMS 18 instalada, a instalação do SSMS 18.3.1 o atualizará para o 18.3.1 Se você tiver uma *versão prévia* mais antiga do SSMS 18.x instalada, ela deverá ser desinstalada antes da instalação do SSMS 18.3.1.

**Informações da versão**

- Número da versão: 18.3.1  
- Número de build: 15.0.18183.0  
- Data de lançamento: 02 de outubro de 2019  

Se você tem sugestões ou comentários ou deseja relatar problemas, a melhor maneira de entrar em contato com a equipe do SSMS é usando o [UserVoice](https://aka.ms/sqlfeedback).

A instalação do SSMS 18.x não atualiza nem substitui versões do SSMS 17.x ou anteriores. O SSMS 18.x é instalado lado a lado com versões anteriores para que ambas versões estejam disponíveis para uso.

Se um computador contiver instalações lado a lado do SSMS, verifique se você iniciou a versão correta para suas necessidades específicas. A versão mais recente é rotulada **Microsoft SQL Server Management Studio 18**

> [!Note]
> Se você estiver acessando esta página em uma versão de idioma diferente do inglês e desejar ver o conteúdo mais atualizado, acesse esta página em [inglês](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver15). Você pode baixar idiomas diferentes do site da versão em inglês selecionando [idiomas disponíveis](#available-languages-ssms-1831).

## <a name="available-languages-ssms-1831"></a>Idiomas disponíveis (SSMS 18.3.1)

Esta versão do SSMS pode ser instalada nos seguintes idiomas:

SQL Server Management Studio 18.3.1:  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x40a)

> [!NOTE]
> O módulo do SQL Server PowerShell é uma instalação separada por meio da Galeria do PowerShell. Para obter mais informações, consulte [Baixar o Módulo SQL Server PowerShell](download-sql-server-ps-module.md).

## <a name="new-in-this-release-ssms-1831"></a>Novidades desta versão (SSMS 18.3.1)

| Novo item | Detalhes |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Classificação de dados | Adicionar informações de classificação de dados à interface do usuário de propriedades da coluna (*Tipo da Informação*, *ID do Tipo da Informação*, *Rótulo de Confidencialidade* e *ID do Rótulo de Confidencialidade* não são expostos na interface do usuário do SSMS). |
| IntelliSense/editor | Suporte atualizado para recursos adicionados recentemente ao SQL Server 2019 (por exemplo, "ALTERAR CONFIGURAÇÃO DO SERVIDOR"). |
| Integration Services | Adicione um novo item de menu de seleção `Tools > Migrate to Azure > Configure Azure-enabled DTExec` que invoca as execuções de pacote SSIS (Integration Services) no Azure-SSIS Integration Runtime como atividades de Executar Pacote SSIS em pipelines do ADF. |
| SMO/script | Adicionado suporte para script de suporte da restrição exclusiva do SQL Data Warehouse do Azure. |
| SMO/script | Classificação de dados – suporte adicionado para o SQL versão 10 (SQL 2008) e posteriores.  – adicionado novo atributo de confidencialidade 'rank' para SQL versão 15 (SQL 2019) e posteriores e Banco de Dados SQL do Azure. |

Para obter detalhes sobre as novidades desta versão, confira [notas sobre a versão do SSMS](release-notes-ssms.md).

## <a name="supported-sql-offerings-ssms-1831"></a>Ofertas de SQL compatíveis (SSMS 18.3.1)

- Esta versão do SSMS funciona com todas as [versões com suporte do SQL Server 2008 – [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) e fornece o maior nível de suporte para trabalhar com os recursos de nuvem mais recentes no Banco de Dados SQL do Azure e SQL Data Warehouse do Azure.
- Além disso, o SSMS 18.x pode ser instalado lado a lado com o SSMS 17.x, o SSMS 16.x ou o SSMS do SQL Server 2014 e anteriores.
- SSIS (SQL Server Integration Services) – a versão SSMS 17.x ou posterior não dá suporte à conexão com o serviço herdado do SQL Server Integration Services. Para conectar-se a uma versão anterior do Integration Services herdado, use a versão do SSMS alinhada com a versão do SQL Server. Por exemplo, use o SSMS 16.x para conectar ao serviço herdado do SQL Server Integration Services 2016. O SSMS 17.x e o 16.x podem ser instalados lado a lado no mesmo computador. Desde o lançamento do SQL Server 2012, o banco de dados de catálogo do SSIS, o SSISDB, é a maneira recomendada para armazenar, gerenciar, executar e monitorar os pacotes do Integration Services. Para obter detalhes, veja o [Catálogo do SSIS](../integration-services/catalog/ssis-catalog.md).

## <a name="supported-operating-systems-ssms-1831"></a>Sistemas operacionais compatíveis (SSMS 18.3.1)

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

## <a name="release-notes-ssms-1831"></a>Notas sobre a versão (SSMS 18.3.1)

Há alguns [problemas conhecidos](release-notes-ssms.md#known-issues-1831) nesta versão.

Para saber detalhes sobre esta versão, confira [as notas sobre a versão do SSMS](release-notes-ssms.md).

## <a name="previous-ssms-releases"></a>Versões anteriores do SSMS

[Versões anteriores do SQL Server Management Studio](../ssms/release-notes-ssms.md#previous-ssms-releases)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

## <a name="see-also"></a>Confira também

- [Tutorial: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Documentação do SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Pacotes de serviço e atualizações adicionais](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [Baixar o SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
