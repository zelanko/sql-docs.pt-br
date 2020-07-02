---
title: Importadores mundiais-banco de dados de exemplo para SQL | Microsoft Docs
description: Saiba como os bancos de dados de exemplo WideWorldImporters dão suporte aos fluxos de trabalho da empresa fictícia WideWorldImporters.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: adc2e7d74f8479384bd9f34b5442e796e4b74d66
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718543"
---
# <a name="wide-world-importers-sample-databases-for-microsoft-sql"></a>Bancos de dados de exemplo de importadores mundiais para Microsoft SQL
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]
Esta é uma visão geral dos importadores mundiais da empresa fictícia e os fluxos de trabalho que são abordados nos bancos de dados de exemplo WideWorldImporters para o SQL Server e o Azure SQL Database.  

A Wide World Importers (WWI) é um atacadista de novidades de bens e distribuidores operando da área de compartimento de San Francisco.

Como um atacadista, os clientes do WWI são principalmente as empresas que revendem para indivíduos. A WWI vende para clientes de varejo em toda a Estados Unidos, incluindo lojas especiais, supermercados, lojas de computação, Tourist atração shops e algumas pessoas. O WWI também vende para outros atacadistas por meio de uma rede de agentes que promovem os produtos em nome de WWI. Embora todos os clientes de WWI estejam atualmente baseados na Estados Unidos, a empresa está pretendendo enviar por push para a expansão em outros países.

O WWI compra bens de fornecedores, incluindo fabricantes de novidade e de brinquedos e outros atacadistas de novidade. Eles estocam as mercadorias em seu depósito WWI e reordenam de fornecedores conforme necessário para atender pedidos de clientes. Eles também compram grandes volumes de materiais de empacotamento e os vendem em quantidades menores como uma conveniência para os clientes.

Recentemente, WWI começou a vender uma variedade de Novelties edible como chocolates chilli.  A empresa anteriormente não tinha que lidar com itens resfriados. Agora, para atender aos requisitos de manuseio de alimentos, eles devem monitorar a temperatura em sua sala de resfriador e em qualquer um dos caminhões que tenham seções mais resfriadoras.

## <a name="workflow-for-warehouse-stock-items"></a>Fluxo de trabalho para itens de estoque do depósito

O fluxo típico de como os itens são incluídos em estoque e distribuído é o seguinte:
- O WWI cria pedidos de compra e envia os pedidos aos fornecedores.
- Os fornecedores enviam os itens, o WWI os recebe e os coloca em seu depósito.
- Os clientes solicitam itens do WWI
- WWI preenche a ordem do cliente com itens de estoque no warehouse e, quando eles não têm estoque suficiente, eles ordenam o estoque adicional dos fornecedores.
- Alguns clientes não desejam aguardar os itens que não estão em estoque. Se eles solicitarem cinco itens de estoque diferentes e quatro estiverem disponíveis, eles desejarão receber os quatro itens e fazer uma ordem pendente do item restante. O item seria então enviado posteriormente em uma remessa separada.
- O WWI fatura os clientes para os itens de estoque, normalmente convertendo o pedido em uma fatura.
- Os clientes podem solicitar itens que não estão em estoque. Esses itens são ordens pendentes.
- O WWI fornece itens de estoque aos clientes por meio de seu próprio vans de entrega ou por meio de outros métodos de Courier ou de frete.
- Os clientes pagam faturas para WWI.
- Periodicamente, o WWI paga os fornecedores por itens que estavam em ordens de compra. Isso costuma ser um pouco depois de receber as mercadorias.

## <a name="data-warehouse-and-analysis-workflow"></a>Fluxo de trabalho de análise e data warehouse

Embora a equipe em WWI Use SQL Server Reporting Services para gerar relatórios operacionais a partir do banco de dados WideWorldImporters, elas também precisam executar análises sobre os respectivos e precisam gerar relatórios estratégicos. A equipe criou um modelo de dados dimensional em uma WideWorldImportersDW de banco de dado. Esse banco de dados é preenchido por um pacote de Integration Services.

SQL Server Analysis Services é usado para criar modelos de dados analíticos a partir dos dados no modelo de dados dimensional. SQL Server Reporting Services é usado para gerar relatórios estratégicos diretamente do modelo de dados dimensional e também do modelo analítico. Power BI é usado para criar painéis com base nos mesmos dados. Os painéis são usados em sites e em telefones e tablets. *Observação: esses modelos de dados e relatórios ainda não estão disponíveis*

## <a name="additional-workflows"></a>Fluxos de trabalho adicionais

Esses são fluxos de trabalho adicionais.
- WWI emite notas de crédito quando um cliente não recebe o bom por algum motivo, ou quando os bens são defeituosos. Elas são tratadas como notas fiscais negativas.
- O WWI conta periodicamente as quantidades de itens de estoque disponíveis para garantir que as quantidades de estoque mostradas conforme disponível em seu sistema sejam precisas. (O processo de fazer isso é chamado de Stocktake).
- Temperaturas da sala fria. Os bens de perishable são armazenados em salas refrigeradas. Os dados do sensor dessas salas são ingeridos no banco de dado para fins de monitoramento e análise.
- Acompanhamento do local do veículo. Os veículos que transportam mercadorias para WWI incluem sensores que acompanham o local. Esse local é novamente ingerido no banco de dados para monitoramento e análise adicional.

## <a name="fiscal-year"></a>Ano fiscal

A empresa opera com um ano financeiro que começa em 1º de novembro.

## <a name="terms-of-use"></a>Termos de uso

A licença para o banco de dados de exemplo e o código de exemplo é descrita aqui: [license.txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt)

O banco de dados de exemplo do inclui um dado público que foi carregado de data.gov e natural EarthData. Os termos de uso estão aqui:[https://www.naturalearthdata.com/about/terms-of-use/](https://www.naturalearthdata.com/about/terms-of-use/)
