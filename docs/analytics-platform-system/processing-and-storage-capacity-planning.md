---
title: Capacidade de processamento e armazenamento - Analytics Platform System | Microsoft Docs
description: Seus requisitos de negócios determinam o número de unidades de escala de dados e o tamanho dos discos de nó de computação que você precisa em seu dispositivo do Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f20de8ebc4e3b2970e439dbc413e588aa08b5324
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678546"
---
# <a name="processing-and-storage-capacity-in-analytics-platform-system"></a>Capacidade de processamento e armazenamento no Analytics Platform System
Seus requisitos de negócios determinam o número de unidades de escala de dados e o tamanho dos discos de nó de computação que você precisa em seu dispositivo do Analytics Platform System (APS). Use esses cálculos de processamento e armazenamento para orientar sua capacidade de compra e decisões de planejamento.  
  
  
## <a name="section1"></a>Planejamento de capacidade de processamento  
Desempenho da consulta para o SQL Server Parallel Data Warehouse (PDW) depende muito o número de núcleos de CPU trabalhando em seus dados em paralelo. Dentro dos limites, aumentar o paralelismo melhora o desempenho de consulta de processamento paralelo maciço (MPP). Mesmo se o tamanho dos dados é relativamente pequeno, o poder do mecanismo de consulta MPP é melhorado por ter maior paralelismo.  
  
Por exemplo, um dispositivo com 12 nós de computação tem 192 núcleos de CPU que processam os dados em paralelo. Que é o paralelismo de maneira 192! Um dispositivo conosco de computação 56 tem 896 núcleos todos operando em paralelo. Este magnitude de paralelismo não é possível sem computar MPP.  
  
À medida que aumenta o número de nós de computação, expandindo o dispositivo requer a adição de mais de um nó de computação por vez para obter um benefício perceptível. Fornecedores de hardware dão suporte a configurações somente específicas de unidades de escala de dados para garantir que o benefício de dimensionar o dispositivo supera o custo de redistribuição de dados em mais nós de computação.  
  
### <a name="data-scale-unit-configuration-examples---hpe"></a>Exemplos de configuração de unidade de escala de dados - HPE  
Estes são exemplos de configurações com suporte do HPE para Uunits de escala de dados. Eles podem variar das configurações com suporte mais atuais, mas são fornecidos como um exemplo de como aumentar a capacidade em aproximadamente 20 por cento.  
  
Upgrade é o ganho de porcentagem de capacidade, aumentando a Uunits de escala de dados de uma linha para a próxima. Por exemplo, aumento de unidades de escala de dados de 6 a 8 fornece um upgrade de 33% em núcleos de CPU e memória.  Isso também aumenta o espaço em disco que não é mostrado nesta tabela.  
  
|Unidades de escala de dados|Nós de computação|Núcleos de CPU|Memória (GB)|Upgrade para|  
|--------------------|-----------------|-------------|-----------------|----------|  
|1|2|32|512|-|  
|2|4|64|1024|100%|  
|3|6|96|1536|50%|  
|4|8|128|2048|33%|  
|5|10|160|2560|25%|  
|6|12|192|3072|20%|  
|8|16|256|4096|33%|  
|10|20|320|5120|25%|  
|12|24|384|6144|20%|  
|16|32|512|8192|33%|  
|20|40|640|10240|25%|  
|24|48|768|12288|20%|  
|28|56|896|14336|17%|  
  
Explicação:  
  
-   **Unidades de escala de dados** por dispositivo. Para saber mais sobre unidades de escala de dados, consulte [componentes de Hardware do sistema de plataforma de análise](hardware-components.md).  
  
-   **Nós de computação** por dispositivo.  
  
-   **Núcleos de CPU** por dispositivo. Há 16 núcleos por nó de computação, um núcleo por cada par de disco espelhada. Para a estrutura de disco do nó de computação, consulte [componentes de Hardware do sistema de plataforma de análise](hardware-components.md).  
  
-   **Memória** por dispositivo. Cada núcleo tem 256 GB de memória.  
  
### <a name="data-scale-unit-configuration-examples---dell-quanta"></a>Exemplos de configuração de unidade dados escala – Dell, Quanta  
Estes são exemplos das configurações com suporte de Dell e Quanta para Uunits de escala de dados. Eles podem variar das configurações com suporte mais atuais, mas são fornecidos como um exemplo de como aumentar a capacidade em aproximadamente 20 por cento.  
  
Upgrade é o ganho de porcentagem de capacidade, aumentando a Uunits de escala de dados de uma linha para a próxima. Por exemplo, aumento de unidades de escala de dados de 6 a 8 fornece um upgrade de 33% em núcleos de CPU e memória. Isso também aumenta o espaço em disco que não é mostrado nesta tabela.  
  
|Unidades de escala de dados|Nós de computação|Núcleos de CPU|Memória (GB)|Upgrade para|  
|--------------------|-----------------|-------------|-----------------|----------|  
|1|3|48|768|-|  
|2|6|96|1536|100%|  
|3|9|144|2,304|50%|  
|4|12|192|3,072|33%|  
|5|15|240|3,840|25%|  
|6|18|288|4,608|20%|  
|7|21|336|5,376|17%|  
|8|24|384|6,144|14%|  
|9|27|432|6,912|13%|  
|12|36|576|9,216|33%|  
|15|45|720|11,520|25%|  
|18|54|864|13,824|20%|  
  
## <a name="section2"></a>Planejamento de capacidade de armazenamento  
Esta tabela estima que você pode carregar e armazenar até 6 petabytes de dados descompactados em um dispositivo do Analytics Platform System totalmente criado. 
  
|fornecedor|Tamanho da unidade|Nó de por computação de armazenamento de dados físico|Máximo de nós de computação por rack|Armazenamento físico de dados máximo por rack|Armazenamento de dados de usuário máxima por rack de estimado|Racks máximo|Estima o armazenamento de dados de usuário máxima por dispositivo|  
|----------|--------------|------------------------------------------|----------------------------------|------------------------------------------|------------------------------------------------|-----------------|-----------------------------------------------------|  
|HPE|1 TB|16 TB|8|128 TB|320 TB|7|2,240 TB|  
|HPE|2 TB|32 TB|8|256 TB|640 TB|7|4,480 TB|  
|HPE|4 TB|64 TB|8|512 TB|1280 TB|7|8,960 TB|  
|DELL|1 TB|16 TB|9|144 TB|360 TB|6|2,160 TB|  
|DELL|2 TB|32 TB|9|288 TB|720 TB|6|4,320 TB|  
|DELL|4 TB|64 TB|9|576 TB|1440 TB|6|8,640 TB|   
  
Explicação:  
  
-   **Tamanho da unidade** é 1, 2 ou 4 TB para cada fornecedor de Hardware.  
  
-   **Armazenamento de dados físicos por nó de computação** = (tamanho da unidade) * (16 discos por nó de computação). Os discos espelhados não são incluídos, pois são para redundância.  
  
-   **Nós de computação máxima por rack** é específico para o fornecedor do hardware.  
  
-   **Armazenamento físico de dados máximo por rack** = (armazenamento de dados físicos por nó de computação) * (nós de computação máxima por rack).  
  
-   **Estima o armazenamento de dados de usuário máxima por rack** = (máximo de dados físicos de armazenamento por rack) * (5 para uma taxa de compactação de 5:1) \* (50% para os logs e tempDB). Isso é uma estimativa conservadora para os dados de usuário não compactado que podem ser carregados e armazenados no dispositivo. Essa é uma estimativa e não é imposta pelo software. O armazenamento de dados de usuário real depende de seus dados e sua configuração.  
  
-   **Máximo racks** é específico para cada fornecedor de Hardware.  
  
-   **Estimado de armazenamento de dados máximo por dispositivo** = (armazenamento de dados máximo estimado por rack) * (máximo racks). Isso é uma estimativa conservadora do tamanho total geral de dados do usuário que você pode carregar e armazenar em um dispositivo totalmente criado.  
  
