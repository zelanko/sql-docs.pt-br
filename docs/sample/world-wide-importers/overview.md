---
title: "Visão geral | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: samples
ms.technology: samples
ms.custom: 
ms.date: 01/30/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4d4dcb00-b93e-44db-9d67-061702bba41a
caps.latest.revision: "3"
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 658c1b3ffd44cd2194c75d6ad45888e24e0772c1
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="wide-world-importers-overview"></a>Visão geral da Wide World Importers
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Isso é uma visão geral a empresa fictícia Wide World Importers e os fluxos de trabalho que são abordados nos bancos de dados de exemplo de WideWorldImporters para SQL Server e banco de dados do SQL Azure.  

Wide World Importers (WWI) é um importador de mercadorias novidade atacado e o distribuidor operacional da área de são Francisco compartimento.

Como um atacadista, clientes do WWI são principalmente a empresas que revender para pessoas físicas. WWI vende para clientes de varejo nos Estados Unidos, incluindo repositórios especializado, supermercados, computação lojas, lojas de atração turísticas e algumas pessoas. WWI também vende para outros wholesalers através de uma rede de agentes que promovem os produtos em nome do WWI. Enquanto todos os clientes do WWI atualmente com base nos Estados Unidos, a empresa é destinado enviar por push para expansão em outros países.

WWI compra bens de fornecedores incluindo novidade e fabricantes brinquedos e outros wholesalers novidade. Eles ações mercadorias em suas warehouse WWI e reordenação de fornecedores conforme o necessário para atenderem a pedidos de clientes. Eles também grandes volumes de materiais de empacotamento de compra e vendem-los em quantidades menores como uma conveniência para os clientes.

Recentemente, WWI começou a vender uma variedade de novelties edible como chilli chocolates.  A empresa anteriormente não tinha que manipular itens chilled. Agora, para atender aos requisitos de tratamento de alimentos, eles devem monitorar a temperatura em seu espaço de Resfriador e qualquer de seus caminhões com seções Resfriador.

## <a name="workflow-for-warehouse-stock-items"></a>Fluxo de trabalho para itens de estoque de depósito

O fluxo típico de como os itens são armazenados e distribuídas é o seguinte:
- WWI cria ordens de compra e envia as ordens para os fornecedores.
- Fornecedores enviar os itens, WWI recebe e estoque-los em seu depósito.
- Itens de ordem de clientes do WWI
- WWI preenche o pedido do cliente com itens de estoque no depósito e quando eles não têm estoque suficiente, eles classificam as ações adicionais de fornecedores.
- Alguns clientes não quiserem aguardar os itens que não estão em estoque. Se dizer solicitar cinco diferentes itens de estoque e quatro estão disponíveis, que desejam receber as quatro itens e pendente do item restante. O item seriam-los enviados posteriormente em uma remessa separada.
- WWI faturas de clientes para os itens de estoque, normalmente, convertendo a ordem em uma fatura.
- Os clientes podem solicitar itens que não estão em estoque. Esses itens estão pendente.
- WWI oferece ações itens aos clientes por meio de seus próprios caminhonetes de entrega ou por meio de outros métodos de frete ou serviços de entrega.
- Os clientes pagam faturas para WWI.
- Periodicamente, WWI paga fornecedores para itens que estavam em ordens de compra. Isso é normalmente em algum momento após ter recebido a produtos.

## <a name="data-warehouse-and-analysis-workflow"></a>Fluxo de trabalho Warehouse e análise de dados

Enquanto a equipe em WWI usa o SQL Server Reporting Services para gerar relatórios operacionais do banco de dados de WideWorldImporters, eles também precisam executar uma análise de seus dados e precisa gerar relatórios estratégicos. A equipe de ter criado um modelo de dados multidimensionais em um banco de dados WideWorldImportersDW. Este banco de dados é preenchido por um pacote do Integration Services.

SQL Server Analysis Services é usado para criar modelos de dados analíticos dos dados no modelo de dados multidimensionais. SQL Server Reporting Services é usado para gerar relatórios estratégicos diretamente do modelo de dados dimensionais e também do modelo analítico. Power BI é usado para criar painéis dos mesmos dados. Os painéis de controle são usados nos sites e em telefones e tablets. *Observação: esses relatórios e modelos de dados ainda não estão disponíveis*

## <a name="additional-workflows"></a>Fluxos de trabalho adicionais

Esses são os fluxos de trabalho adicionais.
- Notas de crédito para problemas de WWI quando um cliente não recebe de BOM por algum motivo, ou quando as mercadorias estão com problemas. Esses são tratados como faturas negativas.
- WWI conta periodicamente as quantidades disponíveis dos itens de estoque para garantir que as quantidades de estoque mostradas como disponíveis no sistema são precisas. (O processo de fazer isso é chamado um stocktake).
- Temperaturas frios. Bens transitórios são armazenados em salas refrigerated. Os dados do sensor dessas salas é incluídos no banco de dados para fins de monitoramento e análise.
- Local de veículo de controle. Veículos que transportar mercadorias para WWI incluem sensores que acompanham o local. Esse local é novamente incluído no banco de dados para análise e monitoramento adicional.

## <a name="fiscal-year"></a>Ano fiscal

A empresa opera com um ano fiscal inicia em 1º de novembro.

## <a name="terms-of-use"></a>Termos de uso

A licença para o banco de dados de exemplo e o código de exemplo descrita aqui: [license.txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt)

O banco de dados de exemplo inclui dados públicos que foi carregados de data.gov e EarthData Natural. Os termos de uso estão aqui: [http://www.naturalearthdata.com/about/terms-of-use/](http://www.naturalearthdata.com/about/terms-of-use/)
