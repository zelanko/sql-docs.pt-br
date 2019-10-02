---
title: Notas sobre a versão do SQL Server 2019 | Microsoft Docs
ms.date: 08/21/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: c7efb49870e148b6a854547d39d4a01139829a89
ms.sourcegitcommit: 4c7151f9f3f341f8eae70cb2945f3732ddba54af
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71326123"
---
# <a name="sql-server-2019-preview-release-notes"></a>Notas sobre a versão a versão prévia do SQL Server 2019
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve as limitações e problemas conhecidos do [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]. Para obter informações relacionadas, consulte:

>[Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)

>[!NOTE]
>O conteúdo é publicado para a versão Release Candidate [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. A versão Release Candidate é um software de pré-lançamento. As informações estão sujeitas a alterações. Para obter informações sobre cenários de suporte, confira [Suporte](#support).

## <a name="includesql-server-2019includessssqlv15-mdmd-release-candidate-rc"></a>Versão release candidate [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] (RC)

A RC [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] é a última versão pública do [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)].

A RC [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] está disponível apenas como Evaluation Edition. Nenhuma outra edição está disponível.

Os detalhes completos sobre o suporte e o licenciamento para as versões de software versão Release Candidate estão em `license_Eval.rtf` com a mídia de instalação.

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

## <a name="documentation"></a>Documentação

- **Problema e impacto sobre o cliente**: A documentação para o SQL Server 2019 (15.x) é limitada e o conteúdo está incluído no conjunto de documentação [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O conteúdo nesses artigos que é específico ao SQL Server 2019 (15.x) é indicado com **Aplica-se a**.

- **Problema e impacto para o cliente**: a documentação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode ser filtrada por versão. Use o controle na parte superior esquerda de cada página de documentação para filtrar os requisitos.

- **Problema e impacto sobre o cliente**: Nenhum conteúdo offline está disponível para o SQL Server 2019 (15.x).

## <a name="build-number"></a>Número de build

O número de build do SQL Server 2019 RC no Windows, Linux e contêineres é `15.0.1900.25`.  O número de build do SQL Server 2019 RC usado em clusters de Big Data é `15.0.1900.47`.

## <a name="hardware-and-software-requirements"></a>Requisitos de hardware e software

- **Problema e impacto sobre o cliente**: Os requisitos de hardware e software ainda estão sendo analisados e não são definitivos para a versão do produto.

  - **Hardware**
    - [Windows – requisitos de processador, memória e sistema operacional](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux – requisitos do sistema](../linux/sql-server-linux-setup.md#system)
  - **Software**
    - Windows Server 2016 ou posterior. Para ver os requisitos adicionais, consulte [Requisitos para instalação do SQL Server](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
    - Microsoft .NET Framework 4.6.2. Disponível no [Centro de Download](https://www.microsoft.com/download/details.aspx?id=53344).
    - Para Linux, consulte [Linux – plataformas compatíveis](../linux/sql-server-linux-setup.md#supportedplatforms)

## <a name="updated-compiler"></a>Compilador atualizado

- **Problema e impacto sobre o cliente**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] é compilado com um compilador atualizado. O CTP 2.1 tinha um problema conhecido em que os resultados de ponto flutuante e outros cenários de conversão podem ter retornado um valor diferente de versões anteriores por causa do compilador atualizado. CTP 2.2 inclui trabalho para garantir que os cenários afetados retornem os mesmos resultados que as versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A partir da versão Release Candidate, não temos conhecimento de nenhum problema restante. Relate quaisquer anomalias de resultado em comparação com [!INCLUDE[ss2017](../includes/sssqlv14-md.md)] à equipe do [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]](https://aka.ms/sqlfeedback) imediatamente.

- **Solução alternativa**: N/A

- **Aplica-se ao**: versão release candidate

## <a name="installation-wizard-may-wait-between-eula-pages"></a>O Assistente de Instalação pode aguardar entre as páginas do EULA

- **Problema e impacto sobre o cliente**: Durante a instalação com o Assistente de Instalação, o processo pode aguardar uma quantidade de tempo estendida entre o EULA (Contrato de Licença de Usuário Final) do R Services e o EULA do Python.

- **Solução alternativa**: Aguarde até o Assistente de Instalação continuar. O tempo de espera pode exceder 30 minutos.

- **Aplica-se ao**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.0

## <a name="utf-8-collations"></a>Ordenações UTF-8

- **Problema e impacto sobre o cliente**: As ordenações UTF-8 habilitadas não poderão ser usadas com alguns dos outros recursos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O UTF-8 não é compatível quando os recursos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a seguir são usados:

  - OLTP in-memory
  - Tabela externa para PolyBase ([!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RC 1)
  - Always Encrypted (até [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RC 1)
  - Servidores vinculados (até [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2)

  > [!Note]
  > No momento, não há nenhuma interface do usuário compatível para escolher as ordenações UTF-8 habilitadas no Azure Data Studio ou SSDT (SQL Server Data Tools). A versão 18 do SSMS ([!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]) mais recente dá suporte à seleção de ordenações habilitadas para UTF-8 na interface do usuário.
 
- **Solução alternativa**: Não há solução alternativa para CTPs do [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)].


- **Aplica-se ao**: todas as versões CTP.

## <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted com enclaves seguros

- **Problema e impacto sobre o cliente**: Cálculos avançados estão aguardando otimizações de desempenho e melhorias de tratamento de erros e atualmente estão desabilitados por padrão.

- **Solução alternativa**: Para habilitar cálculos avançados, execute `DBCC traceon(127,-1)`. Para obter detalhes, consulte [Habilitar cálculos avançados](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave).

- **Aplica-se ao**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2, CTP 3.1

## <a name="sql-server-configuration-manager-may-not-start"></a>O SQL Server Configuration Manager pode não iniciar

- **Problema e impacto sobre o cliente**: O SSCM (SQL Server Configuration Manager) não inicia em um computador sem o arquivo do VCRuntime 140 (VCRUNTIME140.dll). Ao iniciar SSCM, o usuário poderá ver a caixa de diálogo a seguir: 


  `MMC could not create the snap-in. The snap-in might not have been installed correctly.`

- **Solução alternativa**:  Instale o VC Runtime 2013 mais recente (x86):

  - [Verbose](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)
  - [Direto](https://support.microsoft.com/en-us/help/4032938/update-for-visual-c-2013-redistributable-package)

- **Aplica-se ao**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.1, CTP 3.0, CTP 2.5.

## <a name="always-on-availability-group-kubernetes-operator-not-supported"></a>Não há suporte para o operador Kubernetes do grupo de disponibilidade Always On

- **Problema e impacto sobre o cliente**: O operador Kubernetes para grupos de disponibilidade Always On não tem suporte nesta versão Release Candidate e não estará disponível no RTM. 

- **Solução alternativa**: None

- **Aplica-se ao**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] versão release candidate

## <a name="master-data-service-notification-email-contains-broken-link"></a>O email de notificações do Master Data Services contém um link desfeito

- **Problema e impacto sobre o cliente**: O email de notificação do MDS (Master Data Services) contém um link desfeito. O link navega até uma página que retorna um erro como a seguinte mensagem:

   `The view 'Index' or its master was not found or no view engine supports the searched locations.`

- **Solução alternativa**: Abra o portal do MDS e acesse o recurso manualmente.

- **Aplica-se ao**: Versão Release Candidate do SQL Server 2019.

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
