---
title: Documentação do Sistema de Plataforma de Análise | Microsoft Docs
description: O Microsoft APS (Analytics Platform System), uma plataforma de dados projetada para data warehouse e análise de Big Data, oferece integração de dados profunda, processamento de consulta de ala velocidade, armazenamento altamente escalonável e manutenção simples para sua solução de business intelligence de ponta a ponta.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/18/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: bc8765d0bc8fe4b5b9ab3b4bcc98ce940f99400c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181737"
---
# <a name="microsoft-analytics-platform-system"></a>Microsoft Analytics Platform System

O Microsoft APS (Analytics Platform System), uma plataforma de dados projetada para data warehouse e análise de Big Data, oferece integração de dados profunda, processamento de consulta de ala velocidade, armazenamento altamente escalonável e manutenção simples para sua solução de business intelligence de ponta a ponta.

![Arquitetura de dispositivo](media/architecture-high-level.png "arquitetura de dispositivo")

O Analytics Platform System hospeda o SQL Server PDW (Parallel Data Warehouse), que é o software que executa o data warehouse de MPP (processamento paralelo em massa).

A tecnologia PolyBase combina dados relacionais do PDW e dados do Hadoop de várias origens, incluindo Hortonworks no Windows Server, Hortonworks no Linux, Cloudera no Linux e armazenamento de blobs do Microsoft Azure do HDInsight. Esses recursos de integração de dados avançados, juntamente com a integração profunda com ferramentas de Business Intelligence, permitem que o Analytics Platform System retorne a análise integrada que permite que os tomadores de decisão tomem decisões de negócios melhores e mais criteriosas.

O Analytics Platform System é enviado ao seu data center como um dispositivo de hardware e software pré-instalados e pré-configurados para executar várias cargas de trabalho. Quando você adquire o Analytics Platform System, adquire nós de computação para PDW de acordo com seus requisitos de negócios.

O Analytics Platform System não é apenas rápido e escalonável, ele foi projetado com alta redundância e alta disponibilidade, tornando-o uma plataforma segura para a qual você pode confiar seus dados mais críticos de negócios. O Analytics Platform System foi projetado para maior simplicidade, o que o torna mais fácil de aprender e gerenciar. A tecnologia PolyBase do PDW para analisar dados do Hadoop e sua profunda integração com ferramentas de Business Intelligence o tornam uma plataforma abrangente para criar soluções de ponta a ponta.

## <a name="parallel-data-warehouse-software-designed-for-massively-parallel-processing"></a>Parallel Data Warehouse, software projetado para o processamento paralelo em massa

Use o PDW como o componente de data warehouse relacional central de suas soluções de business intelligence de ponta a ponta. Com o design de MPP (processamento paralelo em massa) do PDW, as consultas normalmente são concluídas 50 vezes mais rapidamente do que os data warehouses tradicionais criados em sistemas de gerenciamento de banco de dados de SMP (multiproccessamento simétrico).

> [!NOTE]
> 50 vezes mais rápido significa que as consultas são concluídas em minutos em vez de horas, em segundos em vez de minutos. Com esse desempenho inovador, os analistas de negócios podem gerar resultados mais amplos mais rápido e podem facilmente executar consultas ad hoc ou fazer drill down nos detalhes. Como resultado, seus negócios podem tomar decisões melhores mais rápido.

Além de alcançar o desempenho de consulta inovador, o PDW facilita:

- Aumento do data warehouse para qualquer lugar de alguns terabytes até 6 petabytes de dados em um único dispositivo adicionando "unidades de escala" para seu sistema existente.

- Confie que seus dados estarão disponíveis quando precisar devido à redundância interna de alta e alta disponibilidade.

- Solucionar os desafios de dados modernos de carregamento e consolidação de dados.

- Integre dados do Hadoop com dados relacionais para análise rápida usando a tecnologia PolyBase altamente em paralelo do PDW.

- O uso de ferramentas de Business Intelligence para criar soluções de ponta a ponta abrangentes.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre os benefícios do PDW, consulte o white paper [A Breakthrough Platform for Next-Generation Data Warehousing and Big Data Solutions](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/dn520808%28v=msdn.10%29) (Uma plataforma inovadora para soluções de Big Data e de data warehouse da próxima geração) no MSDN.
