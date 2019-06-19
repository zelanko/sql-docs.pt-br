---
title: Notas sobre a versão do SQL Server 2019 | Microsoft Docs
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 8f44927fb59e6d1b613b2a67e26aed980b3a080a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65993951"
---
# <a name="sql-server-2019-preview-release-notes"></a>Notas sobre a versão a versão prévia do SQL Server 2019
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve as limitações e os problemas conhecidos para as versões do [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP (Community Technology Preview). Para obter informações relacionadas, consulte:
- [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)

## <a name="ctp-30"></a>CTP 3.0

O [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.0 é a última versão pública do [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)].

O [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.0 está disponível apenas como Evaluation Edition. Nenhuma outra edição está disponível. 

Os detalhes completos sobre o suporte e o licenciamento para as versões CTP estão em `license_Eval.rtf` com a mídia de instalação.

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

## <a name="documentation"></a>Documentação

- **Problema e impacto sobre o cliente**: A documentação para o SQL Server 2019 (15.x) é limitada e o conteúdo está incluído no conjunto de documentação [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O conteúdo nesses artigos que é específico ao SQL Server 2019 (15.x) é indicado com **Aplica-se a**.

- **Problema e impacto para o cliente**: a documentação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode ser filtrada por versão. Use o controle na parte superior esquerda de cada página de documentação para filtrar os requisitos.

- **Problema e impacto sobre o cliente**: Nenhum conteúdo offline está disponível para o SQL Server 2019 (15.x).

## <a name="hardware-and-software-requirements"></a>Requisitos de hardware e software

- **Problema e impacto sobre o cliente**: Os requisitos de hardware e software ainda estão sendo analisados e não são definitivos para a versão do produto.

  - **Hardware**
    - [Windows – requisitos de processador, memória e sistema operacional](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux – requisitos do sistema](../linux/sql-server-linux-setup.md#system)
  - **Software**
    - Windows Server 2016 ou posterior. Para ver os requisitos adicionais, consulte [Requisitos para instalação do SQL Server](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
    - Microsoft .NET Framework 4.6.2. Disponível no [Centro de Download](https://www.microsoft.com/download/details.aspx?id=53344).
    - Para Linux, consulte [Linux – plataformas compatíveis](../linux/sql-server-linux-setup.md#supportedplatforms)

## <a name = "release-notes"></a>Recursos excluídos do suporte

- **Problema e impacto sobre o cliente**: o [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] exclui o suporte para os seguintes componentes, recursos e cenários:
  - SQL Sever Analysis Services
  - SQL Server Reporting Services
  - Grupos de disponibilidade Always On no Kubernetes
  - Recuperação de banco de dados acelerada
  - Metadados do tempdb com otimização de memória

- **Solução alternativa**: Nenhum. A exclusão se aplica a todos os clientes, incluindo os participantes do Programa de Usuário Pioneiro do SQL.

- **Aplica-se ao**: CTP 3.0

## <a name="updated-compiler"></a>Compilador atualizado

- **Problema e impacto sobre o cliente**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] é compilado com um compilador atualizado. O CTP 2.1 tinha um problema conhecido em que os resultados de ponto flutuante e outros cenários de conversão podem ter retornado um valor diferente de versões anteriores por causa do compilador atualizado. CTP 2.2 inclui trabalho para garantir que os cenários afetados retornem os mesmos resultados que as versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A partir da versão CTP 3.0, desconhecemos problemas restantes. Relate quaisquer anomalias de resultado em comparação com [!INCLUDE[ss2017](../includes/sssqlv14-md.md)] à equipe do [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]](http://aka.ms/sqlfeedback) imediatamente.

- **Solução alternativa**: N/A

- **Aplica-se ao**: SQL Server 2019 CTP 3.0, CTP 2.5, CTP 2.4, CTP 2.3, CTP 2.2, CTP 2.1

## <a name="installation-wizard-may-wait-between-eula-pages"></a>O Assistente de Instalação pode aguardar entre as páginas do EULA

- **Problema e impacto sobre o cliente**: Durante a instalação com o Assistente de Instalação, o processo pode aguardar uma quantidade excessiva de tempo entre o EULA (Contrato de Licença de Usuário Final) do R Services e o EULA do Python.

- **Solução alternativa**: Aguarde até o Assistente de Instalação continuar. O tempo de espera pode exceder 30 minutos.

- **Aplica-se ao**: SQL Server 2019 CTP 3.0

## <a name="utf-8-collations"></a>Agrupamentos UTF-8

- **Problema e impacto sobre o cliente**: Os agrupamentos UTF-8 habilitados não poderão ser usados com alguns dos outros recursos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O UTF-8 não é compatível quando os recursos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a seguir são usados:

  - OLTP in-memory
  - Tabela externa para PolyBase
  - Always Encrypted

  > [!Note]
  > No momento, não há nenhuma interface do usuário compatível para escolher os agrupamentos UTF-8 habilitados no Azure Data Studio ou SSDT (SQL Server Data Tools). A versão 18 do SSMS ([!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]) mais recente dá suporte à seleção de ordenações habilitadas para UTF-8 na interface do usuário.
 
- **Solução alternativa**: Não há solução alternativa para CTPs do [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)].

- **Aplica-se ao**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.0, CTP 2.5, CTP 2.4, CTP 2.3, CTP 2.2, CTP 2.1, CTP 2.0.

## <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted com enclaves seguros

- **Problema e impacto sobre o cliente**: Os cálculos avançados estão aguardando várias otimizações de desempenho, incluindo a funcionalidade limitada (sem indexação etc.) e estão desabilitados por padrão no momento.

- **Solução alternativa**: Para habilitar cálculos avançados, execute `DBCC traceon(127,-1)`. Para obter detalhes, consulte [Habilitar cálculos avançados](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave).

- **Aplica-se ao**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.0, CTP 2.5, CTP 2.4, CTP 2.3, 2.2, CTP 2.1, 2.0.

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
