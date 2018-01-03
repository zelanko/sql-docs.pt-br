---
title: "Visão geral da arquitetura (SQL Server R Services) | Microsoft Docs"
ms.custom: 
ms.date: 07/11/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6c4a4f66-ea3e-4a73-acf2-6c8aeafc94b0
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 445c28ab59dd3f66f46a0ad43aff40da5696ee0a
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="architecture-overview-for-r-in-sql-server"></a>Visão geral da arquitetura de R no SQL Server

Esta seção fornece uma visão geral da arquitetura do SQL Server 2016 R Services e de serviços de aprendizado de máquina do SQL Server de 2017.

A arquitetura para a arquitetura de extensibilidade é o mesmo ou muito semelhantes para o SQL Server 2016 e versões de 2017 do SQL Server e semelhante também para R e Python. No entanto, para simplificar a discussão, este tópico discute apenas os componentes de R, incluindo novos componentes adicionados no mecanismo de banco de dados do SQL Server para dar suporte a execução do script externo, segurança, bibliotecas de R e interoperabilidade com código-fonte aberto R.

Detalhes adicionais são fornecidos nos links para cada seção.

## <a name="r-interoperability"></a>Interoperabilidade de R

SQL Server 2016 R Services e serviços do aprendizado de máquina 2017 SQL Server (no banco de dados) instalam uma distribuição de software livre de R, bem como pacotes fornecidos pela Microsoft que dão suporte ao processamento distribuído e/ou paralelo.

A arquitetura é projetada, de modo que os scripts externos usando R são executados em um processo separado do SQL Server. Os usuários atuais do R devem ser capazes de portar seu código do R e executá-lo no T-SQL com pequenas modificações.

Para dimensionar sua solução ou usar o processamento paralelo, é recomendável que você use o [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) pacote ou o [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package) pacote. Se você não usar os recursos de computação distribuídos fornecidos por essas bibliotecas, você ainda pode obter melhorias de desempenho executando seu código R no contexto do SQL Server.

Para obter mais informações sobre os componentes de script externos que estão instalados, ou a interação do SQL Server com R, consulte [interoperabilidade de R](../../advanced-analytics/r/r-interoperability-in-sql-server.md)

## <a name="components-to-support-r-integration"></a>Componentes para dar suporte à integração de R

A estrutura de extensibilidade introduzida no SQL Server 2016 continua no SQL Server 2017. Os componentes de extensibilidade são usados pelo SQL Server para iniciar o tempo de execução externo para R, para passar dados entre R e o mecanismo de banco de dados e coordenar tarefas paralelas necessárias para um trabalho de R.

É a função desses componentes adicionais melhorar a velocidade de troca de dados e compactação, enquanto fornece uma plataforma segura, de alto desempenho para a execução de scripts externos.

Para uma descrição detalhada dos componentes que dão suporte a R, como o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] e RLauncher, consulte [novos componentes](../../advanced-analytics/r/new-components-in-sql-server-to-support-r.md).

## <a name="security"></a>Segurança

Quando você executa o código de R usando os serviços de aprendizado de máquina ou SQL Server R Services, todos os scripts de R são executados fora do processo do SQL Server, para fornecer maior capacidade de gerenciamento e de segurança. Esse isolamento de processos se aplica independentemente de você executar o script de R como parte de um procedimento armazenado, ou conecte-se para o trabalho do computador do SQL Server de um computador remoto e inicia um trabalho que usa o servidor como o contexto de computação.

SQL Server intercepta todas as solicitações de trabalho, protege seus dados usando objetos de trabalho do Windows e a tarefa e mantém a segurança em dados usando funções de banco de dados e contas de usuário do SQL Server.

Dados são mantidos dentro do limite de conformidade com a imposição da segurança do SQL Server no nível de instância, banco de dados e tabela. O administrador de banco de dados pode controlar quem tem a capacidade de executar trabalhos em R, e que tem a capacidade de instalar ou compartilhamento de pacotes de R. O administrador também pode monitorar o uso de scripts de R por usuários locais ou remotos e monitorar e gerenciar os recursos consumidos.

## <a name="next-steps"></a>Próximas etapas

[Componentes que dão suporte à integração de R](new-components-in-sql-server-to-support-r.md)

[Interoperabilidade de R](r-interoperability-in-sql-server.md)

[Visão geral de segurança](security-overview-sql-server-r.md)
