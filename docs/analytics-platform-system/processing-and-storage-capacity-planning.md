---
title: Capacidade de processamento e armazenamento - Analytics Platform System | Microsoft Docs
description: Seus requisitos de negócios determinam o número de unidades de escala de dados e o tamanho dos discos de nó de computação que você precisa em seu dispositivo Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f552372ac108d219ad410b88ec9911ecaea63ab3
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539596"
---
# <a name="processing-and-storage-capacity-in-analytics-platform-system"></a>Capacidade de processamento e armazenamento no sistema de plataforma de análise
Seus requisitos de negócios determinam o número de unidades de escala de dados e o tamanho dos discos de nó de computação que você precisa em seu dispositivo Analytics Platform System (APS). Use esses cálculos de processamento e armazenamento para orientar sua capacidade de compra e decisões de planejamento.  
  
  
## <a name="section1"></a>Planejamento de capacidade de processamento  
Desempenho de consulta para SQL Server Parallel Data Warehouse (PDW) depende muito o número de núcleos de CPU trabalhando em seus dados em paralelo. Dentro dos limites, aumentar o paralelismo melhora o desempenho de consulta de processamento paralelo em massa (MPP). Mesmo que o tamanho de dados for relativamente pequeno, a potência do mecanismo de consulta MPP é melhorada por ter maior paralelismo.  
  
Por exemplo, um dispositivo com 12 nós de computação tem 192 núcleos de CPU que processam os dados em paralelo. Que é o paralelismo de maneira 192! Um dispositivo conosco de computação 56 tem 896 núcleos trabalhando todos em paralelo. Este magnitude de paralelismo não é possível sem MPP computação.  
  
À medida que aumenta o número de nós de computação, expandindo o dispositivo requer a adição de mais de um nó de computação por vez para obter um benefício perceptível. Fornecedores de hardware dão suporte a configurações específicas de unidades de escala de dados para garantir que o benefício de dimensionamento do dispositivo supera o custo de redistribuição de dados em mais nós de computação.  
  
### <a name="data-scale-unit-configuration-examples---hpe"></a>Exemplos de configuração de unidade de escala de dados - HPE  
Estes são exemplos de configurações com suporte HPE para Uunits de escala de dados. Eles podem variar das configurações com suporte mais recentes, mas são fornecidos como um exemplo de como aumentar a capacidade em aproximadamente 20 por cento.  
  
Upgrade é o ganho de porcentagem de capacidade, aumentando a escala de dados Uunits de uma linha para a próxima. Por exemplo, aumentar as unidades de escala de dados de 6 a 8 fornece um upgrade 33% em núcleos de CPU e memória.  Ele também aumenta o espaço em disco que não é mostrado nesta tabela.  
  
|Unidades de escala de dados|Nós de computação|Núcleos de CPU|Memória (GB)|Upgrade|  
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
  
-   **Unidades de escala de dados** por dispositivo. Para saber mais sobre as unidades de escala de dados, consulte [componentes de Hardware do sistema de plataforma de análise de](hardware-components.md).  
  
-   **Nós de computação** por dispositivo.  
  
-   **Núcleos de CPU** por dispositivo. Há 16 núcleos por nó de computação, um núcleo por cada par de disco espelhado. Para a estrutura de disco do nó de computação, consulte [componentes de Hardware do sistema de plataforma de análise de](hardware-components.md).  
  
-   **Memória** por dispositivo. Cada núcleo tem 256 GB de memória.  
  
### <a name="data-scale-unit-configuration-examples--dell-quanta"></a>Exemplos de configuração de unidade dados escala – Dell, Quanta  
Estes são exemplos das configurações com suporte de Dell e Quanta para Uunits de escala de dados. Eles podem variar das configurações com suporte mais recentes, mas são fornecidos como um exemplo de como aumentar a capacidade em aproximadamente 20 por cento.  
  
Upgrade é o ganho de porcentagem de capacidade, aumentando a escala de dados Uunits de uma linha para a próxima. Por exemplo, aumentar as unidades de escala de dados de 6 a 8 fornece um upgrade 33% em núcleos de CPU e memória. Ele também aumenta o espaço em disco que não é mostrado nesta tabela.  
  
|Unidades de escala de dados|Nós de computação|Núcleos de CPU|Memória (GB)|Upgrade|  
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
Esta tabela estima que você pode carregar e armazenar até 6 petabytes de dados não compactados em um dispositivo Analytics Platform System totalmente criado. 
  
|Fornecedor|Tamanho da unidade|Nó de por computação de armazenamento de dados físicos|Máximo de nós de computação por rack|Armazenamento físico de dados máximo por rack|Estima o armazenamento de dados de usuário máximo por rack|Racks máximo|Estima o armazenamento de dados de usuário máximo por dispositivo|  
|----------|--------------|------------------------------------------|----------------------------------|------------------------------------------|------------------------------------------------|-----------------|-----------------------------------------------------|  
|HPE|1 TB|16 TB|8|128 TB|320 TB|7|2,240 TB|  
|HPE|2 TB|32 TB|8|256 TB|640 TB|7|4,480 TB|  
|HPE|3 TB|48 TB|8|384 TB|960 TB|7|6,720 TB|  
|DELL|1 TB|16 TB|9|144 TB|360 TB|6|2,160 TB|  
|DELL|2 TB|32 TB|9|288 TB|720 TB|6|4.320 TB|  
|DELL|3 TB|48 TB|9|432 TB|1080 TB|6|6,480 TB|  
  
Explicação:  
  
-   **Tamanho da unidade** é 1, 2 ou 3 TB para cada fornecedor de Hardware.  
  
-   **Armazenamento de dados físico por nó de computação** = (tamanho da unidade) * (16 discos por nó de computação). Os discos espelhados não são incluídos, desde que eles são para redundância.  
  
-   **Nós de computação máxima por rack** é específico para o fornecedor do hardware.  
  
-   **Armazenamento físico de dados máximo por rack** = (armazenamento de dados físico por nó de computação) * (nós de computação máxima por rack).  
  
-   **Estima o armazenamento de dados de usuário máximo por rack** = (armazenamento de dados máximo físico por rack) * (5 para uma taxa de compactação de 5:1) \* (50% de logs e tempDB). Isso é uma estimativa conservadora para os dados do usuário não compactados que podem ser carregados e armazenados no dispositivo. Essa é uma estimativa e não é imposta pelo software. O armazenamento de dados de usuário real depende de seus dados e sua configuração.  
  
-   **Racks máximo** é específica para cada fornecedor de Hardware.  
  
-   **Estimado de armazenamento de dados máximo por dispositivo** = (armazenamento de dados máximo estimado por rack) * (racks máximo). Isso é uma estimativa conservadora do tamanho total geral de dados de usuário que você pode carregar e armazenar em um dispositivo totalmente criado.  
  
