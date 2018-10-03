---
title: Importadores mundiais – banco de dados de exemplo do SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cffb25700ccd160f62cc7ad54164bf5fe168225a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832004"
---
# <a name="wide-world-importers-sample-databases-for-microsoft-sql"></a>Bancos de dados de exemplo Wide World Importers para Microsoft SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Isso é uma visão geral da empresa fictícia Wide World Importers e os fluxos de trabalho que são abordados nos bancos de dados de exemplo WideWorldImporters para SQL Server e banco de dados SQL.  

Wide World Importers (WWI) é um importador de mercadorias novidade atacado e o distribuidor operacional da área de San Francisco Baía de são Francisco.

Como um atacadista, os clientes do WWI são principalmente as empresas revendem para indivíduos. WWI vende para clientes do varejo nos Estados Unidos, incluindo repositórios de especialidade, supermercados, computação lojas, lojas de atração turísticas e algumas pessoas. WWI também vende para outras atacadistas através de uma rede de agentes que promovem os produtos em nome do WWI. Embora todos os clientes do WWI no momento, com base nos Estados Unidos, a empresa pretende enviar por push para a expansão para outros países.

WWI compra bens de fornecedores, incluindo novidade e fabricantes de brinquedos e atacadistas outra novidade. Eles ações as mercadorias em seu depósito de importadores mundiais e reordenação de fornecedores, conforme necessário para atender a pedidos do cliente. Eles também adquirir grandes volumes de empacotamento de materiais e vendem-los em quantidades menores como uma conveniência para os clientes.

Recentemente, WWI iniciado para vender uma variedade de novelties edible como chilli chocolates.  A empresa anteriormente não tinha que manipular itens chilled. Agora, para atender aos requisitos de tratamento de alimentos, eles devem monitorar a temperatura em qualquer um dos seus caminhões que têm seções Resfriador e suas salas de Resfriador.

## <a name="workflow-for-warehouse-stock-items"></a>Fluxo de trabalho para itens de estoque do depósito

O fluxo típico de como os itens estão em estoque e distribuídos é da seguinte maneira:
- WWI cria ordens de compra e envia os pedidos para os fornecedores.
- Fornecedores enviam os itens, WWI recebe-los e estoca-los em seu depósito.
- Itens do pedido de clientes de importadores mundiais
- WWI preenche o pedido do cliente com itens de estoque no depósito e quando eles não tiverem estoque suficiente, solicitar ações adicionais aos fornecedores.
- Alguns clientes não deseja esperar que os itens que não estão em estoque. Se eles classificam digamos cinco diferentes itens de estoque e quatro que estão disponíveis, desejam receber os itens de quatro e a ordem pendente do item restante. O item seriam-los enviados mais tarde em uma remessa separada.
- WWI faturas clientes para os itens de estoque, normalmente, convertendo a ordem em uma nota fiscal.
- Os clientes podem solicitar itens que não estão em estoque. Esses itens estão pendente.
- WWI apresenta os itens de estoque para clientes por meio de seus próprios vans entrega ou por meio de outros serviços de entrega ou métodos de frete.
- Os clientes pagam notas fiscais para WWI.
- Periodicamente, WWI paga fornecedores para itens que estavam em ordens de compra. Isso é geralmente em algum momento depois de ter recebido as mercadorias.

## <a name="data-warehouse-and-analysis-workflow"></a>Fluxo de trabalho Warehouse e análise de dados

Enquanto a equipe em WWI usa o SQL Server Reporting Services para gerar relatórios operacionais do banco de dados de WideWorldImporters, eles também precisam executar análises em seus dados e precisa gerar relatórios estratégico. A equipe criou um modelo de dados dimensionais em um banco de dados WideWorldImportersDW. Este banco de dados é preenchido por um pacote do Integration Services.

SQL Server Analysis Services é usado para criar modelos de dados analíticos de dados no modelo de dados dimensional. SQL Server Reporting Services é usado para gerar relatórios estratégico diretamente do modelo de dados dimensionais e também do modelo de análise. Power BI é usado para criar painéis dos mesmos dados. Os painéis são usados em sites e em telefones e tablets. *Observação: esses relatórios e modelos de dados ainda não estão disponíveis*

## <a name="additional-workflows"></a>Fluxos de trabalho adicionais

Esses são fluxos de trabalho adicionais.
- Notas de crédito para problemas de importadores mundiais quando um cliente não recebe o bom por algum motivo, ou quando as mercadorias não estão com defeito. Esses são tratados como faturas negativas.
- WWI conta periodicamente as quantidades disponíveis de itens de estoque para garantir que as quantidades de estoque mostradas como disponíveis em seu sistema sejam precisas. (O processo de fazer isso é chamado um stocktake).
- Temperaturas frias. Bens perishable são armazenados em salas refrigerated. Dados de sensor desses ambientes são incluídos no banco de dados para fins de monitoramento e análise.
- Rastreamento do local do veículo. Veículos que transportar mercadorias para WWI incluem sensores que controla o local. Esse local novamente é incluído no banco de dados para análise e monitoramento ainda mais.

## <a name="fiscal-year"></a>Ano fiscal

A empresa opera com um ano fiscal que inicia em 1º de novembro.

## <a name="terms-of-use"></a>Termos de uso

A licença para o banco de dados de exemplo e o código de exemplo descrita aqui: [License. txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt)

O banco de dados de exemplo inclui dados públicos que foi carregados de data.gov e EarthData Natural. Os termos de uso estão aqui: [http://www.naturalearthdata.com/about/terms-of-use/](http://www.naturalearthdata.com/about/terms-of-use/)
