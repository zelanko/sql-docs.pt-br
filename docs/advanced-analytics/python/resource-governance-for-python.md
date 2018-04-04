---
title: Governança de recursos para Python | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 11ca749c545f7256ffa803cd6db11679d3f631dd
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2018
---
# <a name="resource-governance-for-python"></a>Governança de recursos para Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Porque o Python é habilitado por meio da mesma arquitetura de extensibilidade que foi implementada para o idioma R no SQL Server 2016, você pode usar as ferramentas existentes no SQL Server como administrador de recursos, DMVs e eventos estendidos, para monitorar a execução do Python scripts no SQL Server.

Governança de recursos em particular é importante porque analisar grandes quantidades de dados de produção pode imposto avançada mesmo hardware.  Para impedir que os dados sendo movidos para fora do banco de dados para computadores que não podem ser gerenciados ou auditados, é importante que o administrador de banco de dados alocar recursos suficientes para operações de análise avançada.

Esta seção fornece informações sobre como você pode gerenciar os recursos usados pelo tempo de execução do Python e monitorar o uso de recursos de Python scripts de trabalhos em execução na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.

> [!NOTE]
> Suporte do Python é um novo recurso do SQL Server 2017 e está na versão de pré-lançamento. Pesquisar para obter mais informações em breve.
> Em geral, você pode monitorar qualquer script externo, incluindo aquele executado Python, usando a mesma estrutura que foi fornecida para o controle de recursos de scripts de R no SQL Server 2016.

## <a name="what-is-resource-governance"></a>O que é a governança de recursos?

A governança de recursos foi projetada para identificar e evitar problemas comuns em um ambiente de servidor de banco de dados, em que geralmente há vários aplicativos dependentes e vários serviços aos quais dar suporte e balancear. Para o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], a governança de recursos envolve as seguintes tarefas:  

+ **Identificando os scripts que usam recursos excessivos servidor**. O administrador precisa ser capaz de cancelar ou limitar os trabalhos que estão consumindo recursos demais.

+ **Redução de cargas de trabalho imprevisíveis**. Se a execução simultânea de vários trabalhos de Python no servidor e os trabalhos não são isolados uma da outra usando pools de recursos, a contenção de recursos resultante pode resultar em desempenho imprevisível ou ameaçam a conclusão da carga de trabalho.

+ **Priorizando a cargas de trabalho**. O administrador ou o arquiteto precisa ser capaz de especificar cargas de trabalho que deverão ter precedência ou, se houver contenção de recursos, assegurar que determinadas cargas de trabalho sejam concluídas.

Você pode usar [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) para gerenciar os recursos usados pelos tempos de execução externos. Isso inclui scripts Python que são iniciados de um controle remoto terminal mas executada usando o computador do SQL Server como o contexto de computação.

> [!NOTE] 
> Administrador de recursos está disponível na edição Enterprise.

## <a name="how-to-use-resource-governor-to-manage-python-execution"></a>Como usar o administrador de recursos para gerenciar a execução do Python

Em geral, você pode gerenciar os recursos alocados para qualquer trabalho de script externo, criando uma *pool de recursos externos* e atribuição de cargas de trabalho ao pool. Um pool de recursos externos é um novo tipo de pool de recursos introduzido no SQL Server 2016, para ajudar a gerenciar o tempo de execução de R e outros processos externos para o mecanismo de banco de dados. Ele pode ser usado para monitorar trabalhos de Python, começando com o SQL Server 2017.

Há três tipos de pools de recursos padrão:

+ O *pool interno* representa os recursos usados pelo próprio SQL Server e não pode ser alterado nem restrito.
+ O *pool padrão* é um conjunto de usuários predefinidos que você pode usar para modificar o uso de recursos para o servidor como um todo. Você também pode definir grupos de usuários que pertencem a esse pool, para gerenciar o acesso aos recursos.
+ O *pool externo padrão* é um pool de usuários predefinido para recursos externos. Adicionalmente, você pode criar novos pools de recursos externos e definir grupos de usuários como pertencentes a um desses pools.

Além disso, você pode criar *pools de recursos definidos pelo usuário* para alocar recursos para o mecanismo de banco de dados ou outros aplicativos e criar *pools de recursos externos definidos pelo usuário* para gerenciar o R e outros processos externos.

Para obter uma boa introdução à terminologia e a conceitos gerais, consulte [Pool de recursos do Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md).

## <a name="resource-management-using-resource-governor"></a>Gerenciamento de recursos usando o Resource Governor

Se você for novo para o administrador de recursos, consulte este artigo para obter uma rápida explicação de como modificar os recursos de instância padrão e criar um novo pool de recursos externos: [como: criar um Pool de recursos para R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)

Você pode usar o *pool de recursos externos* mecanismo para gerenciar os recursos usados pelos executáveis com suporte a seguir:

+ Python35.exe quando chamado do SQL Server ou chamado remotamente com o SQL Server como o contexto de computação remota
+ BxlServer.exe e processos satélite
+ Iniciadores iniciados por barra inicial, como PythonLauncher.dll

> [!NOTE]
> Não há suporte para o gerenciamento direto do serviço barra inicial usando o administrador de recursos. Isso ocorre porque o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] é um serviço confiável que, por design, pode hospedar somente os inicializadores fornecidos pela Microsoft. Inicializadores confiáveis também são configurados para evitar o consumo excessivo de recursos.

É recomendável que você gerencie os processos satélite usando o Resource Governor e ajuste-os para atender às necessidades da configuração do banco de dados individual e da carga de trabalho.  Por exemplo, qualquer processo satélite individual pode ser criado ou destruído sob demanda durante a execução.

## <a name="disable-or-enable-external-script-execution"></a>Desabilitar ou habilitar a execução do Script externo

Suporte para scripts externos é opcional em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instalação e até mesmo após a instalação a execução do script completo, externa é definida como OFF por padrão por motivos de segurança. Portanto, depois de concluir a instalação de um a idiomas e serviços relacionados de aprendizado de máquina, explicitamente, reconfigurar a instância e, em seguida, reinicie o serviço de mecanismo de banco de dados.

No caso de fuga scripts, você pode desabilitar todos a execução do script. Apenas reverter esse processo e defina a propriedade `external scripts enabled` como FALSE ou 0, na instância. Isso desabilitará imediatamente qualquer execução de script externo. Você deve reservar esta opção para problemas de segurança, ou em situações em que um administrador precisa mitigar os problemas de recurso imediatamente.

## <a name="see-also"></a>Consulte também

[Pool de recursos do Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)

