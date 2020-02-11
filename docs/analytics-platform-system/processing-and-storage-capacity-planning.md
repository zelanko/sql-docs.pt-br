---
title: Capacidade de processamento e armazenamento
description: Seus requisitos de negócios determinam o número de unidades de escala de dados e o tamanho dos discos do nó de computação que você precisa em seu dispositivo de sistema de plataforma de análise (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 143c37b6b55b96f8a0225c98db2212f07b2cd3a5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400540"
---
# <a name="processing-and-storage-capacity-in-analytics-platform-system"></a>Capacidade de processamento e armazenamento no Analytics Platform System
Seus requisitos de negócios determinam o número de unidades de escala de dados e o tamanho dos discos do nó de computação que você precisa em seu dispositivo de sistema de plataforma de análise (APS). Use esses cálculos de armazenamento e processamento para orientar suas decisões de compra e planejamento de capacidade.  
  
  
## <a name="section1"></a>Planejando a capacidade de processamento  
O desempenho de consulta para o PDW (data warehouse paralelo) SQL Server depende muito do número de núcleos de CPU trabalhando em seus dados em paralelo. Dentro dos limites, o paralelismo crescente melhora o desempenho de consulta MPP (processamento paralelo maciço). Mesmo que o tamanho dos dados seja relativamente pequeno, o poder do mecanismo de consulta MPP é aprimorado por ter um paralelismo maior.  
  
Por exemplo, um dispositivo com 12 nós de computação tem 192 núcleos de CPU que processam seus dados em paralelo. Esse é um paralelismo de 192 vias! Um dispositivo com nós de computação 56 tem 896 núcleos funcionando em paralelo. Essa magnitude de paralelismo não é atingível sem a computação MPP.  
  
À medida que o número de nós de computação aumenta, a expansão do dispositivo requer a adição de mais de um nó de computação por vez para obter um benefício perceptível. Os fornecedores de hardware dão suporte apenas a configurações específicas de unidades de escala de dados para garantir que o benefício de dimensionar o dispositivo supera o custo da redistribuição dos dados em mais nós de computação.  
  
### <a name="data-scale-unit-configuration-examples---hpe"></a>Exemplos de configuração de unidade de escala de dados-HPE  
Estes são exemplos das configurações de HPE com suporte para a escala de dados Uunits. Eles podem variar de acordo com as configurações mais atuais com suporte, mas são fornecidos como um exemplo de como aumentar a capacidade em aproximadamente 20%.  
  
O upgrade é o percentual de aumento da capacidade aumentando o Uunits de escala de dados de uma linha para outra. Por exemplo, aumentar as unidades de escala de dados de 6 para 8 oferece um upgrade de 33% em núcleos de CPU e memória.  Ele também aumenta o espaço em disco que não é mostrado nesta tabela.  
  
|Unidades de escala de dados|Nós de computação|Núcleos de CPU|Memória (GB)|Premium|  
|--------------------|-----------------|-------------|-----------------|----------|  
|1|2|32|512|-|  
|2|4|64|1.024|100%|  
|3|6|96|1536|50%|  
|4|8|128|2.048|33%|  
|5|10|160|2560|25%|  
|6|12|192|3072|20%|  
|8|16|256|4096|33%|  
|10|20|320|5120|25%|  
|12|24|384|6144|20%|  
|16|32|512|8192|33%|  
|20|40|640|10240|25%|  
|24|48|768|12288|20%|  
|28|56|896|14336|17%|  
  
Explica  
  
-   **Unidades de escala de dados** por dispositivo. Para saber mais sobre unidades de escala de dados, consulte [componentes de hardware do Analytics Platform System](hardware-components.md).  
  
-   **Nós de computação** por dispositivo.  
  
-   **Núcleos de CPU** por dispositivo. Há 16 núcleos por nó de computação, um núcleo por cada par de disco espelhado. Para a estrutura de discos do nó de computação, consulte [componentes de hardware do Analytics Platform System](hardware-components.md).  
  
-   **Memória** por dispositivo. Cada núcleo tem 256 GB de memória.  
  
### <a name="data-scale-unit-configuration-examples---dell-quanta"></a>Exemplos de configuração de unidade de escala de dados-Dell, Quantity  
Estes são exemplos das configurações Dell e quantas com suporte para Uunits de escala de dados. Eles podem variar de acordo com as configurações mais atuais com suporte, mas são fornecidos como um exemplo de como aumentar a capacidade em aproximadamente 20%.  
  
O upgrade é o percentual de aumento da capacidade aumentando o Uunits de escala de dados de uma linha para outra. Por exemplo, aumentar as unidades de escala de dados de 6 para 8 oferece um upgrade de 33% em núcleos de CPU e memória. Ele também aumenta o espaço em disco que não é mostrado nesta tabela.  
  
|Unidades de escala de dados|Nós de Computação|Núcleos de CPU|Memória (GB)|Premium|  
|--------------------|-----------------|-------------|-----------------|----------|  
|1|3|48|768|-|  
|2|6|96|1536|100%|  
|3|9|144|2.304|50%|  
|4|12|192|3.072|33%|  
|5|15|240|3.840|25%|  
|6|18|288|4.608|20%|  
|7|21|336|5.376|17%|  
|8|24|384|6.144|140|  
|9|27|432|6.912|13|  
|12|36|576|9.216|33%|  
|15|45|720|11.520|25%|  
|18|54|864|13.824|20%|  
  
## <a name="section2"></a>Planejando a capacidade de armazenamento  
Esta tabela estima que você pode carregar e armazenar até 6 petabytes de dados não compactados em um dispositivo de sistema de plataforma de análise totalmente compilado. 
  
|Console|Tamanho da unidade|Armazenamento de dados físicos por nó de computação|Máximo de nós de computação por rack|Armazenamento de dados máximo físico por rack|Armazenamento máximo de dados de usuário estimado por rack|Máximo de racks|Armazenamento máximo de dados do usuário estimado por dispositivo|  
|----------|--------------|------------------------------------------|----------------------------------|------------------------------------------|------------------------------------------------|-----------------|-----------------------------------------------------|  
|HPE|1 TB|16 TB|8|128 TB|320 TB|7|2.240 TB|  
|HPE|2 TB|32 TB|8|256 TB|640 TB|7|4.480 TB|  
|HPE|4 TB|64 TB|8|512 TB|1280 TB|7|8.960 TB|  
|DELL|1 TB|16 TB|9|144 TB|360 TB|6|2.160 TB|  
|DELL|2 TB|32 TB|9|288 TB|720 TB|6|4.320 TB|  
|DELL|4 TB|64 TB|9|576 TB|1440 TB|6|8.640 TB|   
  
Explica  
  
-   O **tamanho da unidade** é 1, 2 ou 4 TB para cada fornecedor de hardware.  
  
-   **Armazenamento de dados físicos por nó de computação** = (tamanho da unidade) * (16 discos por nó de computação). Os discos espelhados não são incluídos, pois são para redundância.  
  
-   O **máximo de nós de computação por rack** é específico para o fornecedor de hardware.  
  
-   **Armazenamento de dados máximo físico por rack** = (armazenamento de dados físicos por nó de computação) * (nós de computação máximo por rack).  
  
-   **Armazenamento máximo de dados de usuário estimado por rack** = (armazenamento de dados máximo físico por rack) * (5 para uma \* taxa de compactação 5:1) (50% para logs e tempdb). Essa é uma estimativa conservadora para os dados de usuário não compactados que podem ser carregados e armazenados no dispositivo. Essa é uma estimativa e não é imposta pelo software. O armazenamento real de dados do usuário depende de seus dados e de sua configuração.  
  
-   O **máximo de racks** é específico para cada fornecedor de hardware.  
  
-   **Armazenamento de dados máximo estimado por dispositivo** = (armazenamento de dados máximo estimado por rack) * (máximo de racks). Essa é uma estimativa conservadora do tamanho total geral dos dados do usuário que você pode carregar e armazenar em um dispositivo totalmente compilado.  
  
