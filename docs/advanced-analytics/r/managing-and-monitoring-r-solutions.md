---
title: "Gerenciando e monitorando soluções de aprendizado de máquina | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 07/26/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d455f22a-190f-4a28-9088-98a843cd5db2
caps.latest.revision: "15"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b153db4a35b5ef44e1c385cb902000ef94abc078
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="managing-and-monitoring-machine-learning-solutions"></a>Gerenciando e monitorando soluções de aprendizado de máquina

Este artigo descreve os recursos do SQL Server Machine Learning Services que são relevantes para os administradores de banco de dados que precisam para começar a trabalhar com soluções de R e Python.

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 serviços de aprendizado de máquina

## <a name="security"></a>Segurança

Os administradores de banco de dados devem fornecer acesso a dados não apenas aos cientistas de dados, mas a uma variedade de desenvolvedores de relatório, analistas de negócios e consumidores de dados de negócios. A integração do R (e agora Python) no SQL Server fornece muitos benefícios ao administrador de banco de dados que oferece suporte à função de ciência de dados.

+ A arquitetura do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] protege os bancos de dados e isola a execução das sessões de R da operação da instância do banco de dados.

+ Você pode especificar quem tem permissão para executar os scripts R e certificar-se de que os dados usados em trabalhos de R sejam gerenciados com as mesmas funções de segurança definidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

+ O administrador de banco de dados pode usar funções para gerenciar a instalação de pacotes de R e a execução de scripts de R e Python.

Para obter mais informações, consulte estes recursos:

+ [Considerações sobre segurança para o tempo de execução do R no SQL Server](../../advanced-analytics/r/security-considerations-for-the-r-runtime-in-sql-server.md)

+ [Visão geral de segurança de R](../r/security-overview-sql-server-r.md)

+ [Visão geral de segurança do Python](../python/security-overview-sql-server-python-services.md)

+ [Instalar e gerenciar pacotes do R](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)

## <a name="configuration-and-management"></a>Configuração e gerenciamento

Os administradores de banco de dados devem integrar projetos e prioridades concorrentes em um único ponto de contato: o servidor de banco de dados. Eles devem oferecer suporte à análise mantendo a integridade dos armazenamentos de dados operacional e de relatórios. A integração da máquina de aprendizado com o SQL Server fornece muitos benefícios ao administrador de banco de dados, que serve cada vez mais um papel fundamental na implantação de uma infraestrutura eficiente para ciência de dados.

+ Sessões de R e Python são executadas em um processo separado para garantir que o servidor continue a executar como de costume, mesmo se tiver problemas, o tempo de execução do script externo.

+ Contas de usuário físico de baixo privilégio são usadas para conter e isolar a atividade de script externo.

+ O DBA pode usar ferramentas de gerenciamento de recursos do SQL Server padrão para controlar a quantidade de recursos alocados para o tempo de execução de R, para evitar que cálculos imensos prejudiquem o desempenho geral do servidor.

Para obter mais informações, consulte estes recursos:

+ [Governança de recursos para serviços de R](../r/resource-governance-for-r-services.md)

+ [Monitorar os serviços R](../r/monitoring-r-services.md)

+ [Configurar e gerenciar extensões de análise avançada](../r/configure-and-manage-advanced-analytics-extensions.md)
