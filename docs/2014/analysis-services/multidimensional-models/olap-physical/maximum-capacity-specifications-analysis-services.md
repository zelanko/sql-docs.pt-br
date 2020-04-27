---
title: Especificações de capacidade máxima (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Services], maximum number
- objects [Analysis Services], maximum size
ms.assetid: 49fe1673-b908-4c7a-88ff-415efd294d27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 561cbbb64734c117b295ca6d97420b6980fa5428
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62725490"
---
# <a name="maximum-capacity-specifications-analysis-services"></a>Especificações de capacidade máxima (Analysis Services)
  As tabelas a seguir especificam os tamanhos e números máximos de vários objetos definidos nos componentes do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] em diferentes modos de implantação de servidor.  
  
 Este tópico contém as seguintes seções:  
  
 [Multidimensional e mineração de dados (DeploymentMode=0)](#bkmk_OLAP)  
  
 [SharePoint (DeploymentMode=1)](#bkmk_sharepoint)  
  
 [Tabular (DeploymentMode=2)](#bkmk_vertipaq)  
  
##  <a name="multidimensional-and-data-mining-deploymentmode0"></a><a name="bkmk_OLAP"></a>Multidimensional e mineração de dados (Deploymentmode = 0)  
 O modo de armazenamento MOLAP que armazena dados e metadados tem limites físicos adicionais em tamanhos de arquivos. Os arquivos de repositório de cadeia de caracteres têm, por padrão, um tamanho máximo de 4 GB. Se você precisar de arquivos maiores para repositórios de cadeia de caracteres, poderá especificar outra arquitetura de armazenamento de cadeia de caracteres. Para obter mais informações, consulte [Configurar o armazenamento de cadeia de caracteres para dimensões e partições](../configure-string-storage-for-dimensions-and-partitions.md).  
  
|Objeto|Tamanho máximo/números|  
|------------|----------------------------|  
|Bancos de dados em uma instância|2 ^ 31-1 = 2.147.483.647|  
|Dimensões em um banco de dados|2 ^ 31-1 = 2.147.483.647|  
|Atributos em uma dimensão|2 ^ 31-1 = 2.147.483.647|  
|Membros em um atributo de dimensão|2 ^ 31-1 = 2.147.483.647|  
|Hierarquias definidas pelo usuário em uma dimensão|2 ^ 31-1 = 2.147.483.647|  
|Níveis em uma hierarquia definida pelo usuário|2 ^ 31-1 = 2.147.483.647|  
|Cubos em um banco de dados|2 ^ 31-1 = 2.147.483.647|  
|Grupos de medida em um cubo|2 ^ 31-1 = 2.147.483.647|  
|Medidas em um grupo de medidas|2 ^ 31-1 = 2.147.483.647|  
|Cálculos em um cubo|2 ^ 31-1 = 2.147.483.647|  
|KPIs em um cubo|2 ^ 31-1 = 2.147.483.647|  
|Ações em um cubo|2 ^ 31-1 = 2.147.483.647|  
|Partições em um cubo|2 ^ 31-1 = 2.147.483.647|  
|Traduções em um cubo|2 ^ 31-1 = 2.147.483.647|  
|Agregações em uma partição|2 ^ 31-1 = 2.147.483.647|  
|Células retornadas por uma consulta|2 ^ 31-1 = 2.147.483.647|  
|Tamanho do registro da consulta de origem|64 K|  
|Comprimento de nomes de objeto|100 caracteres|  
|Número máximo de estados distintos na coluna de atributos de modelo de mineração de dados|2 ^ 31-1 = 2.147.483.647|  
|Número máximo de atributos considerados (seleção de recursos)|2 ^ 31-1 = 2.147.483.647|  
  
 Para obter mais informações sobre as diretrizes de nomenclatura de objeto, consulte [objetos ASSL e características de objeto](../scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
 Para obter mais informações sobre limitações de fonte de dados para OLAP (processamento analítico online) e Data Mining, consulte [fontes de dados com suporte &#40;&#41;multidimensional do SSAS ](../supported-data-sources-ssas-multidimensional.md), [fontes de dados com suporte &#40;objetos multi&#41;DIMENSIONAis do SSAS ](../supported-data-sources-ssas-multidimensional.md)e características do [objeto ASSL](../scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
##  <a name="sharepoint-deploymentmode1"></a><a name="bkmk_sharepoint"></a>SharePoint (Deploymentmode = 1)  
  
|Objeto|Tamanho máximo/números|  
|------------|----------------------------|  
|Bancos de dados em uma instância|2 ^ 31-1 = 2.147.483.647|  
|Tabelas em um banco de dados|2 ^ 31-1 = 2.147.483.647|  
|Colunas em uma tabela|2 ^ 31-1 = 2.147.483.647 **AVISO:** o número total de colunas em uma tabela depende do número total de medidas e colunas calculadas associadas à mesma tabela. O número máximo de 'Colunas + Medidas + Colunas Calculadas' para uma tabela é 2^31-1 = 2.147.483.647|  
|Linhas em uma tabela|**Aviso ilimitado:** com a restrição de que nenhuma coluna única pode conter mais de 1.999.999.997 valores distintos.|  
|Hierarquias em uma tabela|2 ^ 31-1 = 2.147.483.647|  
|Níveis em uma hierarquia|2 ^ 31-1 = 2.147.483.647|  
|Relações|2 ^ 31-1 = 2.147.483.647|  
|Colunas de chave em uma tabela|2 ^ 31-1 = 2.147.483.647|  
|Medidas em uma tabela|2 ^ 31-1 = 2.147.483.647 **AVISO:** o número total de medidas em uma tabela depende do número total de colunas e colunas calculadas associadas à mesma tabela. O número máximo de 'Colunas + Medidas + Colunas Calculadas' para uma tabela é 2^31-1 = 2.147.483.647|  
|Colunas calculadas em uma tabela|2 ^ 31-1 = 2.147.483.647 **AVISO:** o número total de colunas calculadas em uma tabela depende do número total de colunas e medidas associadas à mesma tabela. O número máximo de 'Colunas + Medidas + Colunas Calculadas' para uma tabela é 2^31-1 = 2.147.483.647|  
|Células retornadas por uma consulta|2 ^ 31-1 = 2.147.483.647|  
|Tamanho do registro da consulta de origem|64 K|  
|Comprimento de nomes de objeto|100 caracteres|  
  
##  <a name="tabular-deploymentmode2"></a><a name="bkmk_vertipaq"></a>Tabular (Deploymentmode = 2)  
  
|Objeto|Tamanho máximo/números|  
|------------|----------------------------|  
|Bancos de dados em uma instância|2 ^ 31-1 = 2.147.483.647|  
|Tabelas em um banco de dados|2 ^ 31-1 = 2.147.483.647|  
|Colunas em uma tabela|2 ^ 31-1 = 2.147.483.647 **AVISO:** o número total de colunas em uma tabela depende do número total de medidas e colunas calculadas associadas à mesma tabela. O número máximo de 'Colunas + Medidas + Colunas Calculadas' para uma tabela é 2^31-1 = 2.147.483.647|  
|Linhas em uma tabela|**Aviso ilimitado:** com a restrição de que nenhuma coluna única na tabela pode ter mais de 1.999.999.997 valores distintos.|  
|Hierarquias em uma tabela|2 ^ 31-1 = 2.147.483.647|  
|Níveis em uma hierarquia|2 ^ 31-1 = 2.147.483.647|  
|Relações|2 ^ 31-1 = 2.147.483.647|  
|Colunas de chave em uma tabela|2 ^ 31-1 = 2.147.483.647|  
|Medidas em uma tabela|2 ^ 31-1 = 2.147.483.647 **AVISO:** o número total de medidas em uma tabela depende do número total de colunas e colunas calculadas associadas à mesma tabela. O número máximo de 'Colunas + Medidas + Colunas Calculadas' para uma tabela é 2^31-1 = 2.147.483.647|  
|Colunas calculadas em uma tabela|2 ^ 31-1 = 2.147.483.647 **AVISO:** o número total de colunas calculadas em uma tabela depende do número total de colunas e medidas associadas à mesma tabela. O número máximo de 'Colunas + Medidas + Colunas Calculadas' para uma tabela é 2^31-1 = 2.147.483.647|  
|Células retornadas por uma consulta|2 ^ 31-1 = 2.147.483.647|  
|Tamanho do registro da consulta de origem|64 K|  
|Comprimento de nomes de objeto|100 caracteres|  
  
## <a name="see-also"></a>Consulte Também  
 [Determinar o modo de servidor de uma instância de Analysis Services](../../instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Propriedades gerais](../../server-properties/general-properties.md)  
  
  
