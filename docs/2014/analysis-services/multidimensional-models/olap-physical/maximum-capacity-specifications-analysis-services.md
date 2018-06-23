---
title: Especificações de capacidade máxima (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Services], maximum number
- objects [Analysis Services], maximum size
ms.assetid: 49fe1673-b908-4c7a-88ff-415efd294d27
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 52c77297ad9b5db79f235611a4ddf47357445629
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115546"
---
# <a name="maximum-capacity-specifications-analysis-services"></a>Especificações de capacidade máxima (Analysis Services)
  As tabelas a seguir especificam os tamanhos e números máximos de vários objetos definidos nos componentes do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] em diferentes modos de implantação de servidor.  
  
 Este tópico contém as seguintes seções:  
  
 [Multidimensional e mineração de dados (DeploymentMode = 0)](#bkmk_OLAP)  
  
 [SharePoint (DeploymentMode = 1)](#bkmk_sharepoint)  
  
 [Tabela (DeploymentMode = 2)](#bkmk_vertipaq)  
  
##  <a name="bkmk_OLAP"></a> Multidimensional e mineração de dados (DeploymentMode = 0)  
 O modo de armazenamento MOLAP que armazena dados e metadados tem limites físicos adicionais em tamanhos de arquivos. Os arquivos de repositório de cadeia de caracteres têm, por padrão, um tamanho máximo de 4 GB. Se você precisar de arquivos maiores para repositórios de cadeia de caracteres, poderá especificar outra arquitetura de armazenamento de cadeia de caracteres. Para obter mais informações, consulte [configurar o armazenamento de cadeia de caracteres para dimensões e partições](../configure-string-storage-for-dimensions-and-partitions.md).  
  
|Object|Tamanho máximo/números|  
|------------|----------------------------|  
|Bancos de dados em uma instância|2^31-1 = 2,147,483,647|  
|Dimensões em um banco de dados|2^31-1 = 2,147,483,647|  
|Atributos em uma dimensão|2^31-1 = 2,147,483,647|  
|Membros em um atributo de dimensão|2^31-1 = 2,147,483,647|  
|Hierarquias definidas pelo usuário em uma dimensão|2^31-1 = 2,147,483,647|  
|Níveis em uma hierarquia definida pelo usuário|2^31-1 = 2,147,483,647|  
|Cubos em um banco de dados|2^31-1 = 2,147,483,647|  
|Grupos de medida em um cubo|2^31-1 = 2,147,483,647|  
|Medidas em um grupo de medidas|2^31-1 = 2,147,483,647|  
|Cálculos em um cubo|2^31-1 = 2,147,483,647|  
|KPIs em um cubo|2^31-1 = 2,147,483,647|  
|Ações em um cubo|2^31-1 = 2,147,483,647|  
|Partições em um cubo|2^31-1 = 2,147,483,647|  
|Traduções em um cubo|2^31-1 = 2,147,483,647|  
|Agregações em uma partição|2^31-1 = 2,147,483,647|  
|Células retornadas por uma consulta|2^31-1 = 2,147,483,647|  
|Tamanho do registro da consulta de origem|64K|  
|Comprimento de nomes de objeto|100 caracteres|  
|Número máximo de estados distintos na coluna de atributos de modelo de mineração de dados|2^31-1 = 2,147,483,647|  
|Número máximo de atributos considerados (seleção de recursos)|2^31-1 = 2,147,483,647|  
  
 Para obter mais informações sobre as diretrizes de nomenclatura de objeto, consulte [objetos e características de objeto ASSL](../scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
 Para obter mais informações sobre limitações da fonte de dados para processamento analítico online (OLAP) e mineração de dados, consulte [fontes de dados com suporte &#40;multidimensionais do SSAS&#41;](../supported-data-sources-ssas-multidimensional.md), [ &#40;Multidimensional do SSAS&#41;](../supported-data-sources-ssas-multidimensional.md), e [objetos e características de objeto ASSL](../scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
##  <a name="bkmk_sharepoint"></a> SharePoint (DeploymentMode = 1)  
  
|Object|Tamanho máximo/números|  
|------------|----------------------------|  
|Bancos de dados em uma instância|2^31-1 = 2,147,483,647|  
|Tabelas em um banco de dados|2^31-1 = 2,147,483,647|  
|Colunas em uma tabela|2 ^ 31-1 = 2.147.483.647 **Aviso:** Número Total de colunas em uma tabela depende do número total de medidas e colunas calculadas associadas à mesma tabela. O número máximo de 'Colunas + Medidas + Colunas Calculadas' para uma tabela é 2^31-1 = 2.147.483.647|  
|Linhas em uma tabela|Ilimitado **Aviso:** com a restrição que nenhum única coluna pode conter mais de 1.999.999.997 valores distintos.|  
|Hierarquias em uma tabela|2^31-1 = 2,147,483,647|  
|Níveis em uma hierarquia|2^31-1 = 2,147,483,647|  
|Relações|2^31-1 = 2,147,483,647|  
|Colunas de chave em uma tabela|2^31-1 = 2,147,483,647|  
|Medidas em uma tabela|2 ^ 31-1 = 2.147.483.647 **Aviso:** o número Total de medidas em uma tabela depende do número total de colunas e colunas calculadas associadas à mesma tabela. O número máximo de 'Colunas + Medidas + Colunas Calculadas' para uma tabela é 2^31-1 = 2.147.483.647|  
|Colunas calculadas em uma tabela|2 ^ 31-1 = 2.147.483.647 **Aviso:** o número Total de colunas calculadas em uma tabela depende do número total de colunas e medidas associados à mesma tabela. O número máximo de 'Colunas + Medidas + Colunas Calculadas' para uma tabela é 2^31-1 = 2.147.483.647|  
|Células retornadas por uma consulta|2^31-1 = 2,147,483,647|  
|Tamanho do registro da consulta de origem|64K|  
|Comprimento de nomes de objeto|100 caracteres|  
  
##  <a name="bkmk_vertipaq"></a> Tabela (DeploymentMode = 2)  
  
|Object|Tamanho máximo/números|  
|------------|----------------------------|  
|Bancos de dados em uma instância|2^31-1 = 2,147,483,647|  
|Tabelas em um banco de dados|2^31-1 = 2,147,483,647|  
|Colunas em uma tabela|2 ^ 31-1 = 2.147.483.647 **Aviso:** Número Total de colunas em uma tabela depende do número total de medidas e colunas calculadas associadas à mesma tabela. O número máximo de 'Colunas + Medidas + Colunas Calculadas' para uma tabela é 2^31-1 = 2.147.483.647|  
|Linhas em uma tabela|Ilimitado **Aviso:** com a restrição de que nenhuma coluna única na tabela pode ter mais de 1.999.999.997 valores distintos.|  
|Hierarquias em uma tabela|2^31-1 = 2,147,483,647|  
|Níveis em uma hierarquia|2^31-1 = 2,147,483,647|  
|Relações|2^31-1 = 2,147,483,647|  
|Colunas de chave em uma tabela|2^31-1 = 2,147,483,647|  
|Medidas em uma tabela|2 ^ 31-1 = 2.147.483.647 **Aviso:** o número Total de medidas em uma tabela depende do número total de colunas e colunas calculadas associadas à mesma tabela. O número máximo de 'Colunas + Medidas + Colunas Calculadas' para uma tabela é 2^31-1 = 2.147.483.647|  
|Colunas calculadas em uma tabela|2 ^ 31-1 = 2.147.483.647 **Aviso:** o número Total de colunas calculadas em uma tabela depende do número total de colunas e medidas associados à mesma tabela. O número máximo de 'Colunas + Medidas + Colunas Calculadas' para uma tabela é 2^31-1 = 2.147.483.647|  
|Células retornadas por uma consulta|2^31-1 = 2,147,483,647|  
|Tamanho do registro da consulta de origem|64K|  
|Comprimento de nomes de objeto|100 caracteres|  
  
## <a name="see-also"></a>Consulte também  
 [Determina o modo de servidor de uma instância do Analysis Services](../../instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Propriedades gerais](../../server-properties/general-properties.md)  
  
  